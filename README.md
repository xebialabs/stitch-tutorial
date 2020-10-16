# 'Stitch tutorial' repository

Note: This repository shall only be used with the [Stitch tutorial](./tutorial.md). Not for use in production scenarios.

Customizations available for deployments to Kubernetes:

"stitch-rules-add-team-name-label.yaml" :

- k8s.AddTeamName:  Add a 'team-name' label specifying static ('mario') team name

"stitch-rules-add-env-label.yaml" :

- k8s.MacroFreemarkerAddLabels: Reusable macro to add 'application' and 'environment' labels
- k8s.AddEnvAppLabels: Adds 'application' and 'environment' labels using names from XLD context. Utilizes shared macro.

"stitch-rules-content-conditions.yaml" :

- k8s.ChangePortForService: Enforces use of port 8081 instead of 8080 for a K8s service

"stitch-rules-scale-prod.yaml" :

- k8s.StandardJavaSvcProd: Standard configuration for Java FE services in PROD
