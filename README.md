# scicat-helm

Integrated Helm charts for the SciCat project, including the following services:

- backend
- frontend
- elasticSearch
- mongoDB

## Prerequisites

- Kubernetes

## Installing the Chart

SciCat supports both OpenID Connect (OIDC) for authentication and pre-stored local accounts for authentication.

To install SciCat chart with OpenID Connect (OIDC) for authentication:

_(Change localhost to your ingress host accordingly, defaults to localhost)_

```
helm install scicat-app scicat-app --namespace scicat-dev --create-namespace -f scicat-app/values.yaml \
--set backend.configmap.OIDC_ISSUER=<OIDC ISSUER> \
--set backend.configmap.OIDC_AUTHORIZATION_URL=<OIDC_AUTHORIZATION_URL> \
--set backend.configmap.OIDC_CLIENT_ID=<OIDC_CLIENT_ID> \
--set backend.configmap.OIDC_CLIENT_SECRET=<OIDC_CLIENT_SECRET> \
--set backend.configmap.OIDC_CALLBACK_URL="http://localhost/api/v3/auth/oidc/callback" \
--set backend.configmap.OIDC_SUCCESS_URL="http://localhost/auth-callback/"
```

Alternatively, you can choose to run it without OpenID authentication:

_(Pre-stored local accounts can be found in `backend/envfiles/functionalAccounts.json`)_

```
helm install scicat-app scicat-app --namespace scicat-dev --create-namespace -f scicat-app/values.yaml
```

Both commands will install the Helm chart named `scicat-app` with the release name `scicat-app` in the `scicat-dev` namespace. The application will be accessible via the hostname localhost and the URI `http://localhost`.

## Uninstalling the Chart

To uninstall/delete the scicat-app deployment:

```
helm uninstall scicat-app -n scicat-dev
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists part of the configurable parameters for SciCat helm chart and their default values.
More completed lists can be found in [SciCat Backend repository](https://github.com/SciCatProject/scicat-backend-next)

| Parameter                                  | Description                                                                   | Default                                  |
| ------------------------------------------ | ----------------------------------------------------------------------------- | ---------------------------------------- |
| `frontend.ingress.host`                    | URL for frontend                                                              | `localhost`                              |
| `backend.ingress.host`                     | URL for backend                                                               | `localhost`                              |
| `backend.configmap.OIDC_ISSUER`            | URL of the OIDC issuer, providing authentication tokens and configuration     | ``                                       |
| `backend.configmap.OIDC_AUTHORIZATION_URL` | URL for the authorization endpoint where users are redirected to authenticate | ``                                       |
| `backend.configmap.OIDC_CLIENT_ID`         | Client ID issued by the OIDC provider                                         | ``                                       |
| `backend.configmap.OIDC_CLIENT_SECRET`     | Client secret issued by the OIDC provider                                     | ``                                       |
| `backend.configmap.OIDC_CALLBACK_URL`      | URL where the OIDC provider redirects users after authentication.             | ``                                       |
| `backend.configmap.OIDC_SUCCESS_URL`       | URL where users are redirected after successful authentication                | ``                                       |
| `backend.configmap.OIDC_SCOPE`             | Specifies the scope of access requested                                       | `openid profile email`                   |
| `backend.configmap.ELASTICSEARCH_ENABLED`  | Enables or disables the use of Elasticsearch in backend ("yes" or "no")       | `yes`                                    |
| `backend.configmap.ES_HOST`                | Specifies the connection string to your Elasticsearch service.                | `http://scicat-app-elastic-search:9200`  |
| `backend.configmap.MONGODB_URI`            | Specifies the connection string to your MongoDB database.                     | `mongodb://scicat-app-mongodb/scicat-db` |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

Alternatively, parameters can be configured from the `values.yaml` YAML file in the scicat-app directory.
