### Definição: Git Reset

**`git reset`** move a referência HEAD para um [[Commit]] anterior, descartando commits posteriores e mudanças. Ao contrário de [[git restore]], `git reset` **reescreve histórico** — use com cuidado. Existem 3 "modos" que afetam different levels (HEAD, staging, working).

---

### Como Fazer

bash

```bash
# Soft reset: volta ao commit, mantém mudanças no staging
git reset --soft HEAD~1

# Mixed reset: volta ao commit, mudanças ficam no working (padrão)
git reset --mixed HEAD~1

# Hard reset: volta ao commit, descarta TUDO (perigoso!)
git reset --hard HEAD~1

# Reset de arquivo específico (remove do staging)
git reset arquivo.txt

# Ver o que vai mudar (sem fazer)
git reset --soft HEAD~1 --dry-run
```

---

### Os 3 Modos

|Modo|O quê faz|Usa quando|
|---|---|---|
|`--soft`|Move HEAD, mantém staging e working|Quer reverter commit mas manter mudanças prontas|
|`--mixed` (padrão)|Move HEAD, descarta staging, mantém working|Quer descommitar mas manter trabalho local|
|`--hard`|Move HEAD, descarta TUDO|⚠️ Quer descartar commit e mudanças (cuidado!)|

---

### Exemplo 1: Reverter Último Commit (Soft)

Você commitou algo que não deveria ter:

bash

```bash
# Ver histórico
git log --oneline
# abc1234 Commit errado
# def5678 Commit anterior

# Soft reset: volta para def5678, mas mudanças ficam no staging
git reset --soft HEAD~1

# Verifica
git status
# Shows: "Changes to be committed: abc1234"
# Arquivo ainda existe, pronto para novo commit

# Pode agora refazer o commit com mensagem correta
git commit -m "Commit correto"
```

---

### Exemplo 2: Descartar Mudanças de Um Commit

Você fez mudanças que quer descartar completamente:

bash

```bash
# Hard reset: volta 1 commit, descarta tudo
git reset --hard HEAD~1

# Verifica
git log --oneline
# O commit anterior some do histórico
# Seu working está limpo
```

⚠️ **Cuidado:** Após `git reset --hard`, você **não consegue recuperar** facilmente. Use apenas se tiver certeza.

---

### Quando Usar vs Restore

**Use `git reset`** quando:

- Quer desfazer [[git commit]] (não apenas mudanças em arquivos)
- Precisa voltar a um [[Commit]] anterior específico
- Quer reescrever histórico (em branch local, antes de push)

**Use `git restore`** quando:

- Quer descartar mudanças em arquivos (antes de [[git commit]])
- Quer remover do staging sem descartar mudanças

---

### ⚠️ Nunca Reset Commits Já Enviados

bash

```bash
# NUNCA faça isso em commits já no servidor:
git reset --hard origin/main

# Quebra histórico para outras pessoas
# Se fez, avise o time e sincronizem
```