---
layout: post
title: Running Jekyll locally
comments: true
---

So, I had to see that to run the Jekyll locally, it is necessary to add a `Gemfile`

So, add this to your `Gemfile` in the root folder of your repository.

> source 'https://rubygems.org'
> gem 'github-pages', group: :jekyll_plugins

So, you can run this command to generate the necessary stuff:

> bundle install

And followed by this, to run your website locally:

> bundle exec jekyll serve

And, it will promt the URL to access it locally.

That is it!

