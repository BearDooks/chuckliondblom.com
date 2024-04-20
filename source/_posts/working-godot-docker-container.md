---
title: Working Godot Docker Container
date:  2021-04-05 14:00:00
categories: [News]
tags: [Godot, Docker, Automation, github, CentOS, GodotNuts]
---

# The Backstory

Last year I posted an article about making a <a href="https://www.chucklindblom.com/Godot-Server-In-Docker-Container/">godot server in docker</a>, and while I was happy with it, I was not convinced that it was really done. I knew I could do more, but I just didn't have the time or the skills to work on it. Cut to now, and I am working with an awesome team that is helping to implement Firestore natively into Godot (More on that later). You can check out all the awesome work for that <a href="https://github.com/GodotNuts">here</a>

# Docker Loves Godot

I started to look back on the docker container I made, and I noticed a bunch of problems with it. The first being you needed to add CentOS to make the container to work. The idea is to keep these things small, and adding CentOS didn't really play nice with that ideal. I also wanted to make it so you pointed the container at your game, and it would just export it for you and run it. How cool would that be right?

<!--more-->

Working with the awesome team at GodotNuts, I came up with a plan and talked to them about it. They really seemed to like the idea so I went with it. The first thing I had to do was remove CentOS to keep the image small. You will notice that later in the docker files that I switched over to Alpine.

# The Code

You can see everything <a href="https://github.com/GodotNuts/GodotServer-Docker">here</a> as well as the other cool projects GodotNuts has been working on.

## Dockerfile

The Dockerfile was the first thing I had to work on. I took some parts of the old one that helped download Godot and removed everything else. I wanted to start fresh so I would not get caught in my previous mistakes. The first thing I needed to get working was Alpine Linux. Not more would I bog down the system with the CentOS install. Most everything worked, but I needed a special package to allow the running of Godot. You can see it in these lines

    # Allow this to run Godot
    RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.31-r0/glibc-2.31-r0.apk
    RUN apk add --allow-untrusted glibc-2.31-r0.apk

After that it was a matter of getting the variables right for the script. I wanted the user to be able to decide which version of Godot they wanted to use as well as what the repo was that held their game. That is also were the script knows to go to for downloading the app and installing it before running.

You will notice in this version of the script I have a section that installs the export templates for Godot and then runs some commands to make the came for you. I also have another version as well where you just point it to the exported game so you don't need to make all the code open to everyone.

    FROM alpine:latest

    # Variables
    ENV GODOT_VERSION "3.2.3"
    ENV GODOT_GAME_NAME ""
    ENV HTTPS_GIT_REPO ""

    # Updates and installs
    RUN apk update
    RUN apk add --no-cache bash
    RUN apk add --no-cache wget
    RUN apk add --no-cache git

    # Allow this to run Godot
    RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.31-r0/glibc-2.31-r0.apk
    RUN apk add --allow-untrusted glibc-2.31-r0.apk

    # Download Godot and export template, version is set from variables
    RUN wget https://downloads.tuxfamily.org/godotengine/${GODOT_VERSION}/Godot_v${GODOT_VERSION}-stable_linux_headless.64.zip \
        && wget https://downloads.tuxfamily.org/godotengine/${GODOT_VERSION}/Godot_v${GODOT_VERSION}-stable_export_templates.tpz \
        && mkdir ~/.cache \
        && mkdir -p ~/.config/godot \
        && mkdir -p ~/.local/share/godot/templates/${GODOT_VERSION}.stable \
        && unzip Godot_v${GODOT_VERSION}-stable_linux_headless.64.zip \
        && mv Godot_v${GODOT_VERSION}-stable_linux_headless.64 /usr/local/bin/godot \
        && unzip Godot_v${GODOT_VERSION}-stable_export_templates.tpz \
        && mv templates/* ~/.local/share/godot/templates/${GODOT_VERSION}.stable \
        && rm -f Godot_v${GODOT_VERSION}-stable_export_templates.tpz Godot_v${GODOT_VERSION}-stable_linux_headless.64.zip

    # Make directory to run the app from
    RUN mkdir /godotapp
    WORKDIR /godotapp
    RUN git clone ${HTTPS_GIT_REPO} .
    RUN godot --path . --export-pack "Linux/X11" ${GODOT_GAME_NAME}.pck
    CMD godot --main-pack ${GODOT_GAME_NAME}.pck



## Docker-Compose.yaml

You will notice that the docker-compose.yaml file is not much different that it was before, minus the fact I took out the volume you need to add your game to. This is because I am using github as the storage instead. It provides the single source of truth I was looking for, and makes updating things way easier for the end user.
  
    version: '3'

    services:
    godot:
        build: .
        ports:
        - "12345:12345"
        - "12345:12345/udp"
        tty: true
        container_name: godot-server

# Conclusion

It works, and I am happy with it for once. I also know the team at GodotNuts is happy with it to. I had a lot fo good feedback for it, and I plan to make it better one day. Just don't have the time right now. Seems to be a running trend.