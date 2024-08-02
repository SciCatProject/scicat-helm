# To run scicat-app Locally with Minikube

## Prerequisites:

Minikube: Ensure Minikube is installed and running. Follow the official [Minikube installation guide](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Fx86-64%2Fstable%2Fbinary+download) if needed.

Helm: Ensure Helm is installed. Follow the official [Helm installation guide](https://helm.sh/docs/intro/install/) if needed.

# Steps to Run scicat-app

## Step 1: Start Minikube

```
minikube start
```

## Step2: Set up Helm Dependencies

Navigate to the `scicat-app` directory and build the Helm dependencies.

```
cd scicat-app
helm dependency build
```

## Step3: Install scicat-app

Navigate to the `scicat-helm` root directory and install the Helm chart using the specified values file.
[Helm Install Doc ](https://helm.sh/docs/helm/helm_install/)

```
helm install scicat-app scicat-app --namespace scicat-dev --create-namespace -f scicat-app/values.yaml > scicat-app/app.yaml
```

## Verify Installation:

Check the status of the release.

```
helm status scicat-app --namespace scicat-dev
```

## Expose pod to localhost

After successfully starting the tunnel, you can access the application at `http://localhost`

```
minikube tunnel
```

NOTE: ingress needs to be enabled.

# Customization and additional useful commands.

## Customize Ingress Host

Alternatively, you can customize the ingress host and modify your `/etc/hosts` file accordingly. By default, the ingress host is set to `localhost`.
ingress config can be found in the `scicat-app/values.yaml`

## Upgrade Release

```
helm upgrade scicat-app scicat-app --namespace scicat-dev -f scicat-app/values.yaml
```

## Uninstall Release

```
helm uninstall scicat-app --namespace scicat-dev
```

# Notes:

Modify the `values.yaml` file with your desired settings.
The charts directory and Chart.lock file are ignored in version control as specified in the .gitignore file.
By following these steps, you should be able to run scicat-app locally with Minikube.
