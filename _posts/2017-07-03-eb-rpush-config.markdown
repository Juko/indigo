---
title: "Rpush configuration for Elastic Beanstalk"
layout: post
date: 2017-07-03 18:30
image: https://camo.githubusercontent.com/aef53ce272b99a3e0fe72f6e09d132f2206f2545/68747470733a2f2f7261772e6769746875622e636f6d2f72707573682f72707573682f6d61737465722f6c6f676f2e706e67
headerImage: true
tag:
- elastic-beanstalk
- rpush
- aws
category: blog
author: pauljukic
description: A simple configuration for rpush on AWS
---

A sane default for configuring your Rails app on Elastic Beanstalk (EB) for use with [Rpush](https://github.com/rpush/rpush)

This follows the same configuration that the official AWS `.ebextensions` follow.

If you're unsure or want more information about ebextensions [click here](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/ebextensions.html).

## Configuration

This script assumes that your Rails Rpush configuration file is at `config/initializers/rpush.rb` but change it to suit your needs.

Simply create a rpush file in your ebextensions folder:
> `.ebextensions/rpush.config`

{% gist Juko/cc3d54345722fdf1b92494eb0a5b2228 %}

## What it does
1. Creates a file that runs upon post appdeploy. This file is called `03_rpush.sh` so if you need to ensure files run in a certain order, just change the number at the front.
2. Set's up all the needed variables from the environment
3. Stops the currently running Rpush process if there is one running (based off the `.pid`)
4. Starts the new Rpush process with the correct location for `.pid` and configuration