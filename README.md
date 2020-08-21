
Opensource Job Portal
=====================

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/105a3bf03bec4cfbac70d7c30e574bea)](https://www.codacy.com/manual/ashwin/opensource-job-portal?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=MicroPyramid/opensource-job-portal&amp;utm_campaign=Badge_Grade)

[![Build Status](https://travis-ci.org/MicroPyramid/opensource-job-portal.svg?branch=master)](https://travis-ci.org/MicroPyramid/opensource-job-portal)

[![Coverage Status](https://coveralls.io/repos/github/MicroPyramid/opensource-job-portal/badge.svg?branch=master)](https://coveralls.io/github/MicroPyramid/opensource-job-portal?branch=master)

https://opensource-job-portal.readthedocs.io/en/latest/ for latest documentation
Job Portal with Unlimited free job posting, Social Api's authentication.

===============================================

Recruiter
----------

*Enhancements*:

    * Can post jobs to social networking sites like facebook, twitter, linkedin.
    * Walk-in's
    * Copy An Existing Job Post, Deactivate.
    * Added Google Maps
    * Mobile Number Authentication
    * Post their job post message into social networking sites.

Portal
-------

*Enhancements*:

    * Job Alerts
    * New Mobile Design
    * Normal Search and Advanced Search
    * Email Notifications


Quick Installation Guide
========================
For both deployment and deployment we use `docker <https://www.docker.com>`_ so you need to have docker
running on the host. opensource-job-Portal is a django app so it will help if you have
some knowledge of running a django site.

For local environmet
====================

     - cd opensourcr-job-portal/deployment
     - docker-compose up --build -d

For production environment
==========================

    - Log into your server (ssh) or using any CI/CD tooling in place such as travis/Jenkins etc

    - cd opensourcr-job-portal/deployment
    - docker-compose up --build -d

     To scale worker services to a DESIRED number of instances for example
      to run 3 instances of events worker (handling all notifications) and 4 transaction workers (handling all machinery processing such as rebuiding elasticsearch index, updatin meta data etc) you would do the following:

    - docker-compose up --detach --scale worker-events=3
    - docker-compose up --detach --scale worker-transactions=4

Congratulations, lets do some house chores and jump into coding
===============================================================

To run database migrations :

    $ docker exec -it uwsgi_container_ID bash

    $ python manage.py migrate

To collect static files:

    $ docker exec -it uwsgi_container_ID bash
    $ python manage.py collectstatic

To load initial data i.e states, countries, skills, categories etc:

    $ docker exec -it uwsgi_container_ID bash
    $ python manage.py rebuild_index

To create superuser account:


    $ docker exec -it uwsgi_container_ID bash
    $ python manage.py createsuperuser

Alt:

    Instructions for using MAKEFILE and more automation coming soon..


In case your code changes take some seconds to reflect, you can force reload of uwsgi container with:


    $ docker exec -it uwsgi_container_ID bash
    $ uwsgi --reload /tmp/django.pid

- Celery flower can be accessed at http://0.0.0.0:5555 or https://yourhostname/flower,
same for pgadmin4
- Rabbitmq is also accessible at http://0.0.0.0:15672 or https://yourhostname/rabbitmq
- graphql service running under hansura package is also accesible at port 8089

- Please check the docker compose file for some login credentials to the
 above service such as rabbitmq and or pgadmin4

Happy Coding!


Backups
-------

We have automated backups running as a cronjob docker service for your db.
So hang on and relax.

Credits
-------

Opensource-django-project is actively being developed and maintained by MicroPyramid with an extended open source community contributions to the code base `micropyramid.com <https://micropyramid.com>`_.


Thank you
---------

Thank you to the individual contributors who have helped to build *Open-source-portal*:

* Ashwin Kumar
* Alison Mukoma: mukomalison@gmail.com | <sonlinux>
* Manas Ranjan Pati
* Chaitanya
* Loading more ...
=======
Opensource Job Portal developed in python django with Unlimited free job posting, Social Api's authentication.

# Recruiter
* Can post jobs to social networking sites like facebook, twitter, linkedin.
* Walk-in's
* Copy An Existing Job Post, Deactivate.
* Add localtion in Google Maps
* Post their job to social networking sites.

# Portal
* Job Alerts
* New Mobile Design
* Normal Search and Advanced Search
* Email Notifications


# Setup
These are setup instruction for ubuntu 18.04

```
sudo apt install git postgresql python3 python3-dev python3-venv libpq-dev build-essential ruby ruby-dev gem redis-server memcached redis-tools -y
curl -sL https://deb.nodesource.com/setup_12.x -o nodesource_setup.sh
sudo bash nodesource_setup.sh
sudo apt-get install node-less
```

Install and configure sass and less compilers
```
sudo gem install sass
```

you need to create symbolic link if you get error locating lessc
here my lessc file locatin is /usr/bin/lessc
you can find yours with this command ```which lessc```
```
sudo ln -s /usr/bin/lessc /usr/local/bin/lessc
```


Then setup env using the following command
```
python3 -m venv peeljobs-env
```

Activate env with the following command
```
activate peeljobs-env/bin/activate
```

Install requirements
```
pip install -r requirements.txt
```

For env variables, refer to env.md for environment variables and keep those in the .env file in the current folder as your project is in.

Then open http://localhost:8000 in your borwser and it should work properly.

Run docker
```
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:2.4
```

create index
```
python manage.py update_index
```
