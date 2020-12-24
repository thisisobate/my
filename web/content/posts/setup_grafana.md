---
authors:
- name: "Uchechukwu Obasi"
date: 2020-11-22
linktitle: Set up the Grafana dev environment on a Windows 10 PC
type:
- post
- posts
title: Set up the Grafana dev environment on a Windows 10 PC.
weight: 1
categories:
- observability
- setup
images:
- "/images/blog/windows-10.png"
featuredImage: "/images/blog/windows-10.png"
---

> **If you are using a Mac, please refer to [How to contribute to Grafana as a junior dev](https://medium.com/@ivanahuckova/how-to-contribute-to-grafana-as-junior-dev-c01fe3064502), which explains how to set up the Grafana dev environment on a Mac.**

Grafana is an open source platform for monitoring and observability. It allows you to query, visualize, alert on and understand your metrics no matter where they are stored.

The Grafana development environment runs on Linux and thus, it is expected that developers must have Linux installed on their machine. The Macintosh OS already supports Linux out of the box and so, it’s pretty much straight-forward to start up development environments on a Mac.

On the contrary, Windows OS does not have a Linux environment and thus, developing software on a windows machine was a huge hassle.

With the advent of [WSL](https://docs.microsoft.com/en-us/windows/wsl/about) on Windows, it is possible to run a GNU/Linux environment directly on Windows.

> **Note:** To get the latest, up-to-date information on Grafana's setup process, do checkout [README](https://github.com/grafana/grafana/blob/master/contribute/developer-guide.md) on github.

## Dependencies
Dependencies in Grafana, on a windows PC, comes in two different dimensions:
- Linux runtime environment (WSL).
- Development (Dev) dependencies.

### Linux runtime environment

The Grafana developer environment requires a Linux environment to run locally on a windows machine. Fortunately, the Windows Subsystem for Linux (WSL) allows you to run native Linux command-line tools directly on Windows, alongside your traditional Windows desktop and modern store apps.

In order for Grafana and docker to run effectively on your machine, you need to install **WSL**.
For installation instructions, refer to the [Microsoft WSL Installation Guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

### Dev dependency

Before you start installing dev dependencies, please note that you should have WSL and a Linux distro already set up on your machine. It is advisable to use the Linux terminal for installing development dependencies. 

Because Windows 10 has both Windows and Linux environments running concurrently, one might make the mistake of installing a dependency in one environment, and try accessing it from another different environment. This is a major issue most windows users face while setting up their working environments and so, it is advisable to always use the Linux environment (WSL) for any kind of application/software development work.  

There are a few necessary dependencies which you need to install in order to get grafana up and running on your machine:
- Go: I would recommend you use a Go version manager to install the latest Go binary. [GVM](https://github.com/moovweb/gvm) provides an interface to manage Go versions. Check out their installation guide [here](https://github.com/moovweb/gvm).
- [Node.js (Long Term Support)](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04)
- Yarn (`npm install -g yarn`).

## Download Grafana
To download grafana on your windows machine, open your terminal and navigate to your desired directory. As a best practice, I normally clone all my software projects into one central directory- would write more on this topic soon. Run `git clone https://github.com/grafana/grafana.git`. This command downloads Grafana to a new `grafana` directory in your current directory. Navigate to the `grafana` directory by running `cd grafana`. Open the grafana directory in your favorite code editor - if you're using vscode, run `code .` to open grafana in vscode.

>**Warning:** Do not use `go get` to download Grafana. Recent versions of Go have added behavior which isn't compatible with the way the Grafana repository is structured.

## Run Grafana
Grafana comprises two major parts: the frontend and the backend. To completely run the grafana application on your machine, it's important you start up both the frontend and the backend.

### Backend
Navigate to your terminal and start the backend web server by running `make run`. Remember that you can as well start the frontend before the backend.

### Frontend
Before we can build the frontend assets, we need to install the dependencies. Open another different terminal, navigate to the grafana directory, and run:

`yarn install --pure-lockfile`    

After the command has finished, we can start building our source code:

`yarn start`

Grafana is going to be served on http://localhost:3000. You will see the login page. Default credentials are:

**username: admin**    
**password: admin**

![Grafana login page](/images/blog/grafana-login.png)

When you log in for the first time, you will be asked to change your password. You can decide to skip that page.

## Test Grafana

The test suite consists of three types of tests: _Frontend tests_, _backend tests_, and _end-to-end tests_.

### Run frontend tests

We use [jest](https://jestjs.io/) for our frontend tests. Run them using Yarn:

```
yarn test
```

### Run backend tests

If you're developing for the backend, run the tests with the standard Go tool:

```
go test -v ./pkg/...
```

Running the backend tests on Windows currently needs some tweaking, so use the build.go script:

```
go run build.go test
```

### Run end-to-end tests

The end to end tests in Grafana use [Cypress](https://www.cypress.io/) to run automated scripts in a headless Chromium browser. Read more about our [e2e framework](/contribute/style-guides/e2e.md).

To run the tests:

```
yarn e2e
```

By default, the end-to-end tests starts a Grafana instance listening on `localhost:3001`. To use a specific URL, set the `BASE_URL` environment variable:

```
BASE_URL=http://localhost:3333 yarn e2e
```

To follow the tests in the browser while they're running, use the `yarn e2e:debug`.

If you want to pick a test first, use the `yarn e2e:dev`, to pick a test and follow the test in the browser while it runs.

## Adding datasources
Luckily for all developers and contributors, you can easily add datasources and run corresponding databases. You can find the documentation [here](https://github.com/grafana/grafana/tree/master/devenv), but I will still walk you through it and add some additional information.
As a first step, you need to change your directory to devenv.   
```
cd devenv
```
In devenv, you need to run bash command `./setup.sh`. This means that running `./setup.sh` will execute this script (any executable bash script can be run by preceding it with ./) and it will set up a couple of datasources and dashboards in your Grafana. Datasources will be named **gdev-<type>** and dashboard folder will be named **gdev dashboards**. After running this command in the terminal, don't forget to restart grafana server (backend). You should then be able to see the changes.

```
./setup.sh
```
If you want to run databases for those datasources, you are going to need Docker. You can install Docker Hub (containing Docker Engine, Docker CLI client, Docker Compose, Docker Machine, and Kitematic) via its [official site](https://docs.docker.com/docker-for-windows/install/). Installation is pretty straightforward. As soon as you are up and running with Docker, you can follow with next steps.

First, get back to the Grafana directory from devenv.
```
cd ..
```
Second, you are going to run make command.
```
make devenv sources=influxdb,loki
```
This command will create a docker compose file with specified databases configured and ready to run. Just run the command, restart Grafana server, and see the added datasources.

You can as well find the list of all available databases in **grafana/devenv/docker/blocks**.

Thanks for reading! 🤗
