### Definição: Ciclo de Vida dos Arquivos

Todo arquivo em um repositório Git passa por 4 estados. Entender onde cada arquivo está é o que permite organizar commits com precisão — e corrigir erros antes de eles virarem histórico.

|Estado|O que é|Commitável?|
|---|---|---|
|**Untracked**|Git desconhece o arquivo|❌|
|**Unmodified**|Rastreado, sem mudanças|—|
|**Modified**|Alterado, não preparado|❌|
|**Staged**|Preparado para commit|✅|

Ao commitar, o Git calcula o [[Sha-1]] de cada [[Blob]] (arquivo), monta uma [[Tree]] com a estrutura do projeto e cria um [[Commit]] apontando para ela.

---

### Como fazer

**Untracked → Staged** (arquivo novo)

bash

```bash
git add main.js   # arquivo específico
git add .         # todos de uma vez
```

**Unmodified → Modified → Staged** (arquivo editado)

bash

```bash
git status              # ver o que mudou
git diff main.js        # ver as mudanças antes de adicionar
git add main.js         # preparar para commit
git diff --staged       # confirmar o que será commitado
git add -p main.js      # adicionar hunk por hunk — útil para separar commits
```

**Staged → Commit**

bash

```bash
git commit -m "Refatora validação de email"
```

Após o commit, o arquivo volta a **Unmodified** até a próxima edição.

---

### Quando usar `git add -p`

O `-p` mostra cada bloco de mudança individualmente e pergunta se você quer incluir. É a ferramenta certa quando você trabalhou em coisas distintas — bug fix, feature e docs ao mesmo tempo — e quer dividir em commits separados e legíveis. Um `git add .` jogaria tudo num commit só.

---

### Cascata/Efeitos

|Ação|Transição|
|---|---|
|Criar arquivo|→ Untracked|
|`git add`|Untracked / Modified → Staged|
|`git commit`|Staged → Unmodified|
|Editar arquivo rastreado|Unmodified → Modified|
|`git restore --staged`|Staged → Modified / Untracked|

> 💡 Quando em dúvida, [[git status]]. Ele sempre diz onde você está no ciclo e o que fazer a seguir.