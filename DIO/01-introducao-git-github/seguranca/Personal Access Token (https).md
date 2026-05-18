**Personal Access Token** - Chave de acesso alternativa à senha para autenticar com GitHub via HTTPS.

## Quando usar?

- Você usa HTTPS para clonar (não SSH)
- Git pede autenticação no push/pull
- Você tá em máquina compartilhada/temporária

**Melhor alternativa:** Use SSH! (mais seguro)

---

## Passo 1: Gerar Token no GitHub

1. Acesse: https://github.com/settings/tokens
2. Clique em **"Generate new token"** → **"Generate new token (classic)"**
3. Dê um nome (ex: "Meu Computador")
4. Selecione **"repo"** (permissão completa para repos)
5. Clique em **"Generate token"** na base
6. **Copia o token** (aparece uma única vez!)

---

## Passo 2: Usar no Git

Quando Git pedir autenticação:

```bash
Username: seu-usuario-github
Password: cole-aqui-o-token-completo
```

---

## Passo 3: Git Lembrar o Token (Opcional)

Para não digitar toda vez:

```bash
git config --global credential.helper store
```

⚠️ **Aviso:** Armazena token em texto plano. Use apenas em máquina pessoal!

---

## Verificar Token Armazenado

```bash
cat ~/.git-credentials
```

Mostra tokens salvos (não compartilhe!)

---

## Renovar Token

Tokens expiram! Quando expirar:

1. https://github.com/settings/tokens
2. Clique no token expirado
3. Clique em **"Regenerate token"**
4. Copia o novo token
5. Usa no Git normalmente

---

## Revogar Token (Segurança)

Se vazar ou não usar mais:

1. https://github.com/settings/tokens
2. Encontre o token
3. Clique em **"Delete"**

Pronto! Não funciona mais.
