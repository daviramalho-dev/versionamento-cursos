### Definição: Personal Access Token (HTTPS)

Personal Access Token (PAT) é uma chave de acesso que substitui a senha do GitHub na autenticação via HTTPS. O GitHub removeu o suporte a senha convencional — hoje, push e pull via HTTPS exigem um token.

> 💡 Se possível, prefira [[Ssh]] — mais seguro e sem necessidade de gerenciar tokens.

---

### Como fazer

**1. Gerar o token no GitHub**

Acesse `https://github.com/settings/tokens` → _Generate new token (classic)_, dê um nome descritivo, marque a permissão `repo` e clique em _Generate token_.

⚠️ O token aparece **uma única vez**. Copie antes de sair da página.

**2. Usar no Git**

Quando o Git pedir autenticação:

```bash
Username: seu-usuario-github
Password: cole-o-token-aqui   # não sua senha — o token
```

**3. Salvar para não digitar toda vez**

```bash
git config --global credential.helper store
```

Armazena o token em texto plano em `~/.git-credentials`. Use apenas em máquina pessoal.

```bash
cat ~/.git-credentials   # ver tokens salvos
```

---

### Manutenção

**Renovar token expirado:** acesse `https://github.com/settings/tokens`, clique no token → _Regenerate token_, copie o novo valor e use normalmente no próximo push.

**Revogar token comprometido:** mesmo caminho → _Delete_. O token para de funcionar imediatamente.

---

### Cascata/Efeitos

|Ação|Resultado|
|---|---|
|`credential.helper store`|Token salvo em texto plano em `~/.git-credentials`|
|Token expirado|Push/pull falha com erro de autenticação — gere um novo|
|Token vazado|Revogue imediatamente em `github.com/settings/tokens`|

> ⚠️ Nunca compartilhe o arquivo `~/.git-credentials` nem commite tokens em repositórios.