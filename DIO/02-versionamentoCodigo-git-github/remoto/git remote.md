### Definição: Git Remote

**`git remote`** gerencia referências aos repositórios remotos — URLs onde seu código é armazenado (GitHub, GitLab, etc). É o elo entre seu repositório local e o servidor.

Um remote é um apelido + URL. O mais comum é `origin` (criado automaticamente por [[git clone]]), mas você pode ter vários.

---

### Como Fazer: Operações Básicas

bash

```bash
# Ver todos os remotes
git remote -v

# Ver apenas nomes
git remote

# Adicionar um novo remote
git remote add origin https://github.com/usuario/repositorio.git

# Ver detalhes de um remote
git remote show origin

# Remover um remote
git remote remove origin

# Renomear um remote
git remote rename origin upstream
```

---

### Mudar a URL do Remote

Quando você clona com [[Personal Access Token (https)]] mas quer usar [[Ssh]], ou mudou de servidor:

bash

```bash
# Ver URL atual
git remote get-url origin

# Mudar para [[SSH]]
git remote set-url origin git@github.com:usuario/repositorio.git

# Mudar para [[Personal Access Token]] (HTTPS)
git remote set-url origin https://github.com/usuario/repositorio.git
```

---

### Exemplo 1: Setup Inicial (Init + Remote)

Você criou um repositório local vazio e quer conectar a um servidor:

bash

```bash
git init
git remote add origin https://github.com/usuario/novo-repo.git

# Verifica
git remote -v
# Saída: origin https://github.com/usuario/novo-repo.git

# Agora pode fazer push
git add .
git commit -m "primeiro commit"
git push -u origin main
```

---

### Exemplo 2: Múltiplos Remotes (GitHub + GitLab)

Sincronizar código em dois servidores:

bash

```bash
git remote add origin https://github.com/usuario/repo.git
git remote add backup https://gitlab.com/usuario/repo.git

# Ver todos
git remote -v

# Push para ambos
git push origin main
git push backup main
```

---

### Exemplo 3: Mudar de HTTPS para SSH

Você clonou com [[Personal Access Token (https)]] mas quer usar [[Ssh]] (sem senha):

bash

```bash
git remote set-url origin git@github.com:usuario/repo.git

# Verifica
git remote -v

# Agora push/pull usam SSH
git push origin main
```

---

### Troubleshooting

|Problema|Solução|
|---|---|
|`fatal: 'origin' does not appear to be a 'git' repository`|Remote não existe; use `git remote add origin <URL>`|
|`remote already exists`|Remote já foi adicionado; use `git remote remove` depois adicione novamente|
|`Permission denied` ao fazer push|[[SSH]] key não configurada ou URL incorreta|
|Não sabe qual é a URL do origin|Use `git remote get-url origin`|