---
title: "Setting up Postfix on CentOS7"
date: 2015-07-01 15:48:26 -0500
categories: [guide]
tags: [centos, centos7, "7", email, linux, postfix, server]
author: chuck lindblom
sharing: true
show_author_profile: true
---
The following guide is the step by step instructions I wrote out. These instructions will allow you to install Postfix on CentOS7.

<figure>
	<a href="/images/postfix.png"><img src="images/postfix.png" alt=""></a>
</figure>

## **Pre Reqs**

yum update

yum install nano

yum install wget

&nbsp;

## **Install Webmin**
<!--more-->
nano /etc/yum.repos.d/webmin.repo

&nbsp;

\*\* Add the following \*\*

&nbsp;

[Webmin]

name=Webmin Distribution Neutral

#baseurl=http://download.webmin.com/download/yum

mirrorlist=http://download.webmin.com/download/yum/mirrorlist

enabled=1

&nbsp;

**

&nbsp;

wget http://www.webmin.com/jcameron-key.asc

rpm &#8211;import jcameron-key.asc

&nbsp;

yum install webmin

&nbsp;

## **Turn Off SELINUX**

&nbsp;

nano /etc/selinux/config

&nbsp;

\*\* Replace with \*\*

&nbsp;

\# This file controls the state of SELinux on the system.

\# SELINUX= can take one of these three values:

\#     enforcing &#8211; SELinux security policy is enforced.

\#     permissive &#8211; SELinux prints warnings instead of enforcing.

\#     disabled &#8211; No SELinux policy is loaded.

SELINUX=disabled

\# SELINUXTYPE= can take one of three two values:

\#     targeted &#8211; Targeted processes are protected,

\#     minimum &#8211; Modification of targeted policy. Only selected processes are protected.

\#     mls &#8211; Multi Level Security protection.

SELINUXTYPE=targeted

&nbsp;

**

&nbsp;

reboot

&nbsp;

## **Open Firewall**

&nbsp;

firewall-cmd &#8211;permanent &#8211;zone=public &#8211;add-service=http

firewall-cmd &#8211;permanent &#8211;zone=public &#8211;add-service=https

firewall-cmd &#8211;permanent &#8211;zone=public &#8211;add-service=smtp

firewall-cmd &#8211;permanent &#8211;zone=public &#8211;add-port=10000/tcp

firewall-cmd &#8211;permanent &#8211;zone=public &#8211;add-port=25/tcp

firewall-cmd &#8211;reload

&nbsp;

## **Install HTTPD**

&nbsp;

yum install httpd

chkconfig httpd on

service start httpd
