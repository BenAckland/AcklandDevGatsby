---
template: post
title: Creating a GatsbyJs Blog On Azure Static Web Apps - Introduction
slug: azure-static-web-apps-gatsbyjs-intro
socialImage: /media/image-0.jpg
draft: false
date: 2020-09-26T13:43:00.000Z
description: Introduction to the blogging series.
category: Tests
tags:
  - Azure Static Web Apps
  - GatsbyJS
---
Posts in this series:

* [Introduction](/posts/azure-static-web-apps-gatsbyjs-intro)
* Azure Static Web App - Hosting 
* Azure Static Web App - Apex Domains with Cloudflare
* Azure Static Web App - Application Insights
* Github CI/CD Pipeline
* Netlify and Forrestry headless CMS

[Source code](https://github.com/benackland/acklanddevgatsby)

## Intro
I created a blog to act as a public notebook that might be useful to other people. This is that blog.

It's built in Gatsby JS, hosted for free in Azure Static Web Apps, uses a GitHub CI/CD pipeline and uses Contentful as a headless CMS. It's also monitored in Application Insights which was a right pain to set up. Finally it uses its apex domain, which, out of the box is not a thing for Azure Static Apps.

This blog series will cover how I set up all of those things.