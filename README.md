
```markdown
# 🌐 Projeto de Infraestrutura AWS com Terraform

Este repositório contém um projeto de infraestrutura como código (IaC) utilizando **Terraform** para provisionar recursos na **AWS**. O objetivo é criar uma estrutura segura e automatizada que inclui VPC, Subnet, instância EC2 com Nginx e regras de segurança aprimoradas.

---

## 📋 Tecnologias Utilizadas

- **Terraform** - Automação da infraestrutura
- **AWS** - Ambiente de nuvem
- **EC2** - Instância de servidor
- **VPC** - Rede privada virtual
- **Nginx** - Servidor web

---

## ⚙️ Pré-requisitos

Antes de começar, certifique-se de ter as seguintes ferramentas instaladas e configuradas:

- [Terraform](https://www.terraform.io/downloads.html) (v1.0 ou superior)
- Conta e credenciais configuradas na [AWS](https://aws.amazon.com/)
- Permissões para criar e gerenciar recursos na AWS

---

## 🚀 Funcionalidades do Projeto

- Criação de uma **VPC** com sub-rede privada
- Provisionamento de uma instância **EC2** com **Nginx** instalado automaticamente
- **Grupo de Segurança** configurado para acesso seguro via SSH e HTTP
- Uso de **variáveis** para facilitar a configuração e personalização do ambiente

---

## 📂 Estrutura de Arquivos

```plaintext
├── main.tf        # Código principal em Terraform
├── README.md      # Documentação do projeto
```

---

## Como Executar o Projeto

### 1. Clonar o Repositório

```bash
git clone https://github.com/seuusuario/seurepositorio.git
cd seurepositorio
```

### 2. Inicializar o Terraform

```bash
terraform init
```

### 3. Visualizar o Plano de Infraestrutura

```bash
terraform plan
```

### 4. Aplicar a Configuração

```bash
terraform apply
```

### 5. Acessar a Instância EC2 via SSH

Após a configuração ser aplicada, o Terraform exibirá o **IP público** e a **chave privada** gerada. Use o comando abaixo para se conectar:

```bash
ssh -i <caminho-da-chave>/nome-da-chave.pem ubuntu@<ec2_public_ip>
```

---

## 📌 Variáveis do Projeto

As variáveis podem ser ajustadas para personalizar a infraestrutura:

| Variável         | Descrição                                     | Valor Padrão     |
|------------------|-----------------------------------------------|------------------|
| `instance_type`  | Tipo de instância EC2                         | `t2.micro`       |
| `allowed_ssh_ip` | IP permitido para conexões SSH                | `0.0.0.0/0`      |
| `vpc_cidr`       | CIDR para a VPC                               | `10.0.0.0/16`    |
| `subnet_cidr`    | CIDR para a Subnet                            | `10.0.1.0/24`    |

---
