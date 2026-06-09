# 🚀 Deploy Automatizado: ArgoCD + K3s

Este repositório contém os manifests e configurações usados para demonstrar uma esteira GitOps usando ArgoCD sobre um cluster K3s (ex.: rodando em instâncias na AWS). O foco é infraestrutura, automação e entrega contínua.

---

## 🛠️ Tecnologias

- **ArgoCD** — GitOps declarativo para Kubernetes.
- **K3s** — Kubernetes leve, adequado para ambientes de teste e edge.
- **AWS** — Provedor de infraestrutura (ex.: EC2) usado para hospedar o cluster.
- **kubectl / argocd CLI** — ferramentas de linha de comando para operar o cluster e ArgoCD.

---

## Estrutura do repositório

- `k8s/` — manifests e kustomization usados pelo ArgoCD ou aplicáveis diretamente ao cluster.
	- `api-deployment.yaml` — Deployment da API.
	- `api-service.yaml` — Service expondo a API.
	- `argocd-app.yaml` — App manifest do ArgoCD (aponta para este repositório ou paths internos).
	- `kustomization.yaml` — Kustomize para montar os manifests.
	- `namespace.yaml` — Namespace dedicado para a aplicação.
	- `postgres-deployment.yaml` — Deployment do Postgres (ex.: para testes).
	- `postgres-pvc.yaml` — PersistentVolumeClaim para Postgres.
	- `postgres-service.yaml` — Service do Postgres.
	- `secret.yaml.example` — Exemplo de secret para variáveis sensíveis (NUNCA com valores reais neste repositório).

---

## Pré-requisitos

- Acesso ao cluster Kubernetes (kubeconfig configurado).
- `kubectl` instalado.
- `argocd` CLI instalado (opcional, para operações via CLI).
- Credenciais AWS configuradas, se for usar infra na AWS.

---

## Como usar

1. Ajuste as configurações e segredos locais: copie `k8s/secret.yaml.example` para `k8s/secret.yaml` e preencha os valores sensíveis localmente ou use um gerenciador de segredos (SealedSecrets / External Secrets / SSM / Secrets Manager).

2. Aplicar manifests diretamente (modo manual / teste):

```powershell
kubectl apply -f k8s/namespace.yaml
kubectl apply -k k8s
```

3. Aplicar via ArgoCD (fluxo GitOps):

- Garanta que o ArgoCD esteja instalado no cluster.
- Crie ou atualize um `Application` que aponte para este repositório/path. Exemplo mínimo (já existe em `k8s/argocd-app.yaml`):

```powershell
kubectl apply -f k8s/argocd-app.yaml
```

Depois, acesse a UI do ArgoCD ou use `argocd app sync <nome-da-app>` para sincronizar.

---

## Personalização

- Para trocar a imagem da aplicação, edite `k8s/api-deployment.yaml` ou utilize `kustomization.yaml` com `images:`.
- Para alterar recursos de infraestrutura (CPU/memória, volumes), edite os manifests correspondentes em `k8s/`.

---

## Segurança e Segredos

- Não comite segredos em texto plano. Use `secret.yaml.example` como template.
- Recomenda-se integrar com um provedor de segredos (AWS Secrets Manager, SSM Parameter Store, External Secrets, SealedSecrets) para produção.

---

## Testes e validação

- Verifique o estado dos objetos no cluster:

```powershell
kubectl get pods -n <namespace>
kubectl describe pod <pod-name> -n <namespace>
kubectl logs <pod-name> -n <namespace>
```

- Para ArgoCD:

```powershell
argocd app list
argocd app get <nome-da-app>
argocd app sync <nome-da-app>
```

---

## Observações

- Este repositório foi criado como exemplo didático/avaliativo para demonstrar práticas de GitOps e automação. Ajustes serão necessários para executar em um ambiente de produção (rede, segurança, backups, monitoramento).