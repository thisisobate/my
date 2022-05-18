---
authors:
  - name: "Uchechukwu Obasi"
date: 2021-03-03
linktitle: install grafana on windows.
type:
  - post
  - posts
title: "How to set up a Grafana development environment on a Windows PC using WSL"
weight: 1
categories:
  - Grafana
  - windows
  - technical
  - installation
images:
  - "https://user-images.githubusercontent.com/29557702/168991938-f4b4b5f5-b324-4b08-b12a-6588f45ede55.png"
featuredImage: "https://user-images.githubusercontent.com/29557702/168991938-f4b4b5f5-b324-4b08-b12a-6588f45ede55.png"
---

> **Note: This is a guest blog originally published on the Grafana website.**

The Grafana development environment runs on Linux, so most engineers have Linux installed on their machines.

The Macintosh OS already supports Linux out of the box, so it’s straightforward to start up dev environments on a Mac. (If you are using a Mac, please refer to this guide on [how to contribute to Grafana as a junior dev](https://ivanahuckova.medium.com/how-to-contribute-to-grafana-as-junior-dev-c01fe3064502), which explains how to set up the Grafana dev environment on a Mac.)

On the contrary, the Windows OS does not have a Linux environment, so developing software on a Windows machine can be difficult. But with the advent of [WSL](https://docs.microsoft.com/en-us/windows/wsl/about) on Windows, you can now run a GNU/Linux environment directly on Windows. This blog post will explain how to get started.

> **Note:** To get the latest, up-to-date information on Grafana’s setup process, check out the [README](https://github.com/grafana/grafana/blob/main/contribute/developer-guide.md) on GitHub.

## Install dependencies
There are two types of dependencies for running a Grafana development environment on a Windows PC:

1. Linux runtime environment (WSL)
2. Development (Dev) dependencies
Read through and make sure all dependencies are installed on your system.

### Linux runtime environment
> **Note:** Before you start installing the Linux runtime environment, please note that your machine must run on a UEFI BIOS, which supports virtualization out of the box.

To set up the Grafana developer environment with ease, you need a Linux environment to run locally on a Windows machine. Fortunately, the Windows Subsystem for Linux (WSL) allows you to run a native Linux command-line tool directly on Windows, alongside your traditional Windows desktop and modern store apps.

In order for Grafana and Docker to run effectively on your machine, you need to install WSL along with a Linux distribution. For the Linux distribution, I did some test runs using Ubuntu v18.04, and it worked well for me.

For installation instructions, refer to the [Microsoft WSL Installation Guide](https://docs.microsoft.com/en-us/windows/wsl/install).

### Dev dependencies
> **Note:** It’s recommended that you use the Linux terminal for installing development dependencies.

Because Windows 10 has both Windows and Linux environments running concurrently, you might make the mistake of installing a dependency in one environment and trying to access it from a different environment. This is a major issue most Windows users face while setting up their working environments. You should always use the Linux environment (WSL) for any kind of application or software development work.

There are a few necessary dependencies that you need to install in order to get Grafana up and running on your machine:

- [Go (v1.15)](https://sal.as/post/install-golan-on-wsl/).

- Node.js LTS(v14.15.5): I would recommend you use a Node version manager to install Node.js. [NVM](https://github.com/nvm-sh/nvm) provides an interface to manage Node versions. Check out [the installation guide](https://www.mrdemonwolf.me/blog/how-to-setup-nodejs-nvm-on-wsl/).

- Yarn (npm install -g yarn).

- [Docker](https://docs.docker.com/desktop/windows/wsl/): Docker needs to be installed on Windows but activated for each WSL distro. It requires WSL2 for it to run successfully. If you’re not on WSL2 yet, we recommend you update your WSL to WSL2.

## Download Grafana
> **Warning:** Do not use `go get` to download Grafana. Recent versions of Go have added behavior that isn’t compatible with the way the Grafana repository is structured.

To download Grafana on your Windows machine:

1. Open your terminal and navigate to your desired directory. As a best practice, I normally clone all my software projects into one central directory.

2. Run `git clone https://github.com/grafana/grafana.git.` This command downloads Grafana to a new grafana directory in your current directory.

3. Navigate to the grafana directory by running cd grafana.

4. Open the Grafana directory in your favorite code editor. If you’re using Visual Studio Code, run `code .` to open Grafana in VSCode.

## Run Grafana
Grafana is composed of two major parts: the frontend and the backend. To completely run the Grafana application on your machine, you must start up both the frontend and the backend.

### Backend
Navigate to your terminal and start the backend web server by running `make run`. Remember that you can start the frontend before the backend.

### Frontend
Before you can build the frontend assets, you need to install the frontend dependencies. Open a different terminal, navigate to the Grafana directory, and run:

`yarn install --pure-lockfile`

After the command has finished, you can start building our source code:

`yarn start`

Grafana is going to be served on http://localhost:3000. You will see the login page. Default credentials are:

```
username: admin
password: admin
```
When you log in for the first time, you will be asked to change your password. You can decide to skip that page.

## Test Grafana
You can take a look at the [Grafana documentation](https://github.com/grafana/grafana/blob/main/contribute/developer-guide.md#test-grafana) to learn more about this.

## Add data sources
Luckily for all developers and contributors, you can easily add data sources and run corresponding databases. You can find the documentation [here](https://github.com/grafana/grafana/tree/main/devenv), but I will walk you through it and add some additional information.

1. As a first step, you need to change your directory to devenv. 

    `cd devenv`

2. In devenv, you need to run bash command `./setup.sh`. This means that running `./setup.sh` will execute this script (any executable bash script can be run by preceding it with ./) and it will set up a couple of data sources and dashboards in your Grafana. Data sources will be named **gdev-** and the dashboard folder will be named **gdev dashboards**.
3. After running this command in the terminal, restart Grafana server (backend). You should then be able to see the changes.

    `./setup.sh`

4. Get back to the Grafana directory from devenv.

    `cd ..`

5. Run make command.

    `make devenv sources=influxdb,loki`

This command creates a Docker compose file with specified databases configured and ready to run!

You can also find the list of all available databases in **grafana/devenv/docker/blocks**.


