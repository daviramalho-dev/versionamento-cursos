### Definição: Git Branch

**`git branch`** cria, lista ou deleta branches — linhas de desenvolvimento paralelas. Um branch é um "ramo" independente do código onde você trabalha sem afetar a branch principal (`main`). Cada branch tem seu próprio histórico de [[Commit]]s.

---

### Como Fazer

bash

```bash
# Listar branches locais
git branch

# Listar branches locais e remotos
git branch -a

# Criar novo branch
git branch feature-login

# Criar e entrar no branch (em um comando)
git branch feature-login && git checkout feature-login

# Deletar branch (seguro - só deleta se merged)
git branch -d feature-login

# Deletar branch forçado (perigoso - perde commits não merged)
git branch -D feature-login

# Renomear branch
git branch -m feature-login feature-auth
```

---

### Exemplo 1: Criar e Listar Branches

bash

```bash
# Ver branches atuais
git branch
# * main (você está aqui)

# Criar novo branch
git branch feature-api

# Ver branches novamente
git branch
# * main
#   feature-api
```

---

### Exemplo 2: Deletar Branch

Você terminou uma feature e fez merge. Agora quer deletar o branch:

bash

```bash
# Ver branches
git branch

# Deletar (seguro - rejeita se não foi merged)
git branch -d feature-api

# Forçar delete (perigoso!)
git branch -D feature-api
```

---

### Por Quê Usar Branches

Branches permitem que múltiplas pessoas trabalhem em features diferentes sem conflitar. Você cria um branch, trabalha isolado, faz [[git commit]]s, e depois mescla com [[git merge]] quando pronto.

**Fluxo típico:**

```
1. Criar branch: git branch feature-x
2. Entrar no branch: git checkout feature-x
3. Trabalhar e fazer commits
4. Voltar para main: git checkout main
5. Mesclar: git merge feature-x
```

---

### Tabela: Estados de Branch

|Comando|O quê faz|
|---|---|
|`git branch`|Lista branches locais|
|`git branch -a`|Lista todos (locais + remotos)|
|`git branch nome`|Cria novo branch|
|`git branch -d nome`|Deleta (seguro)|
|`git branch -D nome`|Deleta forçado (perigoso)|