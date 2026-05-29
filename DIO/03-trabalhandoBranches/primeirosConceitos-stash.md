### Definição: git stash

O [[git stash]] guarda temporariamente mudanças não commitadas (staged ou untracked) e limpa o working directory, sem criar um [[git commit|commit]]. É útil quando você precisa trocar de contexto — mudar de branch, puxar atualizações — mas o trabalho em andamento ainda não está pronto para ser commitado.

Pense como uma pilha: cada `stash` empilha um estado. Você pode ter vários ao mesmo tempo e restaurar qualquer um individualmente.

---

### Como fazer

**Guardar mudanças**

bash

```bash
git stash                          # salva com mensagem automática (WIP on <branch>)
git stash save "descrição clara"   # salva com mensagem personalizada — prefira isso
```

**Listar o que está guardado**

bash

```bash
git stash list
# stash@{0}: WIP on funcionalidade-grande: 3db5173 adicionando arquivo2...
# stash@{1}: On funcionalidade-grande: Adicionado arquivos iniciando alteracoes
```

O índice `{0}` é sempre o mais recente.

**Restaurar um stash**

bash

```bash
git stash pop              # restaura o stash@{0} e o remove da pilha
git stash pop 1            # restaura o stash@{1} especificamente e o remove
git stash apply stash@{1}  # restaura sem remover da pilha
```

A diferença entre `pop` e `apply`: o `pop` descarta o stash após restaurar; o `apply` mantém na lista para uso posterior.

**Limpar a pilha**

bash

```bash
git stash drop stash@{0}   # remove um stash específico
git stash clear            # remove todos os stashes de uma vez
```

---

### Cascata/Efeitos

|Comando|O que acontece|
|---|---|
|`git stash`|Working directory limpo; estado empilhado em `stash@{0}`|
|`git stash pop`|Estado restaurado; entrada removida da pilha|
|`git stash apply`|Estado restaurado; entrada **permanece** na pilha|
|`git stash clear`|Pilha inteira apagada — sem recuperação|

> ⚠️ `git stash clear` é irreversível. Use `drop` para remover entradas individualmente com mais controle.