 #Build a fully production ready machine learning app with React, Django, and PostgreSQL on Docker
 
This is a simple machine learning application with Django REST framework, which predicts the species of a sample flower based on measurements of its features i.e. the sepal and petal dimensions – length and width.


Tech stack:
 - EKS
 - -Docker
 - -Django
 - -React-App
 -  Python
 -  Nodejs
 -  Postgres

Backend – Django, Django REST framework, PostgresSQL
Frontend – React 

Overview: 

The Django service would use the Dockerfile to build the container, then map the static folder within this container to the corresponding volume in the volumes (django_static_volume). The same volume is mapped to one of the nginx static directories served by nginx as defined in the nginx.conf file. 

This ensures that static files from our django service are served on the nginx service. Also, the Django service would be started with a python package called gunicorn. This is because gunicorn is actually a production server for python applications with multithreading support. 

We expose the port 8000 as this would be used by gunicorn to serve our Django application. Further, the environment variables defined in the .env file in the backend service are available in the django service container. This ensures that our django_app is running with debug set as false, is allowing the right hosts, and can connect to the postgres service with the right credentials.  The Django service depends on the db service. 

The Postgres service is called 'db',  is the simplest as it just needs the environment variables to create our database and serve it to the django service. 

The react service sends the API_SERVER variable to the production build version of our react application, maps the build folder to the corresponding folder on the nginx service and serves the react application with the create-react-app suggested 'serve' server on port 3000. The react service is dependent on the django service. 

The nginx service serves both our django and react services. 

To Dockerize the app:

cd into the souce code directory where the docker compose file is and run the command 'docker-compose up' or 'docker-compose up --build'.

source: https://datagraphi.com/blog/post/2020/8/30/docker-guide-build-a-fully-production-ready-machine-learning-app-with-react-django-and-postgresql-on-docker
