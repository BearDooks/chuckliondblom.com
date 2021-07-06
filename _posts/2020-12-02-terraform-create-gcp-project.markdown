---
title: "Using Terraform To Create A GCP Project"
description: "How to create a GCP project using terraform to have a standard and easy to use method"
date:  2020-12-02 10:00:00 -0500
categories: [GCP, Terraform, Guide]
tags: [GCP, Terraform, GCP Project, Guide, Scripting]
author: chuck lindblom
sharing: true
show_author_profile: true
cover: /assets/images/terraform_logo.png
show_excerpt: true
excerpt_type: html
---

# Creating a GCP Project with Terraform

Like most jobs today, mine requires me to automate as much of it as possible. One of the things that seemed like an easy goal was to auto the creation of a GCP Project using a tool. We used to use Google Deployment Manager, but soon found it was more of a pain than we wanted to keep up to date.

# Project Layout

When creating this I laid out the files in easy to use sections. I also made sure to use the *depends_on* line a lot so I could ensue that everything was working in the order I wanted

* project.tf - Used to create the basic project
* services.tf - Used to turn on APIs
* iam.tf _ Used to create all IAM policies
* network.tf - Used to create basic networking
* storage.tf - Used to create standard buckets
* serviceaccounts.tf - Used to make any service accounts needed

# Project Files

Below I will break down each file and what iot is used for as well as the code inside of it

## project.tf

In this file I look for a few variables that help me create the project including the name, what folder it should live in, and a simple label to be applied to it. I also setup google as the provider since I will be using GCP. To make life easy I setup a service account ahead of time that has the ability to create projects and modify IAM throughout my environment. I then took the JSON key from it and I insert the path so the script knows what to use.

    // Variables needed for this project
    variable "project_name" {
    type        = string
    description = "The name of the project that will be assigned in GCP"
    }

    variable "project_folder" {
    type        = string
    description = "The folder ID the project will live in"
    }

    variable "label1" {
    type        = string
    description = "A label that we can use in the project"
    }

    //**********
    //Terraform Provider Info
    //***********

    // Setup Google as provider for this project
    // credentials is a file that has the key for the terraform service account
    provider "google" {
    credentials = "FULL PATH TO CREDENTIALS"
    region      = "us-east1"
    zone        = "us-east1-b"
    }

    // Setup project, billing account, and labels
    resource "google_project" "project" {
    name            = var.project_name
    project_id      = var.project_name
    billing_account = "INSERT BILLING ACCOUNT # HERE"
    folder_id          = var.project_folder
    labels = {
        label1 = var.label1
        }
    }

## services.tf

In this file I lay out all the APIs I need turned on. I have shorten this list, but you can use it to get a guide on what it should look like

    //****************************************
    // Services and APIs
    //****************************************

    resource "google_project_service" "compute_api" {
    project = google_project.project.project_id
    service = "compute.googleapis.com"

    disable_dependent_services = true
    }

    resource "google_project_service" "deploymentmanager_api" {
    project = google_project.project.project_id
    service = "deploymentmanager.googleapis.com"

    disable_dependent_services = true
    }

## iam.tf

This file is used to set all of the IAM permissions in the project. It can get quite large if you have a lot of sets you need to make, and I am sure there are better ways to write it, but this is currently what is working for us. I have also shortened this list.

You will notice these code blocks all have a line *depends_on*. This forces terraform to wait until the codeblock in that line has finished running. This is important to have since it helps make sure accounts have been created or APIs have been enabled before terraform tries to run this.

    //****************************************
    // IAM Permissions
    //****************************************

    resource "google_project_iam_member" "owner" {
    depends_on = [google_service_account.service_account]
    project = google_project.project.project_id
    role    = "roles/owner"
    member  = "serviceAccount:service_account@serviceaccount.com"
    }

    resource "google_project_iam_member" "owner2" {
    depends_on = [google_service_account.service_account]
    project = google_project.project.project_id
    role    = "roles/owner"
    member  = "user:email@email.com"
    }

## network.tf

Here we setup a basic VPC network with a NAT Gateway so there is no need for public IPs.

    //****************************************
    // Networking
    //****************************************

    resource "google_compute_network" "vpc_network" {
    depends_on              = [google_project_service.compute_api]
    name                    = join("", [google_project.project.project_id, "-vpc"])
    project                 = google_project.project.project_id
    auto_create_subnetworks = false
    }

    resource "google_compute_subnetwork" "default" {
    depends_on               = [google_compute_network.vpc_network]
    name                     = "project-subnet"
    project                  = google_project.project.project_id
    ip_cidr_range            = "10.142.0.0/20"
    region                   = "us-east1"
    network                  = join("", [google_project.project.project_id, "-vpc"])
    private_ip_google_access = true
    }

    resource "google_compute_router" "default" {
    depends_on = [google_compute_subnetwork.default]
    name       = join("", [google_project.project.project_id, "-cr"])
    project    = google_project.project.project_id
    network    = join("", [google_project.project.project_id, "-vpc"])
    bgp {
        asn               = 64512
        advertise_mode    = "DEFAULT"
        }
    }

    resource "google_compute_router_nat" "nat_gateway" {
    depends_on                         = [google_compute_router.default]
    name                               = join("", [google_project.project.project_id, "-natgwy"])
    project                            = google_project.project.project_id
    router                             = join("", [google_project.project.project_id, "-cr"])
    region                             = "us-east1"
    nat_ip_allocate_option             = "AUTO_ONLY"
    source_subnetwork_ip_ranges_to_nat = "ALL_SUBNETWORKS_ALL_IP_RANGES"
    }

    output "project_id" {
    value = google_project.project.project_id
    }

## storage.tf

In this block we create a simple bucket for project data. Note that we have a line *depends_on* and we make sure the storage API has been enabled. If it is not, the terraform script will possibly fail.

    //****************************************
    // Storage Buckets
    //****************************************

    resource "google_storage_bucket" "project-data" {
    depends_on = [google_project_service.storage-component_api]
    project  = google_project.project.project_id
    name     = join("", [google_project.project.project_id, "-project-data"])
    location = "us-east1"
    }

## serviceaccounts.tf

The following code makes a simple service account inside the project that we can use.

    //****************************************
    // Service Accounts
    //****************************************

    // Normal service account used for everything inside of the project
    resource "google_service_account" "service_account" {
    project      = google_project.project.project_id
    account_id   = join("", ["svc-", google_project.project.project_id])
    display_name = join("", ["svc-", google_project.project.project_id])
    }

# Running the terraform script

Running the script is pretty easy. The first step is making sure you have terraform installed by going to <a href="https://www.terraform.io/">their website.</a> Once you have this installed and all the scripts are in the same directory, you can run some simple commands.

To plan the terraform changes, you can run the following command and terraform will print out everything it wants to do

    terraform plan -var="project_name=PROJECT_NAME" -var="project_folder=PROJECT_FOLDER" -var="label1=LABEL1_DATA" 

To apply the terraform changes, you can run the following command and terraform will print out everything it wants to do, and then do it

    terraform apply -var="project_name=PROJECT_NAME" -var="project_folder=PROJECT_FOLDER" -var="label1=LABEL1_DATA" 
