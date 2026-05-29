### Definição: Parente (pai)

Pai é a referência que cada [[Commit]] carrega apontando para o commit anterior. Essa ligação forma a cadeia do histórico — cada novo commit sabe de onde veio, criando uma linha contínua e rastreável de mudanças.

O primeiro commit de um repositório não tem pai. Todos os outros têm exatamente um (ou mais, no caso de um merge).

```
Commit 1  ← sem pai (raiz)
   ↓
Commit 2  ← pai: Commit 1
   ↓
Commit 3  ← pai: Commit 2
   ↓
Commit 4  ← pai: Commit 3
```

---

### Por que importa

A referência ao pai é o que torna o [[git log]] possível — o Git percorre a cadeia de pais do [[HEAD]] até a raiz para montar o histórico. É também a base de [[git reset]] (voltar para um commit anterior) e [[git merge]] (unir duas cadeias com pais diferentes).

Branches são ponteiros que avançam sobre essa cadeia. Quando duas branches divergem e depois fazem merge, o commit resultante tem **dois pais** — um de cada branch.

---

### Cascata/Efeitos

|Situação|Número de pais|
|---|---|
|Primeiro commit do repositório|0|
|Commit normal|1|
|Commit de merge|2 ou mais|

> 💡 Como cada commit referencia seu pai pelo [[Sha-1]], qualquer alteração retroativa no histórico quebra a cadeia — o hash do pai não bate mais. É assim que o Git garante integridade.