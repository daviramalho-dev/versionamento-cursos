
**TREE** - É uma pasta/diretório do seu projeto, mas identificada por seu [[Sha-1]] Quando você faz  [[git add]] o Git:

1. Cria [[Blob]] para cada arquivo
2. Calcula o [[Sha-1]] da estrutura (o que tem dentro)
3. Armazena como uma TREE no Git

- TREE muda quando conteúdo interno muda
- TREE tem [[Sha-1]] próprio baseado nos [[Blob]] que contém
- Cada mudança de arquivo = TREE diferente


## EXEMPLO PRA FIXAR:

Seu projeto:

```
seu_projeto/
├─ index.js
├─ package.json
└─ src/
   └─ app.js
```

### ENTRADA 1: Criar estrutura + Add + Commit

```
TREE raiz root123...
├─ BLOB index.js (abc111...)
├─ BLOB package.json (def222...)
└─ TREE src (src333...)
   └─ BLOB app.js (ghi444...)

└─ TREE root123... (nova) → +X no Git
└─ TREE src333... (nova) → +X no Git
```

### ENTRADA 2: Renomear arquivo + Add + Commit

```
Você renomeia: index.js → main.js (conteúdo igual)

TREE raiz root456...  ← NOVO! (estrutura mudou)
├─ BLOB main.js (abc111...) ← MESMO BLOB!
├─ BLOB package.json (def222...)
└─ TREE src (src333...) ← MANTÉM IGUAL
   └─ BLOB app.js (ghi444...)

└─ TREE root456... (novo) → +X no Git
└─ TREE src333... (reutilizado) → +0 no Git
```

### ENTRADA 3: Editar app.js + Add + Commit

```
Você edita: app.js (conteúdo diferente)

TREE raiz root789...  ← NOVO! (porque src mudou)
├─ BLOB main.js (abc111...)
├─ BLOB package.json (def222...)
└─ TREE src (src999...) ← NOVO! (app.js mudou)
   └─ BLOB app.js (jkl777...) ← NOVO BLOB!

└─ TREE root789... (novo) → +X no Git
└─ TREE src999... (novo) → +X no Git
```

---

## Resultado Final

### Histórico de TREEs

- ✓ **Commit 1** → TREE `root123...` (estrutura original)
- ✓ **Commit 2** → TREE `root456...` (renomeou index.js) ← NOVA TREE RAIZ
- ✓ **Commit 3** → TREE `root789...` (editou app.js) ← NOVA TREE RAIZ

### O Cascata de Mudanças

```
Você edita: app.js

├─ BLOB app.js muda
│  └─ TREE src/ muda (porque contém app.js)
│     └─ TREE raiz/ muda (porque contém src/)
│        └─ COMMIT muda (porque aponta pra nova raiz)
```

---

## 🎯 Lição Principal

|Situação|Resultado|
|---|---|
|Renomear arquivo|TREE raiz muda, TREE src mantém|
|Editar arquivo em pasta|TREE dessa pasta muda + TREE raiz muda|
|Editar arquivo na raiz|Apenas TREE raiz muda|
|Nada muda|Mesma TREE = Git reutiliza|
