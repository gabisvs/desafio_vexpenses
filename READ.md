# Desafio de Estágio em DevOps - VExpenses

## 1. Descrição Técnica da Infraestrutura

Este projeto cria uma infraestrutura básica na AWS usando Terraform. A infraestrutura inclui os seguintes recursos:

- **VPC (Virtual Private Cloud):** Cria uma rede virtual isolada com suporte a DNS. A VPC serve como a base para a comunicação entre os recursos.
- **Subnet:** Configura uma sub-rede dentro da VPC na zona de disponibilidade `us-east-1a`, permitindo a segmentação de rede.
- **Internet Gateway:** Um gateway que permite à sub-rede acessar a internet, essencial para a comunicação externa.
- **Tabela de Rotas:** Define as rotas de tráfego de saída para permitir que a sub-rede envie dados para a internet por meio do Internet Gateway.
- **Grupo de Segurança:** Define regras de firewall para permitir conexões SSH e HTTP. Por padrão, permite conexões SSH de um IP específico e todo o tráfego HTTP (porta 80) para o servidor Nginx.
- **Key Pair:** Gera uma chave SSH para acessar a instância EC2, garantindo acesso seguro.
- **Instância EC2:** Cria uma máquina virtual Debian usando a AMI mais recente, configura o servidor para se conectar à sub-rede e permite acesso remoto e à internet.
- **Outputs:** Exibe a chave privada gerada para o acesso SSH e o IP público da instância EC2.

## 2. Melhorias Implementadas

### 2.1. Melhoria de Segurança
- **Restrição de Acesso SSH:** 
  - No código original, o acesso SSH estava liberado para qualquer endereço IP (`0.0.0.0/0`). Para aumentar a segurança, modifiquei o Grupo de Segurança para permitir conexões SSH apenas a partir de um IP específico, configurado pela variável `allowed_ssh_ip`.
  - **Benefício:** Limitar o acesso SSH reduz as chances de tentativas de acesso não autorizadas, seguindo as melhores práticas de segurança.

### 2.2. Automação do Nginx
- **Instalação e Configuração Automática do Nginx:**
  - Adicionei um script no `user_data` da instância EC2 para instalar, iniciar e configurar o Nginx automaticamente durante a inicialização.
  - **Benefício:** Isso garante que o servidor web Nginx esteja pronto para uso assim que a instância for criada, economizando tempo e evitando erros de configuração manual.

### 2.3. Uso de Variáveis para Flexibilidade
- **Variáveis para Configurações Essenciais:**
  - Criei variáveis para configurar o tipo da instância EC2 e o IP permitido para conexões SSH, facilitando ajustes rápidos sem a necessidade de modificar diretamente o código.
  - **Benefício:** Melhora a modularidade e a flexibilidade do código, tornando-o mais adaptável para diferentes ambientes e cenários.

## 3. Instruções de Uso

### 3.1. Pré-requisitos
- Terraform instalado e configurado.
- Credenciais AWS válidas configuradas no ambiente.
- Permissões adequadas para criar e gerenciar recursos na AWS.

### 3.2. Comandos para Executar o Projeto

1. **Inicializar o Terraform:**
   ```bash
   terraform init
