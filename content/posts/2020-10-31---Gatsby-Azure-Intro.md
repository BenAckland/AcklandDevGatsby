---
template: post
title: Creating a GatsbyJs Blog On Azure Static Web Apps - Introduction
slug: azure-static-web-apps-gatsbyjs-intro
socialImage: /media/image-0.jpg
draft: false
date: 2020-10-31T13:43:00.000Z
description: Walking through the foundational pieces of this blog. Azure Static Web Apps, GatsbyJs and Lumen.
category: Tests
tags:
  - Azure Static Web Apps
  - GatsbyJS 
---
Posts in this series:

* [Introduction](/posts/azure-static-web-apps-gatsbyjs-intro)
* Azure Static Web App - Apex Domains with Cloudflare
* Azure Static Web App - Application Insights
* Netlify and Forrestry headless CMS

[Source code](https://github.com/benackland/acklanddevgatsby)

## Intro
Recently I created a blog to act as a public notebook for the things I am learning. This is that blog.

It's built using GatsbyJS, hosted for free in Azure Static Web Apps, uses a GitHub CI/CD pipeline and NetlifyCMS as a headless CMS. It's also monitored in Application Insights which was a right pain to set up. Finally it uses its apex domain which, out of the box, is not a thing for Azure Static Apps.

This blog series will cover how I set up all of those things.

**First up, the foundations.**

## Theme
Once I'd picked GatsbyJs as my framework I needed a theme (I'm no designer). I chose <a href="https://github.com/alxshelepenok/gatsby-starter-lumen" target="_blank">Lumen</a> by <a href="https://github.com/alxshelepenok" target="_blank">Alexander Shelepenok</a>. Hats off to Alex, Lumen is awesome. Everything you'll need to stand up a new blog project it there and it includes NetlifyCMS built in. 

Clone the starter repo, push it to a new repo of your own on GitHub and start customising.

## Azure Static Web Apps
I'm hosting this blog using the Azure Static Web App service, sure, to learn another Azure technology but mainly because it's completely free while in preview. Read more about it <a href="https://azure.microsoft.com/en-gb/services/app-service/static/" target="_blank">here</a>. If you don't have one already you can sign up for a free Azure <a href="https://azure.microsoft.com/en-gb/free/" target="_blank">account</a>.

The actual process was so simple there's no point me running through it here. Follow the creation wizard, allow it to authenticate with your GitHub account, point it at the GitHub repo containing your code, configure a domain and you're done. The service will even issue and refresh a free LetsEncrypt SSL cert for you.

There's also a handy VS Code extension for Static Apps <a href="https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestaticwebapps" target="_blank">here</a>. 

## GitHub CI/CD
The fact that Microsoft now own GitHub means more and more integration between Azure and GitHub. The upshot here is that creating a new static web app will create a CI/CD pipeline for you automatically using GitHub actions. That pipeline will build and deploy your site on each commit no setup required. Even fancier, creation of a PR the pipeline will deploy an entirely new staging environment for the change. 

This post covers the foundations of this blog and these pieces will get you up and running. The following posts will cover some of the trickier aspects I have encountered while fine tuning it. 
