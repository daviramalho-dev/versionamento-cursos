### Definição: Git Restore

**`git restore`** descarta mudanças em arquivos do working directory ou remove arquivos do staging. É o comando "seguro" para voltar atrás — ele não reescreve histórico, apenas descarta mudanças locais que ainda não foram commitadas.

Pense nele como "desfazer edições" antes de oficializar no [[git commit]].

---

### Como Fazer

bash

```bash
# Descartar mudanças em um arquivo (volta para última versão commitada)
git restore arquivo.txt

# Descartar mudanças em vários arquivos
git restore arquivo1.txt arquivo2.txt

# Descartar mudanças em todos os arquivos
git restore .

# Remover arquivo do staging (oposto de git add)
git restore --staged arquivo.txt

# Remover vários do staging
git restore --staged .
```

---

### Exemplo 1: Desfazer Mudança Acidental

Você modificou um arquivo por engano e quer voltar:

bash

```bash
# Ver o que mudou
git status

# Arquivo aparece como "modified"
# Descartar mudança
git restore arquivo.txt

# Verifica
git status
# Arquivo sumiu da lista (voltou ao estado original)
```

---

### Exemplo 2: Remover do Staging Sem Descartar

Você adicionou um arquivo com [[git add]] mas ainda não quer commitar:

bash

```bash
# Adicionar arquivo
git add feature.js

# Ver status
git status
# Shows: "Changes to be committed: feature.js"

# Remover do staging (mas mantém o arquivo modificado)
git restore --staged feature.js

# Verifica
git status
# Shows: "Changes not staged for commit: feature.js"
# Arquivo ainda existe, só saiu do staging
```

---

### Quando Usar

Use `git restore` quando você quer **descartar mudanças locais** que ainda não foram commitadas. É seguro porque:

- Não afeta commits já feitos
- Não reescreve histórico
- Você pode reverter se mudar de ideia (enquanto não fecha o editor)

---

### Comparação: Restore vs Reset

|Comando|O quê faz|Quando usar|
|---|---|---|
|`git restore arquivo.txt`|Descarta mudanças no arquivo (working)|Erro em edição, quer voltar|
|`git restore --staged arquivo.txt`|Remove do staging, mantém mudanças|Adicionou errado com git add|
|`git reset arquivo.txt`|Remove do staging (efeito similar)|Desfazer git add|
|`git reset --hard`|