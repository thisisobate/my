---
authors:
- name: "Uchechukwu Obasi"
date: 2020-11-22
linktitle: Getting Started With Grafana On A Windows Machine.
type:
- post 
- posts
title: Getting Started With Grafana On A Windows Machine.
weight: 1
categories:
- observability
- setup
images:
- "/images/blog/grafana_labs.png"
featuredImage: "/images/blog/grafana_labs.png"
---

**PS: In case you are using a mac, please refer to [Ivana's](https://medium.com/@ivanahuckova/how-to-contribute-to-grafana-as-junior-dev-c01fe3064502) post on setting up grafana on a mac.**

Setting up and running grafana on a windows PC is quite tricky.

with the advent of wsl on windows, users now have the capability of running linux on a windows environment.

**Set up process**     
**Dependencies**
- Download and set up WSL on your windows machine
- setup go locally using gvm- ensure you have the latest go binary installed     
**Download**
- open up terminal 
- clone grafana into a directory-please know the environment you cloned into: linux? or windows     
**Run Grafana**
- open up terminal and run `make run` to start the backend
- open another terminal and run `make run-frontend` to start the frontend
- visit `localhost:3000` on browser to login-username and password: admin     
**Run datasoources**
- navigate to the `devenv` directory and kick-start data sources by running `/setup.sh` script
- reload the site and find list of different data sources
- Download and install Docker
- Run `make devenv sources=influxdb,loki` to add datasources and start up their databases. 

# Dependencies
Dependencies at Grafana on a windows PC works comes in two different dimensions:
1. Development (Dev) dependencies
2. Linux runtime environment

Linux Runtime environment: It is important to note that for Grafana to run locally on a windows machine, it has to depend on a linux environment. Fortunately enough, windows now have a feature that allow us to run linux on windows 10 PC.
The Windows Subsystem for Linux (WSL) is a new Windows 10 feature that enables you to run native Linux command-line tools directly on Windows, alongside your traditional Windows desktop and modern store apps. 

**download WSL**
In order for grafana and docker to run effectively on your machine, you need to install WSL 2.
Thankfully, Microsoft has a well-documented installation guide which you can follow through.
Please check it out [here](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

Dev dependency: Before you start installing dev dependencies, please note that you should have WSL and a linux distro already set up on your machine. It is advisable to use the linux terminal for installing development dpendencies.  

Because windows 10 have both windows and linux environment running concurrenty, one might make the mistake of installing a dependency in one environment, and try accessing it from another different environment. This is a major issue most windows users face wjile setting up their working environments and so, it is advisable to always use the Linux environment (WSL) for any kind of application/software development work.   

There are a few necessary dependencies which you need to install inorder to get grafana up and running on your machine:
- Go: I would recommend you use a go version manager to install the latest go binary. [GVM](https://github.com/moovweb/gvm) provides an interface to manage Go versions. Check out their installation guide [here](https://github.com/moovweb/gvm).
- [Node.js (Long Term Support)](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04)
- Yarn (`npm install -g yarn`).

# Downloading Grafana

Thanks for reading! 🤗
