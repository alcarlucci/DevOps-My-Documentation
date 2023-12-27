# Terraform - IaC

Provisionamento de infraestrutura como código.

## Terraform Workflow

init -> validate -> fmt -> plan -> apply [-auto-approve] -> destroy

obs.: para executar os comandos terraform precisa estar logado na Cloud:

- Azure: `az login` ou `az login --use-device-code`
- AWS: `aws configure`

## Fundamentos

- **Arquivos no Terraform** (chamados Configuration Files ou Manifests)
  - uso de linguagem declarativa chamada HCL - HashiCorp Configuration Language

- **main.tf**; blocos normalmente utilizados:
  - `terraform {}`
  - `provider "<provedor-cloud>" {}`
  - `resource "<tipo-recurso>" "<nome>" {}`

- **output.tf**; retorno de informações apóes execução, exemplo retornar nome do RG criado:

```text
output "resource_group_name" {
  value = azurerm_resource_group.my_rg1.name
}
```

- **variables.tf**; variáveis - exemplo de var para região na Azure:

```text
variable "azure_region" {
  default = "eastus"
  description = "Azure Region where resources will be created"
  type = string
}
```

- **if** - syntax: `condition ? true_val : false_val`
- **Blocos dinâmicos**
- **Módulos**
- **Terraform Workspaces**
- **Terraform Data Sources**: buscar informações/recursos - usar recursos já existentes

## Boas Práticas

- Use um arquivo de variáveis;
- Use Backends para gerenciar os seus TFStates (storage account);
- Ative controle de versão nos Buckets ou Storage Account;
- Sempre use o CLI;
- Evite configurações *Hardcoded*;
- Use o `terraform fmt`;
- Use Módulos;
- Atualize sempre a versão do terraform.
