### Estrutura geral de um manifest YAML
Recurso (raiz)
│
├── Cabeçalho (identidade)
│   ├── apiVersion
│   ├── kind
│   └── metadata
│       ├── name
│       └── labels
│
└── Spec (comportamento)
    │
    ├── Configurações principais
    │   ├── replicas
    │   └── selector
    │       └── matchLabels
    │
    └── Template (sub-recurso)
        ├── metadata
        │   └── labels
        └── spec
            └── containers
                ├── name
                ├── image
                └── ports

### Estrutura de um Service
Recurso (Service)
│
├── Cabeçalho (identidade)
│   ├── apiVersion
│   ├── kind: Service
│   └── metadata
│       └── name
│
└── Spec (comportamento)
    ├── selector
    │   └── matchLabels (quais Pods o Service conecta)
    │
    ├── type (ClusterIP, NodePort, LoadBalancer)
    │
    └── ports
        ├── port (porta exposta pelo Service)
        └── targetPort (porta do Pod)

### Selector e Labels
Service (raiz)
│
└── Spec
    ├── selector
    │   └── app: nginx-state   ← filtro
    └── ports
        └── port: 80

Pod (filho)
│
├── metadata
│   └── labels
│       └── app: nginx-state   ← etiqueta
└── spec
    └── containers
        └── image: nginx

### Estrutura de um StatefulSet
Recurso (StatefulSet)
│
├── Cabeçalho (identidade)
│   ├── apiVersion
│   ├── kind: StatefulSet
│   └── metadata
│       └── name
│
└── Spec (comportamento)
    ├── serviceName (Service headless associado)
    ├── replicas
    ├── selector
    │   └── matchLabels
    │
    ├── Template (sub-recurso)
    │   ├── metadata
    │   │   └── labels
    │   └── spec
    │       └── containers
    │           ├── name
    │           ├── image
    │           └── volumeMounts
    │
    └── volumeClaimTemplates (PVC por Pod)
        └── spec
            ├── accessModes
            └── resources
                └── requests.storage

### Regras práticas sobre selector e labels
- O **selector** sempre faz match com **labels** dos Pods.
- O match principal (selector ↔ label) deve bater, senão o recurso não funciona.
- Labels extras podem ser adicionadas nos Pods para organização e filtros adicionais.
- A label usada no selector é a **principal** daquele recurso; as demais são auxiliares.

### Analogias para memorizar
- **Raiz** = recurso principal (Deployment, Service, StatefulSet, etc.)
- **Tronco** = spec (comportamento)
- **Galhos** = sub-recursos (containers, volumes, ports, volumeClaimTemplates)
- **Label** = etiqueta colada no Pod
- **Selector** = filtro que procura etiquetas
