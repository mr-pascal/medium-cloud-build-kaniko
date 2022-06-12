# medium-cloud-build-kaniko


## Docker

```sh
# Build
docker build -t nestjs-kaniko .

# Run
docker run -d -p 3000:3000 nestjs-kaniko

```


## Cloud Build

```sh
# Set GCP project
gcloud config set project <project>
gcloud config set project pascal-sandbox-1112

# Trigger Cloud Build
gcloud builds submit --region <region> --config <path_to_cloudbuild_yaml> <entry_point>
gcloud builds submit --region europe-west2 --config cloudbuild.yaml .

```

--compressed-caching
