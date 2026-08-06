---
layout: post
title: "Migrating a WordPress Blog from WordPress.com to WordPress.org"
categories:
  - Programming
  - Web
image: assets/images/wordpress.png
description: "Migrating content, stats, followers, and URL redirects from WordPress.com to a self-hosted WordPress.org installation"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2015/04/03/migrating-a-wordpress-blog-from-wordpress-com-to-wordpress-org/](https://blog.henrypoon.com/blog/2015/04/03/migrating-a-wordpress-blog-from-wordpress-com-to-wordpress-org/)

Since a few months ago, I migrated my blog from the previous free installation of WordPress that [WordPress.com](http://www.wordpress.com) offered, to the self-hosted installation offered by [WordPress.org](http://www.wordpress.org) (note that one is .org and the other is .com). Here are just a few of the key differences stated briefly:

- Self-hosted installations allow greater control over what plugins the blog uses, what domain name to use, monetization, among other things
- The cost is the added time required to tweak and do the setup and customization

After I chose to switch to the self-hosted installation, I faced the problem of having to migrate all of my content, site stats, and followers. I also had to set up proper URL redirection to the new website. Most of the guides I read did answer how to migrate content and set up URL redirects, but it was not so clear as to how to migrate my site stats and followers.

## Content Migration

For migrating content, the WordPress.com blog allows exporting blog content into a file to be imported into the new WordPress installation. Steps 1 to 3 in [this guide](http://www.wpbeginner.com/wp-tutorials/how-to-properly-move-your-blog-from-wordpress-com-to-wordpress-org/) illustrate the process.

## Migrating Site Stats and Followers

Migrating site stats and followers requires installing the [Jetpack](https://wordpress.org/plugins/jetpack/) addon and linking it to the WordPress.com account (so that the self-hosted WP and the existing WP blog are connected). afterward, a support thread has to be made on WordPress.com to ask WP staff to do the rest of the migration (there seems to be no other way). I found the information on how to do this at [this StackExchange post](http://wordpress.stackexchange.com/questions/161633/migrating-stats-from-wordpress-com-blog-to-self-hosted-wordpress-org-blog). The post I made for my own site migration is [here](https://en.forums.wordpress.com/topic/transferring-stats-and-subscribers-from-wordpresscom-to-self-hosted-wordpress?replies=8).

## Setting Up URL Redirection

This part costs money unfortunately. I paid ~$17 CAD for this so that my old URL would be redirected to the new one. If redirection is not required, then there is no need to buy anything. The setup is pretty straightforward. After buying the redirect, it is just a matter of setting the destination WordPress site to go to. Reference link here: [https://en.support.wordpress.com/site-redirect/](https://en.support.wordpress.com/site-redirect/)
