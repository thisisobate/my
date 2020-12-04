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
- "/images/blog/windows-10.png"
featuredImage: "/images/blog/windows-10.png.png"
---

> **In case you are using a mac, please refer to [Ivana's](https://medium.com/@ivanahuckova/how-to-contribute-to-grafana-as-junior-dev-c01fe3064502) post on setting up grafana on a mac.**

Setting up and running Grafana on a windows PC is quite tricky.

With the advent of [WSL](https://docs.microsoft.com/en-us/windows/wsl/about) on windows, users now have the capability of running linux on a windows environment.

**TL/DR**     

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

**Adding datasources**
- navigate to the `devenv` directory and kick-start data sources by running `/setup.sh` script
- reload the site and find list of different data sources
- Download and install Docker
- Run `make devenv sources=influxdb,loki` to add datasources and start up their databases. 

> **NOTE: To get the latest, up to date information on Grafana's setup process, do checkout [README](https://github.com/grafana/grafana/blob/master/contribute/developer-guide.md) on github.**

# Dependencies
Dependencies in Grafana, on a windows PC, comes in two different dimensions:
1. Linux runtime environment (WSL).
2. Development (Dev) dependencies.

## Linux Runtime environment

It is important to note that for Grafana to run locally on a windows machine, it has to depend on a linux environment. Fortunately enough, windows now have a feature that allow us to run linux on windows 10 PC.
The Windows Subsystem for Linux (WSL) is a new Windows 10 feature that enables you to run native Linux command-line tools directly on Windows, alongside your traditional Windows desktop and modern store apps. 

In order for grafana and docker to run effectively on your machine, you need to install **WSL**.
Thankfully, Microsoft has a well-documented installation guide which you can follow through.
Please check it out [here](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

## Dev dependency

Before you start installing dev dependencies, please note that you should have WSL and a linux distro already set up on your machine. It is advisable to use the linux terminal for installing development dpendencies.  

Because windows 10 have both windows and linux environment running concurrenty, one might make the mistake of installing a dependency in one environment, and try accessing it from another different environment. This is a major issue most windows users face wjile setting up their working environments and so, it is advisable to always use the Linux environment (WSL) for any kind of application/software development work.   

There are a few necessary dependencies which you need to install inorder to get grafana up and running on your machine:
- Go: I would recommend you use a go version manager to install the latest go binary. [GVM](https://github.com/moovweb/gvm) provides an interface to manage Go versions. Check out their installation guide [here](https://github.com/moovweb/gvm).
- [Node.js (Long Term Support)](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04)
- Yarn (`npm install -g yarn`).

# Downloading Grafana
To download grafana on your windows machine, open your terminal and navigate to your desired directory. As a best practice, I normally clone all my software projects into one central directory- Would be writing more on this topic soon. Run `git clone https://github.com/grafana/grafana.git`. This command downloads Grafana to a new `grafana` directory in your current directory. Navigate to the `grafana` directory by running `cd grafana`. Open the grafana directory in your favorite code editor - if you're using vscode, run `code .` to open grafana in vscode.

**Please Note: Do not use `go get` to download Grafana. Recent versions of Go have added behavior which isn't compatible with the way the Grafana repository is structured.**

# Run Grafana
Grafana comprises of two major parts: the frontend and the backend. To completely run the grafana aaplication on your machine, it's important you start up both the frontend and the backend. 

## Backend
Navigate to your terminal and start the backend web server by running `make run`. Please note that you can as well start the frontend before the backend.

## Frontend
Before we can build the frontend assets, we need to install the dependencies. Open another different terminal, navigate to the grafana directory, and run:

`yarn install --pure-lockfile`     

After the command has finished, we can start building our source code:

`yarn start`

Grafana is going to be served on http://localhost:3000. You will see the login page. Default credentials are:
```
username: admin
password: admin

```

![Grafana login page](../../static/images/blog/grafana-login.png)

When you log in for the first time you will be asked to change your password. You can decide to skip that page if you want.

## Tests
Run tests using `yarn test`
```
yarn test

```
# Adding datasources
Luckily for all developers and contributors, you can easily add datasources and run corresponding databases. You can find the documentation here, but I will still walk you thought it and add some additional information.
As a first step, you need to change your directory to devenv.    
``` 
cd devenv

```
In devenv, you need to run bash command `./setup.sh`. This means, that running `./setup.sh` will execute this script (any executable bash script can be run by preceding it with ./) and it will setup a couple of datasources and dashboards in your Grafana. Datasources will be named **gdev-<type>** and dashboard folder will be named **gdev dashboards**. After running this command in terminal, don't forget to restart grafana server (backend). You should then be able to see the changes.

```
./setup.sh

```
If you want to run databases for those datasources, you are going to need Docker. You can install Docker Hub (containing Docker Engine, Docker CLI client, Docker Compose, Docker Machine, and Kitematic) via its [official site](https://docs.docker.com/docker-for-windows/install/). Installation is pretty straight forward. As soon as you are up and running with Docker, you can follow with next steps.

Firstly, get back to grafana directory from devenv.
```
cd ..

```
Secondly, you are going to run make command.
```
make devenv sources=influxdb,loki

```
This command will create a docker compose file with specified databases configured and ready to run. Just run the command, restart Grafana server, and you should see the added datasources.

You can as well find the list of all available databases in **grafana/devenv/docker/blocks**.

Thanks for reading! 🤗
