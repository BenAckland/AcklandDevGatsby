---
template: post
title: Azure Static Web App - Apex Domains with Cloudflare
slug: azure-static-web-apps-apex-domains-cloudflare
socialImage: /media/image-0.jpg
draft: true
date: 2020-11-14T19:07:00.000Z
description: How to use CloudFlare to enable the use of root domains with Azure
  Static Web Apps.
category: Tests
tags:
  - Azure Static Web Apps
  - GatsbyJS
  - Cloudflare
---
Posts in this series:

* [Introduction](/posts/2020-10-31---Gatsby-Azure-Intro.md)
* Azure Static Web App - Apex Domains with Cloudflare
* Azure Static Web App - Application Insights
* Netlify and Forrestry headless CMS

[Source code](https://github.com/benackland/acklanddevgatsby)

## Intro

This blog is hosted in Azure using the Static Web App service. As the service iscurrently in preview it is missing a few things that you might expect. One of those is the inability to use root domains for for your site. Sub domains like www.ackland.dev will work just fine but ackland.dev will not. To get around that we need to use Cloudflare which will allow us to set up a redirect from the root domain to the www. sub domain.

## Cloudflare to the rescue

Cloudflare offer loads of security and performance features for your website. You can add things like DDOS protection, a CDN and SSL for free! We need to use their DNS and page rules services to solve our root domain problem. Sign up for a free account <a href="https://www.cloudflare.com/" target="_blank">here</a>.

### Configure Cloudflare as your DNS server

First up you need to configure Cloudflare to be the DNS server for the domain that you want to use to serve your blog. If you haven't already, sign up for an account and register your domain. Cloudflare will then give you the nameservers you need to configure with your domain registrar.

### Create your CNAME records

Once Cloudflare is set up as your DNS server your need to configure some CNAME records.

### Add your redirect page rule