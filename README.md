Vaadin on Heroku
================

The goal of this project is to demonstrate how to build a [Vaadin](https://vaadin.com/home) application and deploy it on [Heroku](http://www.heroku.com).

It uses [Embed for Vaadin](https://vaadin.com/directory#addon/embed-for-vaadin) to configure and start an embedded [tomcat](http://tomcat.apache.org/)
configured to start Vaadin and store session in memcached.

What is heroku specific in there?
---------------------------------

* Procfile: Heroku is using [foreman](https://github.com/ddollar/foreman) to launch processes and the Procfile is the file that define the processes.
* maven-dependency-plugin configured in the pom of the server module to copy the dependencies.
* Launcher class that will configure the tomcat server based on env variables and launch it.
* [memcached-session-manager](http://code.google.com/p/memcached-session-manager/): Heroku doesn't allow sticky session and can restart an application at any given time,
  and it's using [an ephemeral file system](https://devcenter.heroku.com/articles/dyno-isolation#ephemeral_filesystem) .
  For those reasons, session should be stored in another place that is common to all servers and doesn't restart with them.
  Memcached is perfect for that.

Where tho go from here?
-----------------------

If you never used heroku before, install the [toolbelt](https://toolbelt.heroku.com/) and [create an account](http://heroku.com/signup).

Just clone this repository and type

    heroku create --stack cedar

Heroku will create your app and give you it's url. You can change it later.

You'll also need to add the memcache add-on.

    heroku addons:add memcache

Then push the application like this :

    git push heroku master

And the application is up and running.


As an example, this application is deployed on heroku and accessible at http://hello-vaadin-heroku.herokuapp.com/
