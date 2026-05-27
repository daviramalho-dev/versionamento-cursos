### Definição: Git Commit

**`git commit`** cria um commit — oficializa as mudanças que estão em staging (adicionadas com [[git add]]). Cada commit gera um [[Sha-1]] único e entra no histórico do [[Parente (pai)]].

Um commit bem feito explica **por quê** uma mudança foi necessária, não apenas **o quê** foi alterado.

---

### Como Fazer

```bash
# Commit simples com mensagem
git commit -m "Descrição da mudança"

# Commit usando editor (mais espaço para detalhes)
git commit

# Commit de arquivos modificados (sem git add antes)
git commit -a -m "Mensagem"

# Alterar último commit (antes de push)
git commit --amend

# Commit vazio (sem mudanças, raro)
git commit --allow-empty -m "Mensagem"
```

---

### Exemplo 1: Workflow Básico

```bash
# Modificar arquivo
echo "novo conteúdo" > app.js

# Adicionar ao staging
git add app.js

# Commitar
git commit -m "Add função de login"

# Ver histórico
git log --oneline
# a1b2c3d Add função de login
```

Você pode visualizar o histórico com [[git log]] para confirmar que o commit foi criado.

---
### Exemplo 2: Alterar Último Commit

Se você cometeu algo no último commit antes de fazer push:

````bash
# Modificar o arquivo
echo "correção" >> app.js

# Adicionar
git add app.js

# Amend (modifica o commit anterior)
git commit --amend

# O commit anterior é reescrito, não cria novo

`⚠️ **Nunca amend commits que já foram enviados (push)** — quebra histórico de outros.`
````

