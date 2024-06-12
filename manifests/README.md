# Manifests

They run on Kustomize. There are 3 types of deployments.

- Open Data Hub (`./odh`)
- Red Hat OpenShift AI (`./rhoai`)
  - RHOAI Managed (`./rhoai/addon`)
  - RHOAI Self Managed (`./rhoai/onprem`)

The `common` & `./rhoai/shared` are two locations where the bases are found. Base folder has the resources or overrides (for RHOAI) to deploy the dashboard. 

## Installation

Use the `kustomize` tool to process the manifest for the `oc apply` command.

```
# Parse the base manifest to deploy ODH Dashboard WITHOUT the required configs for groups
cd manifests/base
kustomize edit set namespace <DESTINATION NAMESPACE>   # Set the namespace in the manifest where you want to deploy the dashboard
kustomize build . | oc apply -f -
```

```
# Deploy ODH Dashboard with authentication AND the default configs for groups and ODHDashboardConfig
cd manifests/overlays/odhdashboardconfig
kustomize edit set namespace <DESTINATION NAMESPACE>   # Set the namespace in the manifest where you want to deploy the dashboard
kustomize build . | oc apply -f -
# You will need to re-run the previous step if you receive the error below
# error: unable to recognize "STDIN": no matches for kind "OdhDashboardConfig" in version "opendatahub.io/v1alpha"
```
