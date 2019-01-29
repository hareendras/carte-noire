---
layout:     post
title:      Getting back on track - Episode II
date:       2018-05-18 07:01:18
summary:    Getting my hands dirty on jekyll
categories: progress
thumbnail: jekyll
tags:
 - thumbnils 
---

This is Part II of getting back on development track posts where I try to record my progress and interesting tools and problems and solutions I come across.

So in last post we had some progress on getting jekyll site up and running using docker. We were able to generate new Jekyll site using Jekyll new command. Let’s work on getting this site up and running.


Aww snap!!

![ImgList](/assets/img/2018-05-18/docker_compose_err.png){:class="img-responsive"}

This error was resolved after restarting docker from the task bar icon. And now as usual to the next error. 😉

![ImgList](/assets/img/2018-05-18/docker_compose_err2.png){:class="img-responsive"}

Got rid of this error. The reason was my gem directory was in the same folder as my site root. Explicitly excluding in _config.yml resolved the error. [more info](http://talk.jekyllrb.com/t/invalid-date-error-using-bundle-exec-jekyll-serve-vendor-not-working/538/3)
```yml
exclude:
# - Gemfile
# - Gemfile.lock
# - node_modules
# - vendor/bundle/
# - vendor/cache/
# - vendor/gems/
# - vendor/ruby/
# - vendor
 - gems

```

Try again...

![ImgList](/assets/img/2018-05-18/docker_err2.png){:class="img-responsive"}

Looks like it is a good time to try some alternative way of getting this up and running locally. So instead of trying with docker-compose, let’s try to run the container using docker run.
```terminal
docker run -it -v C:/Users/hareendras/myblog:/srv/jekyll -v C:/Users/hareendras/myblog:/usr/local/bundle jekyll/jekyll jekyll new .
```
Above command creates a new Jekyll site in current directory of the container.  -v means <sourcepath in my c drive>:<destination path in container> source path is the local path in my laptop and mount path is in container. To use volumes like this, the sharing should be enabled in docker settings.

![ImgList](/assets/img/2018-05-18/docker_share.png){:class="img-responsive"}

Create site.

![ImgList](/assets/img/2018-05-18/create.png){:class="img-responsive"}

run it

```terminal
$>  docker run -it -p 4000:4000 -v C:/Users/hareendras/myblog:/srv/jekyll -v C:/Users/hareendras/myblog:/usr/local/bundle jekyll/jekyll jekyll serve
```
At last success!!

![ImgList](/assets/img/2018-05-18/success.png){:class="img-responsive"}

Default theme for jekyll looks nice. But let's search for theme which is even better.

It turned out that there is absolutely no need to run Jekyll locally to set the site up and running in github pages! :D :D :D Its just a matter of forking an existing Jekyll theme and name the repository as <username>.github.io format. Then the page will be published in https://<username>.github.io. However since we setup the local site it is easier for us to edit the posts locally, test them and publish them after testing locally. Since this is a user page, ie urls has the format of https://<username>/github.io we should do the moifications on master branch and the same should be pushed to github repo named <username>github.io and git hub will automatically build and publish the site for us. Awesome

Now that we have our static site successfully published at gh pagaes, let’s try to understand jekyll mechanism of adding posts. So the next goal is to add the content to the page published.
Even though running the site on local is not mandatory, since we already have the infrastructure setup in local, let’s just first clone the repository and run it locally anyway.
So cd into the C:/Users/hareendras/myblog, clear the content and clone the repository. Now let’s try to bring it up locally.

```terminal
$> docker run -it -p 4000:4000 -v C:/Users/hareendras/myblog:/srv/jekyll -v C:/Users/hareendras/myblog:/usr/local/bundle jekyll/jekyll jekyll serve
```
![ImgList](/assets/img/2018-05-18/docker_run.png){:class="img-responsive"}
