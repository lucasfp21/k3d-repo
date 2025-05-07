# Cluster Kubernetes com K3d

Este README fornece um resumo sobre a criação e gerenciamento de clusters Kubernetes utilizando K3d, além de conceitos básicos de Pods e ReplicaSets.

## Criando um Cluster Kubernetes com K3d
K3d é uma ferramenta que facilita a execução de clusters Kubernetes em Docker.

### Criar um cluster padrão:
```sh
k3d cluster create
```

### Criar um cluster sem LoadBalancer:
```sh
k3d cluster create <nome-do-cluster> --no-lb
```

### Validar o cluster:
```sh
kubectl cluster-info
```

### Listar nós do cluster:
```sh
kubectl get nodes
```

### Listar containers em execução:
```sh
docker container ls
```

### Listar clusters K3d ativos:
```sh
k3d cluster list
```

### Criar um cluster com 3 control planes e 3 nós worker:
```sh
k3d cluster create <nome-do-cluster> --servers 3 --agents 3
```

### Criar um cluster com bind de porta:
```sh
k3d cluster create <nome-do-cluster> --servers 3 --agents 3 -p "8080:30000@loadbalancer"
```

### Deletar um cluster:
```sh
k3d cluster delete <nome-do-cluster>
```

## Gerenciamento de Recursos no Cluster
Podemos criar e gerenciar recursos como Deployments, Jobs e Pods utilizando arquivos YAML.

```sh
kubectl apply -f <arquivo.yaml>
```

### Exemplo de estrutura YAML para um Pod:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: meu-pod
spec:
  containers:
    - name: app
      image: nginx
      ports:
        - containerPort: 80
```

### Exemplo de estrutura YAML para um ReplicaSet:
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: meu-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
        - name: web
          image: nginx
          ports:
            - containerPort: 80
```

Esse README fornece um resumo dos conceitos essenciais para criar e gerenciar clusters Kubernetes com K3d. Caso queira ajustes ou mais detalhes, me avise! 🚀