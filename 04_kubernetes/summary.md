# Kubernetes (K8s): ferramenta para Orquestração de Containers

## Arquitetura

- **Master node**: Kube-apiserver; Kube Controller Manager / Cloud Controller Manager; kube-scheduler; etcd; Container Runtime (Docker; ContainerID)
- **Worker nodes**: kubelet (agent); kube-Proxy; Container Runtime
- **kubectl**: CLI (interface de linha de comandos) do Kubernetes

## Componentes

- Pod
- ReplicaSet
- Deployment
- Services
- Disks (Persistent Volume)
- Requests & Limits
- HPA
- Namespaces
- Health Check

## Services

- ClusterIP
- NodePort
- LoadBalancer
- Ingress
- externalName

## Clusters Kubernetes em Cloud (serviços gerenciados)

- Azure Kubernetes Service (**AKS**)
- AWS Elastic Kubernetes Service (**EKS**)
