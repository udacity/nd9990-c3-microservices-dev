# Udagram Image Filtering Microservice

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

# Solution Overview
`docker-compose` isn't necessarily required for deploying to Kubernetes. However, it is useful because it helps you conceptualize the relationship between the containers and allows you to run all the containers locally.

A container using nginx named `reverseproxy` is used. It helps add another layer between the frontend and API so that the frontend only uses a single endpoint and doesn't realize it's deployed separately. This is one approach and not necessarily the only way to deploy the services.

## Setup Instructions

### Environment Variables
Set environment variables for config values such as the database connection. The required environment values can be found in the `docker-compose.yaml` file.

### Setup Docker Environment
You'll need to install docker https://docs.docker.com/install/. Open a new terminal within the project directory and run:

1. Build the images: `docker-compose -f docker-compose-build.yaml build --parallel`
2. Push the images: `docker-compose -f docker-compose-build.yaml push`
3. Run the container: `docker-compose up`

## Notes
* The frontend container starts earlier than the backend containers. Loading the frontend before they are running will prompt an error. Confirm that all the desired containers are running before testing out the frontend and API.
* When migrating this application to use containers, we may run into an issue with the `bcrypt` package. This is because the `node_modules` were installed on an operating system different than that of the one in the Docker image. The solution is to set `node_modules` in our `.dockerignore` file so that `node_modules` are not copied over from our local machine into the container.