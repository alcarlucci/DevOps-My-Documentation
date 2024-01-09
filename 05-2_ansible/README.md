# Ansible - IaC

Gestão de configuração de infraestrutura - automatizar IT tasks.

## Fundamentos

- O que é uma IT task (tarefas de TI)
  - Backups
  - Updates; instalar dependências
  - Atribuir Grupos
  - Reiniciar Servidores
  - Criar usuários
  - Copiar arquivos

- Por que usar o Ansible
  - executar da própria máquina (Control Tower)
  - agnóstico de plataforma
  - automatizar IT tasks para tarefas repetitivas
  - Agentless: não requer agentes, é baseado em SSH

- Instalação do Ansible:
  > `apt install ansible`

- Arquivos no Ansible:
  - **Inventory** (txt): IP address ou hostname para os Targets
  - **Playbooks** (yaml): definição das IT tasks de configuração

- Componentes:
  - Variables
  - Roles
  - Module (pequena task epecífica)

- Comandos básicos para execução
  - Direto no terminal usando apenas arquivo de inventário (exemplo com Ping)
    > `ansible vm-target1 -i inventory.txt -m ping`
  - Usando Playbook e arquivo de inventário
    > `ansible-playbook -i inventory.txt playbook.yaml`
