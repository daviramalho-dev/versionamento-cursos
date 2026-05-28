### Definição: Git Pull

**`git pull`** baixa os [[Commit]] do repositório remoto e mescla com seu branch local. É basicamente `git fetch` + `git merge` executados juntos — você não apenas baixa, mas integra as mudanças ao seu código.

Pull sincroniza seu trabalho local com o que o time fez no servidor.

---

### Como Fazer

bash

```bash
# Pull do branch atual (usa remote padrão origin)
git pull

# Pull explícito
git pull origin main

# Pull com rebase (em vez de merge)
git pull --rebase

# Ver o que vai descer sem fazer (dry-run)
git pull --no-commit
```

---

### Exemplo 1: Pull Básico

Seus colegas pushearam código e você quer atualizar:

bash

```bash
# Ver que há mudanças remotas
git status

# Baixar e mesclar
git pull

# Seu código agora tem as mudanças do time
git log --oneline
# Novos commits aparecem no histórico
```

---

### Exemplo 2: Conflito During Pull

Você e um colega editaram o mesmo arquivo:

bash

```bash
# Pull tenta mesclar
git pull origin main
# Conflito! Ambos editaram arquivo.js

# Ver status
git status
# Shows: "both modified: arquivo.js"

# Abrir arquivo e resolver manualmente
# (editar secções com <<<<<<, ======, >>>>>>)

# Após resolver
git add arquivo.js
git commit -m "Resolve merge conflict"
```

---

### Push vs Pull

|Comando|O quê faz|Quando usar|
|---|---|---|
|`git push`|Envia seus commits para servidor|Terminou feature, quer compartilhar|
|`git pull`|Baixa commits do servidor, mescla|Começar dia de trabalho, antes de trabalhar|
|**Fluxo ideal**|Pull → Trabalhar → Commit → Push|Sempre Pull antes de Trabalhar|

---

### Cascata: Antes e Depois

```
Antes de git pull:
Local: commit A, B
Remote: commit A, B, C, D (time fez mais commits)

Depois de git pull:
Local: commit A, B, C, D (atualizado com trabalho do time)
```

---

### Troubleshooting

|Problema|Causa|Solução|
|---|---|---|
|`fatal: No configured push destination`|Remote não existe|Configure com `git remote add origin URL`|
|Conflitos na mesclagem|Você e colega editaram mesmo arquivo|Resolva manualmente os conflitos|
|`Updates were rejected` (pull)|Seu remote está desatualizado|Faça `git fetch` antes ou `git pull --rebase`|
|Muitos conflitos|Divergência grande entre local e remoto|Considere checkout novo ou discutir com time|
