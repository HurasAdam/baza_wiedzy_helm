# Server

This repo is a list of services, which I use. Steps to set them up:

- Forgejo = initialize git
- Sealed secrets

While running this app for the first time, make sure to fill gitea.admin data in values-x.yaml. Without them, no admin will be created. Once admin is created, replace values with empty strings.



This application uses sealed secrets. Apply it first. After starting sealed secrets service, encrypt secrets from `forgejo-pre` folder using:

```sh
kubeseal \
  --controller-namespace ${namespace} \
  --controller-name sealed-secrets \
  --format yaml \
  < secret-file.yaml \
  > output.yaml
```

Save outputs into proper files and apply helm again

## Important

Make of copy of sealed secrets key just in case

```sh
kubectl -n ${namespace} get secret | grep sealed-secrets
kubectl -n ${namespace} get secret ${secretNameFromPreviousStep} -o yaml > key.yaml
```


Gitea-runners are added externally outside argo due to some issues with deployments



