### Definição: Git Push

**`git push`** envia seus [[Commit]] locais para o repositório remoto (servidor). É a forma de compartilhar seu trabalho com o time — sem push, seus commits ficam apenas na sua máquina.

Push conecta ao [[git remote]] configurado (geralmente `origin`) e sincroniza o histórico.

---

### Como Fazer

bash

```bash
# Push do branch atual para origin
git push

# Push explícito (nome do remote + branch)
git push origin main

# Push de um branch específico
git push origin feature-x

# Push forçado (sobrescreve histórico remoto - cuidado!)
git push --force

# Push com rastreamento automático (primeira vez)
git push -u origin branch-novo
```

---

### Exemplo 1: Push Básico

Você fez [[git commit]] e quer enviar para o servidor:

bash

```bash
# Verificar se há mudanças
git status

# Fazer commits
git add arquivo.js
git commit -m "Add nova funcionalidade"

# Enviar para origin
git push

# Ou explícito
git push origin main
```

---

### Exemplo 2: Push de Novo Branch

Você criou um branch local e quer enviá-lo:

bash

```bash
git checkout -b feature-login

# Fazer edições e commits
git add .
git commit -m "Implement login form"

# Enviar e rastrear automaticamente
git push -u origin feature-login

# Próximos push nesse branch não precisam de -u
git push
```

---

### Quando Usar

Use `git push` quando você quer **compartilhar commits** com o time. Normalmente acontece após [[git commit]] e antes de pedir code review (Pull Request).

⚠️ **Nunca use `git push --force`** em branches compartilhados — quebra histórico para outros. Só use em branches pessoais.

---

### Troubleshooting

|Problema|Causa|Solução|
|---|---|---|
|`fatal: No configured push destination`|Remote não configurado|`git push origin branch` (explícito)|
|`Permission denied`|Sem acesso ao servidor|Verifique [[Ssh]] ou [[Personal Access Token (https)]]|
|`rejected: updates were rejected`|Servidor tem commits novos|Faça [[git pull]] primeiro|
|`fatal: The current branch has no upstream`|Branch sem rastreamento|Use `git push -u origin branch-novo`|