### Definição: git fetch

O [[git fetch]] baixa objetos e referências de um repositório remoto sem tocar no working tree ou na branch atual. É a metade segura do [[git pull]] — traz as informações, mas não as aplica.

Internamente, atualiza os ponteiros `refs/remotes/origin/*` e baixa os [[Blob]]s, [[Tree]]s e [[Snapshot]]s necessários para reconstruir os commits recebidos. Nenhum arquivo é alterado.

---

### Como fazer

```bash
git fetch                        # busca todas as atualizações do origin
git fetch upstream               # busca de um remote específico
git fetch origin main            # busca uma branch específica
git fetch --all                  # busca todos os remotes configurados
git fetch --prune                # remove refs locais de branches deletadas no remoto
```

---

### Fluxo seguro: fetch → inspecionar → integrar

O [[git pull]] equivale a `fetch` + `merge` em uma operação só. Usar `fetch` primeiro permite inspecionar o que chegou antes de integrar — essencial em times ou antes de merges complexos.

```bash
git fetch origin
git log HEAD..origin/main --oneline   # commits que chegaram
git diff HEAD origin/main             # o que mudou nos arquivos
git merge origin/main                 # integra só quando quiser
```

---

### Cascata/Efeitos

|Comando|O que acontece|
|---|---|
|`git fetch`|Atualiza `refs/remotes/origin/*`; working tree intacto|
|`git fetch --prune`|Remove ponteiros locais de branches que não existem mais no remoto|
|`git pull`|`fetch` + [[git merge]] automático — sem chance de inspecionar antes|

> 💡 Prefira `fetch` quando não tem certeza do que está chegando. Use `pull` só quando o merge é trivial e você já sabe o que esperar.