# Kubernetes Django Starter

Example Kubernetes manifests to create a Django project.

This is created to work with our Django starter project at https://github.com/wildfish/wildfish-django-starter/ so projects based on that should work out of the box, otherwise there are a few environment variables and secrets to configure as described below. It's presumed that the Django container runs on port 8000.

## Quickstart

Presuming you have `kubectl` configured and pointing at a Kubernetes cluster you can create the objects using:

    kubectl create -f k8s/

## Secrets

Some sensitive values are stored in secrets and passed to the containers as environment variables.

Secrets are defined in the `secrets.yaml` manifest and encoded using `base64`.

To encode a secret:

    echo "mysecretvalue" | base64 -w 0
    
To decode:

    echo "bXlzZWNyZXR2YWx1ZQo=" | base64 --decode

| Secret | Environment Variable | Passed To | Default Value | 
| ------ | -------------------- | --------- | ------------- |
| credentials/postgres-user | POSTGRES_USER | django, postgres | django-example |
| credentials/postgres-password | POSTGRES_PASSWORD |  django, postgres | password |
| credentials/gcs-key | GCS_KEY | django | TODO |
