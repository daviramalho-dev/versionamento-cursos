### Definição: Commit (objeto interno)

> Esta nota descreve o **commit como objeto interno do Git** — diferente de [[git commit]], que é o comando. Raramente você interage com isso diretamente, mas entender a estrutura explica por que o Git funciona como funciona.

Commit é um [[Snapshot]] do projeto inteiro. Internamente, ele armazena metadados (autor, data, mensagem) e aponta para uma [[Tree]] raiz — que por sua vez aponta para [[Blob]]s e outras Trees. Cada commit tem seu próprio [[Sha-1]] e carrega a referência do commit anterior ([[Parente (pai)]]), formando a cadeia do histórico.

---

### Estrutura em cascata

Três commits mostrando como objetos são reutilizados ou recriados:

**Commit 1 — estrutura inicial**

```
COMMIT abc000
└─ Tree root123
   ├─ Blob index.js  (abc111)
   └─ Tree src       (src333)
      └─ Blob app.js (ghi444)
```

**Commit 2 — renomear index.js → main.js**

```
COMMIT def000         ← novo
└─ Tree root456       ← nova (filho mudou)
   ├─ Blob main.js    (abc111) ← mesmo blob
   └─ Tree src        (src333) ← mesma tree
      └─ Blob app.js  (ghi444)
Pai: abc000
```

**Commit 3 — editar app.js**

```
COMMIT ghi000         ← novo
└─ Tree root789       ← nova
   ├─ Blob main.js    (abc111)
   └─ Tree src        (src999) ← nova (blob filho mudou)
      └─ Blob app.js  (jkl777) ← novo blob
Pai: def000
```

Apenas o que mudou gera objetos novos. O restante é reaproveitado.

---

### Comandos para inspecionar

bash

```bash
git log                # histórico completo
git log --oneline      # histórico com SHA abreviado
git show <SHA>         # detalhes de um commit
git rev-parse HEAD     # SHA do commit mais recente
```

---

### Cascata/Efeitos

|Objeto|O que representa|Novo SHA quando|
|---|---|---|
|[[Blob]]|Conteúdo de um arquivo|Conteúdo muda|
|[[Tree]]|Estrutura de um diretório|Qualquer filho muda|
|Commit|[[Snapshot]] completo|Você executa [[git commit]]|

A cadeia é sempre: `Commit → Tree → Blob / Tree → Blob...` Uma mudança num [[Blob]] força novos [[Sha-1]] em toda a cadeia acima dele até o commit.