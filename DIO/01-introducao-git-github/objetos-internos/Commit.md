**COMMIT** - [[Snapshot]] do seu projeto inteiro. Aponta para uma [[Tree]] raiz, que por sua vez aponta para [[Blob]]s.

Quando você faz `git commit -m "mensagem"`, o Git:
1. Pega a [[Tree]] raiz atual
2. Cria um objeto commit com metadados
3. Armazena o [[Sha-1]] do commit

- COMMIT tem [[Sha-1]] próprio (identificação única)
- COMMIT aponta para uma [[Tree]]
- Cada novo commit = novo [[Sha-1]]

---

## EXEMPLO PRA FIXAR:

### ENTRADA 1: Criar estrutura + Commit
```
COMMIT abc000...
└─ Tree root123...
   ├─ Blob index.js (abc111...)
   └─ Tree src (src333...)
      └─ Blob app.js (ghi444...)
```

### ENTRADA 2: Renomear arquivo + Commit
```
COMMIT def000... ← NOVO!
└─ Tree root456... ← NOVA!
   ├─ Blob main.js (abc111...) ← MESMO BLOB
   └─ Tree src (src333...) ← MESMA TREE
      └─ Blob app.js (ghi444...)

Pai: abc000...
```

### ENTRADA 3: Editar app.js + Commit
```
COMMIT ghi000... ← NOVO!
└─ Tree root789... ← NOVA!
   ├─ Blob main.js (abc111...)
   └─ Tree src (src999...) ← NOVA!
      └─ Blob app.js (jkl777...) ← NOVO BLOB!

Pai: def000...
```

---

## Histórico

- ✓ **Commit abc000...** → Tree root123...
- ✓ **Commit def000...** → Tree root456... ([[Parente (pai)]]: abc000)
- ✓ **Commit ghi000...** → Tree root789... ([[Parente (pai)]]: def000)

---

## Conexão Completa

```
COMMIT → Tree → Blob/Tree → Blob/Tree...
```

---

## Comandos

```bash
git log                 # Todos os commits
git log --oneline       # Commits abreviados
git show <SHA>          # Detalhes de um commit
git rev-parse HEAD      # SHA do último commit
```

---

## Diferenças

| Conceito | O quê | Muda quando |
|----------|-------|------------|
| **[[Blob]]** | Arquivo | Conteúdo muda |
| **[[Tree]]** | Pasta | [[Blob]] ou [[Tree]] interna muda |
| **COMMIT** | [[Snapshot]] | Você faz commit |