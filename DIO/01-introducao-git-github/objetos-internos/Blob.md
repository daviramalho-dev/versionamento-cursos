blob (Binary Large Obeject) - É um arquivo normal do seu projeto, mas identificado por seu SHA-1
Quando você faz `git add index.js`, o Git:

1. Lê o conteúdo do arquivo
2. Calcula o SHA-1 do conteúdo
3. Armazena como um blob no Git 

- Git NÃO duplica conteúdo idêntico
- Economiza espaço reutilizando blobs
- Cada mudança de conteúdo = novo blob

# EXEMPLO PRA FIXAR:


### ENTRADA 1: Criar + Add + Commit

```
video.mp4 (500MB)
└─ blob abc123... (novo) → +500MB no Git
```

### ENTRADA 2: Renomear + Add + Commit

```
meu_video.mp4 (mesmo conteúdo)
└─ blob abc123... (reutilizado) → +0MB no Git
```

### ENTRADA 3: Compactou + Add + Commit

```
meu_video.mp4 (450MB - comprimido)
└─ blob xyz789... (novo) → +450MB no Git
```

---

#### Resultado Final

##### Espaço total no Git

- **950MB** (ao invés de 1.45GB sem Git)

#### Histórico de commits

- ✓ **Commit 1** → blob `abc123...` (video.mp4)
- ✓ **Commit 2** → blob `abc123...` (meu_video.mp4) ← MESMO
- ✓ **Commit 3** → blob `xyz789...` (meu_video.mp4) ← NOVO

---

### 🎯 Lição Principal

|Situação|Resultado|
|---|---|
|Mesmo conteúdo|= mesmo blob = Git reutiliza|
|Conteúdo diferente|= novo blob = Git cria novo|

