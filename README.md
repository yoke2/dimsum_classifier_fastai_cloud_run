# Dim Sum Image Classification App with [fast.ai](https://www.fast.ai) models on [Google Cloud Run](https://cloud.google.com/run/)

This repo contains a version of the web app for classifying [dim sum](https://en.wikipedia.org/wiki/Dim_sum) that can be deployed to Google Cloud Run. It supports 5 dim sum types currently.

----------
## Deploy with Google Cloud Run

### Pre-requisites
- Google Cloud Account
- Enable Cloud Run and Cloud Build API

### Deploy
To run the webapp on Google Cloud Run, launch Cloud Shell from your Dashboard.

- export PROJECT_ID={your project id here}
- Run `gcloud config set project $PROJECT_ID`
- Run `git clone https://github.com/yoke2/dimsum_classifier_fastai_cloud_run.git`
- Change directory: `cd dimsum_classifier_fastai_cloud_run`
- Build container image with [Google Cloud Build](https://cloud.google.com/cloud-build/) by running `gcloud builds submit --tag gcr.io/$PROJECT_ID/dimsumapp`
    - If prompted that Cloud Build API not enabled on the project, enter 'y' to enable and retry
- Deploy container built: `gcloud run deploy --image gcr.io/$PROJECT_ID/dimsumapp --platform managed --allow-unauthenticated --memory 512M`
    - You will be prompted for the service name: press Enter to accept the default name
    - You will be prompted for region: select the region us-central1
- You will receive an URL to access the app. This can be seen on the Cloud Run page for `dimsumapp` in the Dashboard as well

----------
## Docker Installation

You can test your changes locally by installing Docker and using the following command:

```
docker build -t dimsum-fastai-v3-cr . && docker run --rm -it -p 5000:5000 dimsum-fastai-v3-cr
```

----------
## Local Installation

* Install dependencies
```
$ pip install -r requirements.txt
```

## Run app
```
$ python app/server.py serve
```

----------
## Reference

* [Guide for production deployment to Render](https://course.fast.ai/deployment_render.html)

* [Render's fast.ai forum thread](https://forums.fast.ai/t/deployment-platform-render/33953)

* [Github for deployment of the same app on Render](https://github.com/yoke2/dimsum_classifier_fastai)
