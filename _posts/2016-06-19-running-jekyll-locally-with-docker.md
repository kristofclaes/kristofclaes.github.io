---
title: Running Jekyll locally with Docker
description: Setting up a Jekyll website locally using Docker.
---

This website is built with static site generator Jekyll and hosted on GitHub pages. There are a number of reasons why this combination is awesome:

* I can write everything in Markdown
* The workflow has source control baked in
* The website is automatically updated by pushing to master

If you want to give Jekyll a go and you're running Linux or OS X, you have to make sure you have the correct version of Ruby and some gems installed. Running it on Windows isn't officially supported, but it can be done using Chocolatey and it also requires Ruby and some gems. Regardless of your operating system, there is an easier way to get Jekyll running on your machine. This is where Docker comes into play.

When you run Jekyll from inside a Docker container, you won't have to bother with installing a specific version of Ruby or with different versions of gems you already had installed potentially clashing. You could of course use the Ruby Version Manager, but working with Docker really is a breeze.

The rest of this post assumes you have Docker and Docker Compose installed and have some basic knowledge of working with it. Docker has some great getting started guides for [Linux](https://docs.docker.com/linux/), [Mac](https://docs.docker.com/mac/) and [Windows](https://docs.docker.com/windows/).

The easiest way to get started is probably to download a theme for Jekyll. This website uses a slightly modified version of the Hyde theme. It's [hosted on GitHub](https://github.com/poole/hyde), so you can download or clone it from there.

The friendly people of Jekyll have already made a Docker image available on [Docker Hub](https://hub.docker.com/r/jekyll/jekyll/). Let's take advantage of that! Suppose you have downloaded or cloned the Hyde repository into `~/jekyll-site/`. To use the Jekyll image without having to pass in the required options every time to create a container, we can make use of Docker Compose. Create a file called `docker-compose.yml` in `~/jekyll-site` with these contents:

{% highlight yml %}
jekyll:
    image: jekyll/jekyll:pages
    command: jekyll serve --watch --incremental
    ports:
        - 4000:4000
    volumes:
        - .:/srv/jekyll
{% endhighlight %}

* With `image: jekyll/jekyll:pages` you indicate you want to use Jekyll's Jekyll image tagged with "pages". This is a specific image suited for GitHub pages.
* The part after `command:` is the command to execute in the container. The `jekyll serve` command starts Jekyll's builtin development web server. The options `--watch` and `--incremental` instruct Jekyll to automatically regenerate the HTML when a file is changed.
* `4000:4000` forwards port 4000 of the container to your local port 4000.
* Finally, on the last line you map the current directory (`~/jekyll-site/`) to `/srv/jekyll/`. That's where the images is configured to go looking for a Jekyll site.

That's all! You can start your Jekyll site by browsing to your site's directory using a terminal and doing `docker-compose up`. You will see something like this:

{% highlight plaintext %}
jekyll_1  | Configuration file: /srv/jekyll/_config.yml
jekyll_1  |             Source: /srv/jekyll
jekyll_1  |        Destination: /srv/jekyll/_site
jekyll_1  |  Incremental build: enabled
jekyll_1  |       Generating...
jekyll_1  |                     done in 0.343 seconds.
jekyll_1  |  Auto-regeneration: enabled for '/srv/jekyll'
jekyll_1  | Configuration file: /srv/jekyll/_config.yml
jekyll_1  |     Server address: http://0.0.0.0:4000//
jekyll_1  |   Server running... press ctrl-c to stop.
{% endhighlight %}

If you go to http://0.0.0.0:4000 (or the IP of your VM if you're running Docker on OS X or Windows) in a browser you'll see your Jekyll site. Easy, right?
