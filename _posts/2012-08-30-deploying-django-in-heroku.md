---
layout: post
title: Deploying Django in Heroku
author: Rag Sagar
authorlink: 
summary: Most of the django developers know how hard it is to deploy django. Most people worry about not being able to concentrate more on coding because of the time they need to invest on managing servers. Making the hard part easier heroku makes the django deployment a piece of cake. Heroku is a Platform as a Service provider which runs on top of aws platform. Here I am going to create a sample django app and going to deploy it in the heroku cloud.
---

Most of the django developers know how hard it is to deploy django. Most people
worry about not being able to concentrate more on coding because of the time
they need to invest on managing servers. Making the hard part easier heroku
makes the django deployment a piece of cake. Heroku is a Platform as a Service
provider which runs on top of aws platform. Here I am going to create a sample
django app and going to deploy it in the heroku cloud.

 1) First of all, go to heroku.com and create an account in heroku.

You can signup for a free account. What free account offers is enough to run a
small django app.

 2) Install the [heroku toolbelt](http://toolbelt.herokuapp.com)

 3) Start a django app using the following command.

    >$django-admin startproject sample
    >$cd sample

 4) Run the following command and give the heroku account credentials.

    >$heroku login

 5) Then add remotes for heroku using the following command.

    >$heroku create

 6) Initialize a git repo and do the first commit.

    >$git init
    >$git add .
    >$git commit -m "First commit"

 7) Now push the django app to heroku

    >$git push heroku master

 8) Go run the following command to open the django app we deployed in
heroku in browser

    >$heroku open

Now you will be able to see the "it works!" page.

When you make real world django apps, you might want to maintain a
requirements.txt file with all the python dependency modules. Heroku
looks for this file and pip installs the listed packages in it. The best way to
do is to create a virtual environment and pip install all the needed packages
into it.

To create a virtual env, from the project directory run this command.

    $easy_install virtualenv
    $virtualenv venv --no-site-packages

This will create a venv directory inside project directory. Better add this
directory to your git ignore file.

    $echo "venv" >> .gitignore

Now activate the virtualenv.

    >$source venv/bin/activate

Now you can pip install the needed packages. Packages will be installed inside
the virtualenv only. You can use pip to keep track of the requirements 

    >$pip freeze > requirements.txt
    >$git add requirements.txt
    >git commit -m "Added requirements"
    >$git push heroku master

Heroku will read that file and install all needed python packages.
Only the code pushed into heroku master, will be deployed. If you are working
on another branch and you want to deploy it into heroku without merging it with
the master you can do the following.

    >$git push heroku yourbranch:master

That's it for now. You can find lot more stuffs in heroku documentation. :)

