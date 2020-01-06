# demo.bokeh.org

Hosted Bokeh App Demos

***NOTE***: *The [demo.bokeh.org](https://demo.bokeh.org) site has moved to a simpler deployment based on Docker and Elastic AWS Beanstalk. To see the old Nginx/Salt based deployment code, look at the ``nginx_salt_deploy`` branch.*

## Using Locally

### Setup

Clone this repository:
```
git clone https://github.com/bokeh/demo.bokeh.org.git
```
and [install Docker](https://docs.docker.com/install/) on your platform

### Building 

In the top level of this repository, execute the command
```
docker build --tag demo.bokeh.org .
```

### Running

Execute the command to start the Docker container:
```
docker run --rm -p 5006:5006 -it demo.bokeh.org
```
Now navigate to ``http://localhost:5006`` to interact with the demo site. 

## Deploying to AWS

The published [demo.bokeh.org](https://demo.bokeh.org) site is deployed using [Elastic Beanstalk with Docker Containers](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker.html). 

Random notes for future reference:

* Load balancer protocol needs to be set to TCP to allow websocket connections
* Similar rules needed to security group config

## Deploying on Google App Engine (GAE)

At the time of writing (January 2020), Google App Engine only supports [websockets on the Flex environment](https://cloud.google.com/blog/products/application-development/introducing-websockets-support-for-app-engine-flexible-environment). To deploy Bokeh on GAE, you can follow [the instructions in the documentation](https://cloud.google.com/appengine/docs/flexible/custom-runtimes/how-to).

Once you have setup the project and `gcloud` SDK, you need to rename the Dockerfiles

```
mv Dockerfile Dockerfile-default && mv Dockerfile-GAE Dockerfile
```

after which deploying to GAE can be done with

```
gcloud app deploy
```

Note this is just a bare-bones deployment, with no SSL or any security measures. Using a load-balancer is recommended as described in the GAE documentation.
