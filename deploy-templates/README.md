# springboot-rollout

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.1.0](https://img.shields.io/badge/AppVersion-0.1.0-informational?style=flat-square)

A Helm chart for Kubernetes

**Homepage:** <https://github.com/KubeRocketCI/template-springboot.git>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| DEV Team |  |  |

## Source Code

* <https://github.com/KubeRocketCI/template-springboot.git>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `100` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"springboot-rollout"` |  |
| image.tag | string | `""` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets[0].name | string | `"regcred"` |  |
| ingress.annotations | object | `{}` |  |
| ingress.className | string | `""` |  |
| ingress.dnsWildcard | string | `"development.krci-dev.cloudmentor.academy"` |  |
| ingress.enabled | bool | `true` |  |
| ingress.hosts[0].host | string | `"edpDefault"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ingress.tls | list | `[]` |  |
| livenessProbe.tcpSocket.port | string | `"http"` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` | https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| readinessProbe.initialDelaySeconds | int | `20` |  |
| readinessProbe.tcpSocket.port | string | `"http"` |  |
| replicaCount | int | `3` |  |
| resources | object | `{}` |  |
| securityContext | object | `{}` |  |
| service.port | int | `8080` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.automount | bool | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template |
| tolerations | list | `[]` | https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/ |
| volumeMounts | list | `[]` |  |
| volumes | list | `[]` |  |


This diagram illustrates the CI/CD workflow for performing a rolling update of a sample Java application using KubeRocketCI, Github, Tekton, Argo CD, and other integrated tools:

Code Push to Github:

The process starts with the student pushing code changes to the Github repository $<account_id>/springboot-rollout.
This action triggers Github to generate an event.
Event Trigger:

The Github event triggers a series of automated processes within the KubeRocketCI platform.
Review Pipeline:

The event triggers the Review pipeline in KubeRocketCI, which is executed using Tekton.
The review pipeline fetches the code from the Git Server and performs code review and quality checks using SonarQube.
After successful completion, it passes the control to the Build Pipeline.
Build Pipeline:

The Build pipeline is responsible for compiling the code, running tests, and building the application artifact.
The pipeline creates a container image of the application and pushes it to the AWS Elastic Container Registry (ECR).
It also tags the Git repository to mark the successful build.
Manual Trigger:

A manual trigger is required to initiate the Deploy Pipeline.
The student or an automated process can trigger the deployment.
Deploy Pipeline:

The Deploy Pipeline is responsible for deploying the application to the Kubernetes cluster in a Rolling Update strategy.
It retrieves the container image from AWS ECR and deploys it to the specified deployment flow.
Argo CD Integration:

Argo CD manages the deployment process and ensures that the desired state of the application is maintained in the Kubernetes cluster.
The deploy pipeline integrates with Argo CD to manage deployments and rollbacks.
Dev Environment Deployment:

The application is deployed to the Dev environment within the Kubernetes cluster.
The deploy pipeline ensures that the application is running as a pod in the specified deployment flow.
The Rolling Update strategy ensures that the updates are gradually applied to the pods, maintaining high availability and zero downtime.
New Tool: Rollout Deployment
One of Kubernetes' features is its ability to leverage various deployment strategies. One such strategy is the Rolling Update, which allows updates to be gradually released to pods in a deployment, ensuring no downtime and that the update process can be automatically rolled back if issues arise. This approach maintains high availability and ensures that updates do not disrupt the user experience. With KubeRocketCI, developers can configure and manage rolling updates, enforcing continuous deployment best practices in a Kubernetes environment.

Task Goal
The task goal is to perform a rolling update of a sample Java 17 application using KubeRocketCI, showcasing the platform's capabilities in achieving continuous deployment with zero downtime. To achieve this, you will practice updating a deployment on KubeRocketCI using a Rolling Update strategy.

Naming Conventions
Please adhere to the following naming conventions for the resources to ensure smooth task verification:

Application: springboot-rollout
Deployment Flow: rollout
Environment: dev