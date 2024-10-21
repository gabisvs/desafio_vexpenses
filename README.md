---

##  Desafio do Estágio em DevOps - VExpenses

--- 

### 🌟 Automação de Infraestrutura com Terraform na AWS

---

```markdown
## 📖 Descrição Técnica da Infraestrutura

Este projeto configura uma infraestrutura básica na **AWS** com os seguintes recursos:

- 🌐 **VPC (Virtual Private Cloud):** Cria uma rede virtual isolada com suporte a DNS. A VPC serve como a base para a comunicação entre os recursos.
- 🏷️ **Subnet:** Configura uma sub-rede dentro da VPC na zona de disponibilidade `us-east-1a`, permitindo a segmentação de rede.
- 🌍 **Internet Gateway:** Um gateway que permite à sub-rede acessar a internet, essencial para a comunicação externa.
- 🛣️ **Tabela de Rotas:** Define as rotas de tráfego de saída para permitir que a sub-rede envie dados para a internet por meio do Internet Gateway.
- 🔒 **Grupo de Segurança:** Define regras de firewall para permitir conexões SSH e HTTP. Por padrão, permite conexões SSH de um IP específico e todo o tráfego HTTP (porta 80) para o servidor Nginx.
- 🔑 **Key Pair:** Gera uma chave SSH para acessar a instância EC2, garantindo acesso seguro.
- 💻 **Instância EC2:** Cria uma máquina virtual Debian usando a AMI mais recente, configura o servidor para se conectar à sub-rede e permite acesso remoto e à internet.
- 📤 **Outputs:** Exibe a chave privada gerada para o acesso SSH e o IP público da instância EC2.

---

## 🚀 Funcionalidades e Melhorias Implementadas

### 🔐 Segurança Aprimorada
- **Acesso SSH restrito:** 
  - No código original, o acesso SSH estava liberado para qualquer endereço IP (`0.0.0.0/0`). Para aumentar a segurança, modifiquei o Grupo de Segurança para permitir conexões SSH apenas a partir de um IP específico, configurado pela variável `allowed_ssh_ip`.
  - **Benefício:** Limitar o acesso SSH reduz as chances de tentativas de acesso não autorizadas, aumentando a segurança e protegendo contra ataques de força bruta.

### 🤖 Automação Completa do Nginx
- **Instalação e Configuração Automática do Nginx:**
  - A instância EC2 é provisionada com um script que instala, inicia e configura o Nginx automaticamente durante a inicialização, utilizando `user_data`.
  - **Benefício:** Isso garante que o servidor web Nginx esteja pronto para uso assim que a instância for criada, economizando tempo e evitando erros de configuração manual. Assim, qualquer nova instância criada a partir deste código estará pronta para servir páginas web imediatamente.

### 🛠️ Uso de Variáveis para Flexibilidade e Modulação
- **Variáveis para Configurações Essenciais:**
  - O código foi estruturado para usar variáveis, permitindo a configuração do tipo de instância EC2 (`instance_type`), o IP permitido para SSH (`allowed_ssh_ip`), e o CIDR da VPC e Subnet. 
  - **Benefício:** Isso facilita ajustes rápidos e personalização do ambiente sem a necessidade de modificar diretamente o código principal, tornando o gerenciamento mais eficiente e o código mais limpo.

---

## 🛠️ Pré-requisitos

Antes de começar, certifique-se de ter as seguintes ferramentas instaladas e configuradas:

- [Terraform](https://www.terraform.io/downloads.html) (v1.0 ou superior)
- Conta e credenciais configuradas na [AWS](https://aws.amazon.com/)
- Permissões para criar e gerenciar recursos na **AWS**

---

## 📂 Estrutura de Arquivos

```plaintext
├── main.tf        # Código principal em Terraform
```

---

## 🏗️ Como Executar o Projeto

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

## 🏆 Conclusão

Este projeto demonstra como criar uma infraestrutura segura e automatizada na AWS utilizando **Terraform**. As melhorias de segurança e a automação garantem uma solução eficiente e fácil de gerenciar, alinhada com as melhores práticas de DevOps.
```
