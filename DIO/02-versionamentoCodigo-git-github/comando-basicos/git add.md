### Definição: Git Add

**`git add`** prepara (stage) arquivos para serem incluídos no próximo [[git commit]]. É o passo entre modificar um arquivo e oficializar a mudança no histórico. Sem `git add`, o arquivo fica "modified" mas não entra no commit.

**Você pode adicionar um arquivo, vários, ou tudo de uma vez.**

Veja também: [[git status]] para verificar o estado antes de adicionar.

---

### Como Fazer

bash

```bash
# Adicionar um arquivo específico
git add arquivo.txt

# Adicionar vários arquivos
git add arquivo1.txt arquivo2.txt

# Adicionar todos os arquivos modificados
git add .

# Adicionar todos com padrão (ex: todos os .js)
git add *.js

# Adicionar interativamente (escolher cada mudança)
git add -p
```

---

### Por Quê Existe Esse Passo?

Git separa "modificar" de "commitar" propositalmente. Você pode trabalhar em vários arquivos, mas commitar apenas alguns. Isso dá controle fino — você não é forçado a commitar tudo.

**Exemplo:** Você mexeu em 5 arquivos, mas quer commitar só 2 porque os outros ainda estão em progresso.

bash

```bash
git add arquivo-pronto1.txt arquivo-pronto2.txt
git commit -m "feature x completa"

# Os outros 3 ficam modified, mas não no commit
```

---

### Exemplo 1: Adicionar Um Arquivo

bash

```bash
# Modificar
echo "mudança" > app.js

# Ver status
git status
# Mostra: modified: app.js (não staged)

# Adicionar
git add app.js

# Ver status novamente
git status
# Mostra: modified: app.js (staged, pronto para commit)
```

---

### Exemplo 2: Adicionar Seletivamente (-p)

bash

```bash
git add -p

# Git mostra cada mudança e pergunta:
# Stage this hunk? (y/n/...)
# Você escolhe qual mudança adicionar

# Útil quando um arquivo tem várias mudanças e você quer separar
```

---

### Exemplo 3: Desfazer um Add

Se você adicionou algo por engano:

bash

```bash
# Remove do staging (mas mantém as mudanças no arquivo)
git reset arquivo.txt

# Verifica
git status
# Mostra: arquivo.txt volta a "modified" (não staged)
```

---

### Cascata: O Que Happens After Add

```
Arquivo modificado
        ↓
git add
        ↓
Arquivo staged (pronto)
        ↓
git commit
        ↓
Entra no [[Commit]] no histórico
```