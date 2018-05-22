---
layout:     post
title:      Getting back on development track
date:       2018-05-17 07:39:18
summary:    Hello world!! this is my very first blog post
categories: progress
thumbnail: jekyll
tags:
 - thumbnils
 - carte noire
---

## Some background on progress so far

I’ve played around with nodejs express and react technologies and have some idea on the JavaScript scene. I’ve followed some courses in udemy on React and React native technologies and tried building some stuff as side projects.

![work-in-progress](/assets/img/2018-05-17/courses.png){:class="img-responsive"}

Some side projects I work on these days are TimeApp and AthalBot. TimeApp is and React Native application where I try to replicate [this](http://tiii.me/)  (as much as I can). AthalBot is a facebookBot that returns gags from 9gag and it is integrated with dialog flow for nlp processing. 

## Trying to publish AthalBot

I’ve already finished working on AthalBot and want to publish. When I try to publish this bot however, Facebook requires a privacy policy URL.

![privacy-error](/assets/img/2018-05-17/privacy_err.png){:class="img-responsive"}

So, to publish a url first I must have a site rite? I need some sort of published url before publishing the bot. Meh.. 😐 This might be the best time for me to publish some static site and host the url there. 
After some research I came across github pages for publishing and site generator called [Jekyll](https://jekyllrb.com/). Github pages supports Jekyll too. Cool. 

## Getting my head around Jekyll 

Home: [https://jekyllrb.com/](https://jekyllrb.com/) Docs: [https://jekyllrb.com/docs/home/](https://jekyllrb.com/docs/home/) 

Mmm looks like Jekyll needs some other stuff to run and windows 10 is not the perfect platform to run Jekyll. So instead of trying to install Jekyll on my windows 10 laptop, I’m going to try Jekyll docker container and get the thing done. (I already have docker installed and have some idea about the images containers and stuff). Let’s get to work!! 

Side note: Currently I’m writing this blog on a word document and the immediate goal I have is to publish this using Jekyll and gh pages. Afterwards I will add the privacy policy URL to the same blog as a page and try to send my facebook bot for approval.

Wohoo!! Doceker container for Jekyll [https://hub.docker.com/r/jekyll/jekyll/](https://hub.docker.com/r/jekyll/jekyll/)

Let’s try to grab that image and give it a shot.

```terminal
$>docker pull jekyll/Jekyll
```

Downloading

![downloading](/assets/img/2018-05-17/downloading_image.png){:class="img-responsive"}

Done!!

![Done](/assets/img/2018-05-17/dowload_done.png){:class="img-responsive"}

Let’s check the downloaded image

```terminal
$>docker images
```

![ImgList](/assets/img/2018-05-17/img_list.png){:class="img-responsive"}

Cool!

Let’s see how we can use this image. Docs: [https://github.com/envygeeks/jekyll-docker/blob/master/README.md](https://github.com/envygeeks/jekyll-docker/blob/master/README.md)  
To use the downloaded image as mentioned in above readme, we need to use docker-compose. So let’s create a docker-compose.yml with below content

```yml
version: "3"
services:
  site:
    command: jekyll serve
    image: jekyll/jekyll:latest
    volumes:
      - C:/Users/hareendras/myblog:/srv/jekyll
      - C:/Users/hareendras/myblog:/usr/local/bundle
    ports:
      - 4000:4000
      - 35729:35729
      - 3000:3000
      -   80:4000
```

And after trying again with command

```terminal
$> docker-compose run site jekyll new . --force
```

![ImgList](/assets/img/2018-05-17/docker_compose1.png){:class="img-responsive"}
...
![ImgList](/assets/img/2018-05-17/docker_compose2.png){:class="img-responsive"}

Awesome!! Files got generated.

Aww snap!!

![ImgList](/assets/img/2018-05-17/docker_compose_err.png){:class="img-responsive"}

This error was resolved after restarting docker from the task bar icon. And now as usual to the next error. 😉

![ImgList](/assets/img/2018-05-17/docker_compose_err2.png){:class="img-responsive"}
