# medium-cloud-build-kaniko

Run the below commands inside the `kaniko-demo` folder!

## Docker

```sh
# Build "kaniko-demo" app on your local machine
docker build -t kaniko-demo .

# Run local container in detached mode
docker run -d -p 3000:3000 kaniko-demo

```

## Cloud Build

```sh
# Set GCP project
gcloud config set project <project>

# Build "kaniko-demo" app on Cloud Build
gcloud builds submit --region <region> --config <path_to_cloudbuild_yaml> <path_to_build_context>
gcloud builds submit --region europe-west2 --config cloudbuild.yaml .

```