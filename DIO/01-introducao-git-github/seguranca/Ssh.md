### Definição: SSH

SSH é um protocolo de autenticação por criptografia assimétrica. Você gera um par de chaves — a privada fica na sua máquina, a pública vai para o GitHub. A cada conexão, o GitHub verifica se sua chave privada corresponde à pública registrada. Nenhuma senha trafega pela rede.

É a alternativa recomendada ao [[Personal Access Token (https)]]: mais seguro e sem precisar gerenciar tokens.

---

### Como fazer

**1. Gerar o par de chaves**

```bash
ssh-keygen -t ed25519 -C "seu_email@example.com"
```

Gera dois arquivos em `~/.ssh/`:

- `id_ed25519` — chave privada, **nunca compartilhe**
- `id_ed25519.pub` — chave pública, vai para o GitHub

**2. Iniciar o agente e adicionar a chave**

```bash
eval "$(ssh-agent -s)"       # inicia o agente na memória
ssh-add ~/.ssh/id_ed25519    # adiciona a chave privada
```

O agente guarda a chave em memória para não precisar redigitar a passphrase.

**3. Registrar a chave pública no GitHub**

```bash
cat ~/.ssh/id_ed25519.pub    # copie a saída
```

Acesse `https://github.com/settings/keys` → _New SSH key_ → cole e salve.

**4. Verificar a conexão**

```bash
ssh -T git@github.com
# Hi seu_usuario! You've successfully authenticated...
```

**5. Configurar Git para usar SSH automaticamente**

```bash
git config --global url."git@github.com:".insteadOf "https://github.com/"
```

A partir disso, URLs HTTPS são substituídas por SSH automaticamente — `git clone https://github.com/...` passa a usar SSH sem precisar trocar o comando.

---

### Troubleshooting

|Erro|Causa|Solução|
|---|---|---|
|`Permission denied (publickey)`|Agente não está rodando ou chave não adicionada|`eval "$(ssh-agent -s)"` + `ssh-add ~/.ssh/id_ed25519`|
|`No such file or directory`|Par de chaves não existe|Rode `ssh-keygen` novamente|
|Git ainda pede senha|Chave tem passphrase e não está no agente|`ssh-add ~/.ssh/id_ed25519` e digite a passphrase|

```bash
ssh-add -l          # listar chaves ativas no agente
ls -la ~/.ssh/      # verificar se os arquivos existem
```

> ⚠️ Nunca compartilhe `id_ed25519`. Se a chave privada vazar, delete a chave pública no GitHub imediatamente e gere um novo par.