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
- career
images:
- "/images/blog/grafana_labs.png"
featuredImage: "/images/blog/grafana_labs.png"
---

**PS: In case you are using a mac, please refer to [Ivana's](https://medium.com/@ivanahuckova/how-to-contribute-to-grafana-as-junior-dev-c01fe3064502) post on setting up grafana on a mac.**

Setting up and running grafana on a windows PC is quite tricky.

with the advent of wsl on windows, users now have the capability of running linux on a windows environment.

**Set up process**
- setup go locally using gvm- ensure you have the latest go binary installed
- open up terminal 
- clone grafana into a directory-please know the environment you cloned into: linux? or windows
- open up terminal and run `make run` to start the backend
- open another terminal and run `make run-frontend` to start the frontend
- visit `localhost:3000` on browser to login-username and password: admin
- navigate to the `devenv` directory and kick-start data sources by running `/setup.sh` script
- reload the site and find list of different data sources     

Thanks for reading! 🤗
