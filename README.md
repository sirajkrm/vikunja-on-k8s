# This is a local helmchart to deploy Vikunja TODO app on Kubernetes + Keycloak
Vikunja is an to-do app that can be selfhosted.


# Architecture
- The app consist of 3 microservices: frontend, backend, and database.
- NOTE: the version in use here is 0.22.1 as it's the last release that has this kind of architecture.
- If you're going to use later releases e.g. 0.23 then be aware that frontend+backend are consolidated into one single deployment.


# Prerequites
- The storage solution in use here is **Longhorn** as it guaratees the HA of the volumes in use by creating replicas (copies) across the k8s cluster nodes.
- The default storageclass is **longhorn**.
- The app expects to have Keycloak deployed and configured to have a realm called "vikunja" along with a client secret.
- This is to implement Identity and Access Management (IAM) for secure authentication and authorization for the  multiple users and groups.
- Please check the **backend.yaml** file and edit the config accordingly.


# Install the helmchart
```
helm install vikunja selfhosted-vikunja-keycloak/ --values selfhosted-vikunja-keycloak/values.yaml
```

# Accessing it
- depending on the ingress host you indicated, you should be able to access it by pasting the host on the browser.


# Room for improvement
- You can use a managed database e.g. AWS RDS or Google Cloud SQL to remove the headache of maintaing the database workload.
- You can use Keycloak chart if you don't want to define the whole deployment/statefulset from scratch.
- By default all microservices are accessible to each other, use Network Policies to control egress+ingress traffic.
