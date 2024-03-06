# Git - Controle de Versionamento de Código

## Comandos

### Instalação (Linux) e Configuração do git

### Comandos de rotina

```bash
git init
```

```bash
git status
```

```bash
git add .
```

```bash
git commit -m "mensagem"
```

```bash
git push
```

```bash
git pull
```

### Trabalhar com Branchs Tags

```bash
git branch
```

```bash
# alternar entre as branchs
git checkout new-branch
# criar e alternar para a nova branch
git checkout -b new-branch
```

```bash
# boa prática: deletar as branchs não mais utilizadas
git branch -d branch-name
git push # apagar no repositório remoto
```

```bash
git tag new-tag
```

gitflow(imagem)

### Trabalhando com repositórios remotos

- Criar Chaves SSH

```bash
ssh-keygen -t RSA -b 4096 -C "meu_email@email.com"
cat ~/.ssh/id_rsa.pub
```

```bash
git clone
```

```bash
git remote -v
```
