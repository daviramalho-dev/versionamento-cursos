### Definição: Git Reflog

**`git reflog`** mostra o histórico de **movimentações de HEAD** — cada ação que você fez ([[git commit]], [[git reset]], [[git checkout]], etc). Enquanto [[git log]] mostra "o quê aconteceu", `git reflog` mostra "para onde você foi".

Use `git reflog` para recuperar commits que parecem "perdidos" após [[git reset]] ou outras operações.

---

### Como Fazer

bash

```bash
# Ver reflog completo
git reflog

# Ver resumido
git reflog -n 10

# Ver reflog de uma branch específica
git reflog main

# Ver detalhes de uma entrada
git show HEAD@{n}
```

**Saída típica:**

```
a1b2c3d (HEAD -> main) HEAD@{0}: reset: moving to abc1234
def5678 HEAD@{1}: commit: Add feature
ghi9012 HEAD@{2}: reset: moving to ghi9012
```

---

### Exemplo: Recuperar Commit Após Reset

Você fez `git reset --hard` e "perdeu" um commit:

bash

```bash
# Ver reflog
git reflog
# a1b2c3d HEAD@{0}: reset: moving to old-commit
# abc1234 HEAD@{1}: commit: Mudança importante
# def5678 HEAD@{2}: reset: moving to ...

# Ver qual commit você quer recuperar
git show HEAD@{1}

# Voltar para esse commit
git reset --hard HEAD@{1}

# Ou criar nova branch de um commit "perdido"
git checkout -b recover-branch abc1234
```

---

### Quando Usar

Use `git reflog` quando:

- Você fez [[git reset]] e quer desfazer
- Um commit desapareceu e precisa localizá-lo
- Quer ver tudo que você fez (audit de ações)

**Diferença rápida:**

- `git log` = histórico de commits
- `git reflog` = histórico do que **você** fez

---

### ⚠️ Reflog É Local

`git reflog` é **local** — só mostra suas ações nessa máquina. Não sincroniza com servidores. Dados do reflog expiram após 30 dias por padrão.