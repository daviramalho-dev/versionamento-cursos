### Definição: Git Fetch

Baixa objetos e referências de um repositório remoto **sem modificar o working tree ou o branch atual**. É a metade segura do [[git pull]] — ele traz as informações, mas não as aplica.

Internamente, `git fetch` atualiza os ponteiros `refs/remotes/origin/*` e baixa os [[Blob]], [[Tree]] e [[Snapshot]] necessários para reconstruir os commits recebidos. Nenhum arquivo é alterado.

bash

```bash
# Busca todas as atualizações do remote padrão (origin)
git fetch

# Busca de um remote específico
git fetch upstream

# Busca um branch específico
git fetch origin main

# Busca todos os remotes configurados
git fetch --all

# Remove referências locais a branches deletados no remote
git fetch --prune
```

**Por que usar `fetch` antes de `pull`?** O [[git pull]] equivale a `fetch` + `merge` em uma única operação. Usar `fetch` primeiro permite inspecionar as mudanças com [[git diff]] antes de integrá-las — essencial em times ou antes de merges complexos.

bash

```bash
# Fluxo seguro: buscar → inspecionar → integrar
git fetch origin
git log HEAD..origin/main --oneline   # o que chegou
git diff HEAD origin/main             # o que mudou
git merge origin/main                 # agora sim
```