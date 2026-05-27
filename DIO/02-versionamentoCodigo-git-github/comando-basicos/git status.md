### Definição: Git Status

**`git status`** mostra o estado atual do repositório — quais arquivos foram modificados, quais estão prontos para commit (staged), quais não estão rastreados. É o comando que você executa para entender "onde estou agora?".

Git divide arquivos em três estados: **modified** (alterado), **staged** (pronto para [[git commit]]), **untracked** (não rastreado ainda).

---

### Como Fazer

bash

```bash
# Ver status completo
git status

# Ver resumido (mais limpo)
git status -s
git status --short
```

**Saída típica:**

```
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to stage)
        modified:   arquivo.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        novo.txt

nothing added to commit but untracked changes present
```

---

### Interpretando a Saída

|Status|Significa|
|---|---|
|`modified:`|Arquivo mudou, mas ainda não foi adicionado ao staging|
|`new file:`|Arquivo novo foi adicionado ao staging (pronto para commit)|
|`Untracked files:`|Git não conhece esse arquivo ainda|
|`nothing to commit`|Tudo já foi commitado ou não há mudanças|

---

### Exemplo 1: Workflow Básico

bash

```bash
# Criar arquivo
echo "conteúdo" > arquivo.txt

# Ver status
git status
# Mostra: arquivo.txt é untracked

# Adicionar ao staging
git add arquivo.txt

# Ver status novamente
git status
# Mostra: "new file: arquivo.txt" pronto para commit
```

---

### Exemplo 2: Resumido vs Completo

bash

```bash
# Completo (padrão)
git status

# Resumido
git status -s
# Saída: M  arquivo.txt (M = modified)
#        ?? novo.txt  (?? = untracked)
```

---

### Por Quê Usar

Antes de fazer [[git add]] ou [[git commit]], você precisa saber o que mudou. `git status` previne commits acidentais — você vê exatamente quais arquivos serão incluídos e qual é o estado deles.