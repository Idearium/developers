# Google Cloud Platform

We use as much of the Google Cloud Platform as we can. There are bunch of guides in here for using particular GCP services.

## Projects

Our organisation has a few projects. This guide helps you work with projects.

### Creating a new project

When creating a new project, using the following rules:

- Make sure a billing account is setup prior to creating a new project.
- When choosing a project id, using something short and memorable.

#### gcloud configuration

Once you've created a project, setup `gcloud` with:

- `gcloud config set project {project-id}` (you can see all projects with `gcloud projects list`).

### Shared service account

You'll need to add a shared service account so that you can push to gcr. To add one to your new project follow these steps:

- Visit IAM in the new project.
- Click add and enter `{service-account-email}`.
- Choose the Service Account User role and then save the new user.

## Google Kubernetes engine

We use GKE for all of Kubernetes workloads.

## Creating a new Kubernetes cluster

To create a new Kubernetes cluster:

- Set the `gcloud` project with `gcloud config set project teamly-cloud`.
- Create a cluster with `gcloud beta container clusters create {cluster-name} --cluster-version=1.8.8-gke.0 --zone=us-east1-b --enable-autorepair --machine-type=n1-standard-1`.

## Google container registry

To use the Google container registry from the command line:

- Execute `gcloud auth configure-docker`.
- Tag a local docker image with `docker tag {image-name} gcr.io/{project-id}/{image-name}`.
- Then push to gcr with `docker push gcr.io/{project-id}/{image-name}`.

To use the Google container registry from Codefresh:

- Make sure you've added a shared service account.
- Visit the Storage browser and show the info panel for the desired bucket.
- In the _Add members_ field enter the service account email.
- Choose the following roles:
    - Storage Legacy Bucket Reader
    - Storage Legacy Bucket Writer

### Pushing via Codefresh

You can also puth to the Google container registry from Codefresh. To do so:

- In the deploy steps in your `codefresh.yml`, use the following:
    - registry: gcr
    - image_name: {project-id}/{image-name}