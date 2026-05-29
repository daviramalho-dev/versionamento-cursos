### Definição: Git Stash
Salva temporariamente mudanças não commitadas (working tree e index) em uma pilha interna, retornando o repositório ao estado do último [[git commit]]. Útil quando você precisa trocar de contexto sem perder trabalho em andamento e sem criar um commit prematuro.

O stash armazena as mudanças como um commit especial em `refs/stash`, estruturado com [[Tree]] e [[Parente (pai)]] para permitir reaplicação posterior.

bash

```bash
# Salva o estado atual
git stash

# Com mensagem descritiva (recomendado)
git stash push -m "WIP: ajuste no timeout de conexão"

# Inclui arquivos untracked (novos arquivos não adicionados)
git stash push -u

# Lista todos os stashes
git stash list

# Aplica o stash mais recente (mantém na pilha)
git stash apply

# Aplica e remove da pilha
git stash pop

# Aplica um stash específico
git stash apply stash@{2}

# Remove um stash específico
git stash drop stash@{1}

# Remove todos os stashes
git stash clear
```

#### Fluxo típico

bash

```bash
# Situação: você está no meio de uma feature e precisa corrigir um bug urgente

git stash push -m "WIP: nova tela de login"
git checkout main
git checkout -b hotfix/timeout

# ... faz a correção, commita e faz merge ...

git checkout feature/login
git stash pop           # restaura exatamente onde parou
```

#### Troubleshooting

**Conflito ao aplicar stash** Se o stash conflitar com mudanças atuais, o Git marca os conflitos no arquivo e o stash **não** é removido automaticamente (mesmo com `pop`). Resolva os conflitos, faça `git add` e então `git stash drop` manualmente.

**Arquivos novos não foram salvos** Arquivos _untracked_ (que nunca passaram pelo [[git add]]) são ignorados por padrão. Use `git stash push -u` para incluí-los.

**Perdi um stash com `clear`** Os objetos ainda existem no repositório por um tempo. Use [[git reflog]] para localizar:

bash

```bash
git fsck --unreachable | grep commit
git show <sha>   # inspeciona o conteúdo
```