### Definição: Git Checkout

**`git checkout`** muda de branch ou volta um arquivo a um [[Commit]] anterior. É o comando para "navegar" entre branches ou "reverter" mudanças. Checkout alterna seu working directory para refletir um estado diferente do repositório.

---

### Como Fazer

bash

```bash
# Mudar para outro branch
git checkout main

# Mudar para branch e criar se não existir
git checkout -b feature-novo

# Voltar um arquivo a um commit anterior
git checkout HEAD -- arquivo.txt

# Voltar arquivo a um commit específico
git checkout abc1234 -- arquivo.txt

# Voltar a um commit anterior (detached HEAD)
git checkout abc1234
```

---

### Exemplo 1: Navegar Entre Branches

Você está em `main` e quer trabalhar em `feature-api`:

bash

```bash
# Ver branch atual
git branch
# * main

# Mudar para feature-api
git checkout feature-api

# Ver branch atual novamente
git branch
# * feature-api
#   main
```

---

### Exemplo 2: Revertendo Arquivo a Commit Anterior

Você editou um arquivo e quer voltar:

bash

```bash
# Ver histórico do arquivo
git log -- arquivo.js

# Voltar para versão anterior
git checkout HEAD -- arquivo.js

# Ou para um commit específico
git checkout abc1234 -- arquivo.js

# Verifica
git status
# arquivo.js está como era no commit
```

---

### Checkout vs Branch vs Merge

Use esses comandos juntos:

|Comando|O quê faz|Quando|
|---|---|---|
|`git branch nome`|Cria branch|Começar feature|
|`git checkout nome`|Muda para branch|Entrar em feature|
|`git checkout -b nome`|Cria E muda|Combo: cria + entra|
|`git merge nome`|Mescla branches|Terminar feature|

---

### Detached HEAD (Avançado)

Quando você faz `git checkout` de um [[Commit]] específico (não uma branch), entra em "detached HEAD". Útil para inspecionar histórico:

bash

```bash
# Ver um commit específico
git checkout abc1234

# Você está "desanexado" - mudanças aqui não salvam em branch
# Para voltar à branch
git checkout main
```