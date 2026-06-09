# 🚀 Deploy Automatizado: ArgoCD + K3s na AWS

Este repositório contém os manifestos e as configurações de infraestrutura utilizadas para implementar uma esteira de **GitOps** completa, realizando o deploy automatizado de uma aplicação.

O objetivo principal deste projeto foi focar na engenharia de infraestrutura, automação e práticas de entrega contínua (CD).

---

## 🛠️ Tecnologias Utilizadas

* **ArgoCD:** Ferramenta declarativa de GitOps para Kubernetes.
* **K3s:** Distribuição leve do Kubernetes, ideal para otimização de recursos.
* **AWS:** Provedor de nuvem utilizado para hospedar o cluster [mencione se usou EC2, instâncias puras, etc.].
* **Kubernetes:** Orquestração dos containers da aplicação.
* **[Adicione outra ferramenta se usou, ex: GitHub Actions, Terraform, Docker]**

---

## 🏗️ O que foi desenvolvido?

1. **Estrutura de GitOps:** Configuração do ArgoCD para monitorar este repositório e garantir que o estado do cluster na AWS seja sempre idêntico ao definido no Git.
2. **Orquestração com K3s:** Criação e configuração de um cluster Kubernetes leve e performático na nuvem.
3. **Gerenciamento de Recursos:** Escrita de manifestos declarativos (Deployments, Services, Ingress, etc.) para a aplicação.

> 💡 **Nota sobre a aplicação:** Como o foco absoluto deste projeto foi a arquitetura de DevOps, automação e resiliência da infraestrutura, a API utilizada no backend é um fork de um projeto existente, servindo como base real de testes para validar o pipeline.

---

## 👥 Como testar / Contribuir
[Escreva uma linha rápida aqui, ex: "Os manifestos principais do ArgoCD estão na pasta /k8s ou /argo-apps."]
