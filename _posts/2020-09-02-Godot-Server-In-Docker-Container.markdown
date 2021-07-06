---
title: "Godot Server In Docker Container"
date:  2020-09-02 10:00:00 -0500
categories: [Godot, Guide]
tags: [Godot, Docker, CentOS, Godot Server, Guide, Nakama]
author: chuck lindblom
sharing: true
show_author_profile: true
cover: /assets/images/godot_logo.png
---

# Godot Has A Server???

I learned about Godot server the other day, and I became very interested in it as a replacement for trying to learn Nakama Server. For anyone who is curious you can download the Godot Server <a href="https://godotengine.org/download/server">on their website here.</a> After trying to learn the integration between Nakama and Godot, I realized I had a giant mountain in front of me and I was going to have to learn things like LUA. This was not something I was looking to do right away for simple multiplayer games.

<!--more-->

# But Wait, I Have Docker!

I have been dipping my toes into Docker recently trying to get a better idea of how containers work and how I can apply it to my job if I wanted to. Looking at how the Godot Server runs on Linux, I had the idea to create my own container for it. The idea was simple, if I could make a container for Godot server that could run my game, I could easily create multiple servers at once to handle extra load.

Below I have posted the two files I use when creating this docker container. Please note you will also need the file **centos-7-x86_64-docker.tar.xz** in the same directory as everything else for this to work.

# Dockerfile

    FROM scratch
    ADD centos-7-x86_64-docker.tar.xz /

    LABEL \
        org.label-schema.schema-version="1.0" \
        org.label-schema.name="CentOS Base Image" \
        org.label-schema.vendor="CentOS" \
        org.label-schema.license="GPLv2" \
        org.label-schema.build-date="20200504" \
        org.opencontainers.image.title="CentOS Base Image" \
        org.opencontainers.image.vendor="CentOS" \
        org.opencontainers.image.licenses="GPL-2.0-only" \
        org.opencontainers.image.created="2020-05-04 00:00:00+01:00"

    CMD ["/bin/bash"]

    RUN yum install wget git unzip ca-certificates -y

    ENV GODOT_VERSION "3.2.2"

    RUN wget https://downloads.tuxfamily.org/godotengine/${GODOT_VERSION}/Godot_v${GODOT_VERSION}-stable_linux_server.64.zip \
        && wget https://downloads.tuxfamily.org/godotengine/${GODOT_VERSION}/Godot_v${GODOT_VERSION}-stable_export_templates.tpz \
        && mkdir ~/.cache \
        && mkdir -p ~/.config/godot \
        && mkdir -p ~/.local/share/godot/templates/${GODOT_VERSION}.stable \
        && unzip Godot_v${GODOT_VERSION}-stable_linux_server.64.zip \
        && mv Godot_v${GODOT_VERSION}-stable_linux_server.64 /usr/local/bin/godot \
        && unzip Godot_v${GODOT_VERSION}-stable_export_templates.tpz \
        && mv templates/* ~/.local/share/godot/templates/${GODOT_VERSION}.stable \
        && rm -f Godot_v${GODOT_VERSION}-stable_export_templates.tpz Godot_v${GODOT_VERSION}-stable_linux_server.64.zip

# Docker-Compose.yaml

    version: '3'

    services:
    centos:
    build: .
    ports:
    - "12345:12345"
    - "12345:12345/udp"
    tty: true
    volumes:
    - ./context:/context
    container_name: godot-server

# End Result

I was able to get this to work, and with the context folder I can easily add files on the local server that are added into the container. This allows me to run the Godot Server and test changes with ease and not have to continue to recreate the server.
