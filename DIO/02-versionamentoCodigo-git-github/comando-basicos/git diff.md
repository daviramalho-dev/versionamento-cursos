###  Definição: Git Diff

Compara estados do repositório e exibe as diferenças linha a linha. O output usa o formato **unified diff**: linhas com `-` são remoções, com `+` são adições, e o contexto neutro mostra onde a mudança ocorre.

bash

```bash
# Mudanças no working tree (não staged)
git diff

# Mudanças staged (prontas para commit)
git diff --staged        # ou --cached

# Diferença entre dois commits (usando [[Sha-1]])
git diff abc1234 def5678

# Diferença entre branch atual e outro branch
git diff main feature/login

# Diff de um arquivo específico
git diff HEAD -- src/app.js

# Só os nomes dos arquivos alterados (sem conteúdo)
git diff --name-only

# Estatística resumida
git diff --stat
```

#### Tabela de contextos

|Comando|O que compara|
|---|---|
|`git diff`|Working tree vs index (staged)|
|`git diff --staged`|Index vs último commit|
|`git diff HEAD`|Working tree vs último commit|
|`git diff branch-a branch-b`|Ponta de um branch vs outro|
|`git diff origin/main`|Local vs remote (após [[git fetch]])|

#### Lendo o output

diff

```diff
diff --git a/src/app.js b/src/app.js
index 3a1f2b..9c4d8e 100644
--- a/src/app.js
+++ b/src/app.js
@@ -12,7 +12,7 @@ function init() {
-  const timeout = 3000;
+  const timeout = 5000;
   startServer(timeout);
```

O cabeçalho `@@ -12,7 +12,7 @@` indica: a partir da linha 12, mostrando 7 linhas — antes e depois. O [[Sha-1]] abreviado (`3a1f2b..9c4d8e`) identifica os [[Blob]] comparados.