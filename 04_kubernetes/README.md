# Kubernetes - Orquestração de Containers

## Arquitetura

![Arquitetura Kubernetes](img/arquitetura-k8s.png)

- Master (node): responsável por gerenciar todas as operações do cluster
  - **Kube-apiserver**: ponto de entrada para todas as operações do cluster - API rest
  - **Kube Controller Manager** / **Cloud Controller Manager**: manter o estado do cluster
  - **kube-scheduler**: responsável pela alocação dos PODs nos workers
  - **etcd**: armazena os arquivos de configuração do kubernetes
  - **Container Runtime**: runtime de execução dos PODs (Docker; ContainerID)

- Worker Nodes:
  - **kubelet** (agent): agente que gerencia os PODs alocados no node
  - **kube-Proxy**: lidar com o roteamento de rede do node
  - **Container Runtime**: K8s é compatível com Docker, ContainerID e outros

## Fundamentos

- **Pod**: menor unidade do k8s; única instância de um aplicativo

```yaml
apiVersion: v1
kind: Pod
```

- **ReplicaSet**: conjunto de Pods; garantir a disponibilidade

```yaml
apiVersion: apps/v1
kind: ReplicaSet
```

- **Deployment**: rollout; rollback (add-on: flagger p/ outros tipos de deploy - canary, AB)

```yaml
apiVersion: apps/v1
kind: Deployment
```

- **Services**: fornece um IP virtual; fica na frente do Pod e atua como balanceador de carga
- Kubernetes **Disks** - persistent volume (PV) - armazenamento persistente:
  - Persistent Volumes: tipo do armazenamento (AKS: Azure Disk; Azure Files)
  - Storage Classes: classe de armazenamento (AKS: standard; premium)
  - Persistent Volume Claims: provisionamento dinâmico
- Kubernetes **Requests & Limits**:
  - Requests: CPU; Mem
  - Limits  : CPU; Mem
- Kubernetes **HPA** (Horizontal Pod Autoscaler) - escala horizontal automática de Pods
- Kubernetes **Namespaces**; boas práticas:
  - um cluster kubernetes para cada ambiente (dev; hml; prd)
  - um Namespace no cluster para cada aplicação (app1; app2; ...)
- **Health Check**:
  - Liveness Probe: ver se um container está em execução corretamente
  - Readiness Probe: ver se um container está pronto para receber tráfego
  - Startup Probe: ver se um container está em processo de inicialização

### Kubernetes Services

- **ClusterIP** (internal): comunicação interna entre Pods - frontend acessando backend
- **NodePort** (to internet): acessar aplicativos usando portas de work nodes (acessar pelo navegador)
- **LoadBalancer** (to internet): serviço k8s LoadBalancer que será mapeado para o balanceador de carga no provedor Cloud - (Azure Standard LB; AWS ELB)
- **Ingress** (to internet): balanceador de carga avançado de camada 7 (AWS ALB por ex.)

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
```

- **externalName**: acessar serviços externos (ex.: acessar DB AWS RDS por app presente no cluster k8s)

### Serviços gerenciados de Kubernetes em Cloud

- Azure: **AKS** - Azure Kubernetes Service
- AWS: **EKS** - Elastic Kubernetes Service
