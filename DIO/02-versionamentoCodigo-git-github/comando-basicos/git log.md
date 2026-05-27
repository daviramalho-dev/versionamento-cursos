### Definição: Git Log

**`git log`** mostra o histórico de commits — quem fez o quê, quando, e por quê. Cada commit tem um [[Sha-1]] único (identificador), autor, data e mensagem. Use [[git log]] para navegar, pesquisar e entender a evolução do projeto.

---

### Como Fazer

bash

```bash
# Ver histórico completo
git log

# Ver resumido (uma linha por commit)
git log --oneline

# Ver últimos 5 commits
git log -5

# Ver com gráfico de branches
git log --graph --oneline --all

# Ver commits de um arquivo específico
git log -- arquivo.txt

# Ver commits por autor
git log --author="Nome"

# Pesquisar por mensagem
git log --grep="bugfix"
```

**Saída típica:**

```
commit a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6
Author: Maria Silva <maria@email.com>
Date:   Wed May 27 10:30:00 2026 -0300

    Fix bug no login

commit z9y8x7w6v5u4t3s2r1q0p9o8n7m6l5k4
Author: João Santos <joao@email.com>
Date:   Tue May 26 15:20:00 2026 -0300

    Add nova feature
```

---

### Exemplo 1: Ver Histórico Básico

bash

```bash
# Completo
git log

# Resumido (mais útil para navegar)
git log --oneline

# Saída:
# a1b2c3d Fix bug no login
# z9y8x7w Add nova feature
# p9o8n7m Initial commit
```

---

### Exemplo 2: Ver Commits de Um Arquivo

Quando você quer entender a evolução de um arquivo específico, use [[git log]] com o arquivo como filtro. Combine com [[git add]] e [[git commit]] para ver o histórico completo de mudanças.

bash

```bash
git log -- app.js

# Mostra apenas commits que modificaram app.js
```

---

### Exemplo 3: Pesquisar por Autor ou Mensagem

bash

```bash
# Commits de uma pessoa
git log --author="Maria"

# Commits com "bugfix" na mensagem
git log --grep="bugfix"

# Combinar filtros
git log --author="Maria" --grep="fix" --oneline
```

---

### Exemplo 4: Visualizar com Gráfico

Para entender fluxo de branches:

bash

```bash
git log --graph --oneline --all

# Saída:
# * a1b2c3d (HEAD -> main) Fix bug
# | * z9y8x7w (develop) Add feature
# |/
# * p9o8n7m Initial commit
```

---

### Por Quê É Importante

`git log` não apenas mostra histórico — você usa ele para entender a evolução do projeto. Com [[git log]], você pode encontrar quando um bug foi introduzido, entender decisões passadas, e auditar mudanças. Combine com [[git commit]] para criar um histórico limpo e bem documentado.