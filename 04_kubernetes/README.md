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

## Lista de Comandos

Utilizando o **kubectl** que é a CLI (interface de linha de comandos) do Kubernetes.

### Pods

```bash
# Criar um Pod
# kubectl run <desired-pod-name> --image <container-image>
kubectl run my-first-pod --image iesodias/nginx-images:v1
```

```bash
# Listar Pods
kubectl get pods
kubectl get pods -o wide
```

```bash
# Descrever um Pod
# kubectl describe pod <pod-name>
kubectl describe my-first-pod
```

```bash
# Excluir um Pod
# kubectl delete pod <pod-name>
kubectl delete my-first-pod
```

### ReplicaSet

### Deployment

### Services

```bash
# Obter informações de Serviços
kubectl get service
kubectl get svc
```

```bash
# Descrever um Serviço
# kubectl describe service <service-name>
kubectl describe service my-first-service
```

```bash
# Load Balancer Service (Expor um Pod)
# kubectl expose pod <pod-name> --type=LoadBalancer --port=<porta> --name=<service-name>
kubectl expose pod my-first-pod --type=LoadBalancer --porta=80 --name=my-first-service

# Para acessar a Aplicação
http://<External-IP-from-get-service-output>
```

### YAML (Manifestos do Kubernetes - arquivos de definições)

```yaml
# Estrutura básica
apiVersion:
Kind:
metadata:
spec:
```

```yaml
# Criar a definição simples de um Pod (ex.: "meu-manifeto.yaml" com conteúdo abaixo)
apiVersion: v1
Kind: Pod
metadata: # Dict
  name: my-first-pod
  labels:
    app: my-first-pod
spec:
  containers: # List
    - name: my-first-pod
      image: iesodias/nginx-images:v1
      ports:
        - containerPort: 80
```

```bash
# Criar os recurso a partir de um Manifesto Kubernetes (arquivo de configuração)
# kubectl create -f <nome-arq-manifesto.yaml>
kubectl create -f meu-manifesto.yaml
```
