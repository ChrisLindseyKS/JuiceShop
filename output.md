# OWASP Juice Shop Demo Set up

his project uses Docker Scout to perform software composition analysis (SCA) on the containerized Juice Shop application.

To experience Docker Scout, you will need a  [Docker account](https://app.docker.com/signup).  A free personal account can be used to run Docker Scout for one image.  

Once you have an account, [create an organization](https://hub.docker.com/orgs) to use to store your Docker images.

## Run the Application Locally as a Docker Container from a Newly Built Image


To run the containerized juice shop web application locally, you will need to install [Docker](https://www.docker.com/products/docker-desktop/).  If you install Docker Desktop, then Docker Scout will be automatically installed.  If you are using Docker Engine without Docker Desktop, follow the [instructions here](https://docs.docker.com/scout/install/) to install the Docker Scout binary.

Once you have installed Docker, perform the following steps in a terminal window:

1. Clone this repository

`git clone https://github.com/julieabyrne-devsecops/juice-shop.git`

2. Navigate to the repository root directory

`cd juice-shop`

3. Build the Docker image and push it to your DockerHub orgaanization (note: you must be logged into Docker to perform this operation)

`docker build --push -t <ORG_NAME>/juiceshop:v1 .`

4. To run the web application locally, run the command: 

`docker run --rm -p 127.0.0.1:3000:3000 <ORG_NAME>/juiceshop:v1`

The homepage will then be available at <http://localhost:3000>

![Juice Shop Screenshot](screenshots/juice_shop.png)

## Use Docker Scout for SCA

You can run Docker Scout on the local image by running the command:

`docker scout quickview`

That will provide a summary of the vulnerabilities found and prompt you with additional commands to run as next steps.  A full list of packages and vulnerabilities will also be created for the image you pushed to your organization.  These details can be viewed from the [Docker Scout web interface](https://scout.docker.com/).

![Docker Scout Results](screenshots/scout_results.png)

## Locking Down the GitHub Repo
By default, GitHub allows code changes to be pushed directly to the default branch.  This is an insecure configuration, however, as it allows developers to forego code review of changes before they are integrated with production code.  To prevent the push to the default branch (master), use the repository settings to create a new ruleset to require that code changes can only be merged from a PR for a feature branch to the default branch.

![Rules](screenshots/ruleset.png)

![PR Rule](screenshots/rule.png)



