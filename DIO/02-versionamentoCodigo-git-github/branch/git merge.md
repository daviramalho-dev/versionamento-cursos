### Definição: Git Merge

**`git merge`** mescla uma branch em outra, integrando os [[Commit]]s. Quando você termina uma feature em uma branch separada, merge reintegra esse trabalho com a branch principal (`main`). Git tenta mesclar automaticamente, mas às vezes há conflitos.

---

### Como Fazer

bash

```bash
# Mesclar feature-api em main
git checkout main
git merge feature-api

# Mesclar sem criar commit de merge (squash)
git merge --squash feature-api

# Abortar merge se der conflito
git merge --abort

# Mesclar e deletar branch automaticamente
git merge --delete feature-api
```

---

### Exemplo 1: Merge Simples (Sem Conflito)

Feature terminou e está pronta para main:

bash

```bash
# Entrar em main
git checkout main

# Mesclar feature-api
git merge feature-api

# Git cria commit de merge automaticamente
# main agora tem todos os commits de feature-api
```

---

### Exemplo 2: Merge com Conflito

Você e um colega editaram o mesmo arquivo:

bash

```bash
# Tentar mesclar
git merge feature-login

# Conflito! Git marca as diferenças
# arquivo.js contém:
# <<<<<<< HEAD
# seu código
# =======
# código do colega
# >>>>>>> feature-login

# Resolver manualmente (editar arquivo)
# Depois marcar como resolvido
git add arquivo.js
git commit -m "Resolve merge conflict"
```

---

### Cascata: Antes e Depois do Merge

```
Antes de merge:
main:  commit A → B → C
feature-api: commit A → B → D → E

Depois de merge:
main: commit A → B → C → (merge commit) → D → E
feature-api: continua igual (não muda)
```

---

### Estratégias de Merge

|Tipo|Comando|Quando usar|
|---|---|---|
|Fast-forward|`git merge feature`|Branch é continuação linear (padrão)|
|Merge commit|`git merge --no-ff`|Quer preservar que foi uma branch|
|Squash|`git merge --squash`|Muitos commits pequenos, quer limpar história|

---

### Troubleshooting

|Problema|Solução|
|---|---|
|Conflito de merge|Edite arquivo manualmente, `git add`, `git commit`|
|Muitos conflitos|Converse com colega, considere rebase|
|Errou o merge|`git merge --abort` antes de comitar|
|Quer reverter merge pronto|`git revert -m 1 <commit-do-merge>`|