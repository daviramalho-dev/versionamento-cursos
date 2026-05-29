### Definição: Tree

Tree é como o Git representa um diretório. Ela armazena referências para [[Blob]]s (arquivos) e outras Trees (subdiretórios), identificada pelo [[Sha-1]] calculado a partir do seu conteúdo interno. Quando qualquer filho muda, a Tree recebe um novo [[Sha-1]] — e essa mudança propaga para cima até o [[Commit]].

---

### Estrutura em cascata

Considere este projeto e três commits:

```
seu_projeto/
├─ index.js
├─ package.json
└─ src/
   └─ app.js
```

**Commit 1 — estrutura inicial**

```
Tree raiz  (root123)
├─ Blob index.js      (abc111)
├─ Blob package.json  (def222)
└─ Tree src           (src333)
   └─ Blob app.js     (ghi444)
```

**Commit 2 — renomear index.js → main.js**

```
Tree raiz  (root456) ← nova (estrutura mudou)
├─ Blob main.js       (abc111) ← mesmo blob
├─ Blob package.json  (def222)
└─ Tree src           (src333) ← reutilizada
   └─ Blob app.js     (ghi444)
```

**Commit 3 — editar app.js**

```
Tree raiz  (root789) ← nova (src mudou)
├─ Blob main.js       (abc111)
├─ Blob package.json  (def222)
└─ Tree src           (src999) ← nova (blob filho mudou)
   └─ Blob app.js     (jkl777) ← novo blob
```

---

### Cascata/Efeitos

|Situação|O que muda|
|---|---|
|Editar arquivo em subpasta|Novo [[Blob]] → nova Tree da pasta → nova Tree raiz|
|Renomear arquivo|Nova Tree raiz; Trees internas sem alteração|
|Editar arquivo na raiz|Apenas nova Tree raiz|
|Nada muda|Mesma Tree — Git reutiliza sem custo|

A propagação sempre sobe: [[Blob]] → Tree da pasta → Tree raiz → [[Commit]]. Apenas o caminho afetado gera objetos novos; o restante é reaproveitado.