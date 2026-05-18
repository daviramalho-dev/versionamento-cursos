**SSH** - Protocolo de segurança que usa criptografia para comunicação segura com GitHub.

## Como Funciona

```
Você                          GitHub
(Chave Privada)      ←→       (Chave Pública)
  secreta                       registrada
```

GitHub verifica: chave privada combina com pública? ✅ Então é você!

---

## Passo 1: Gerar o Par de Chaves

```bash
ssh-keygen -t ed25519 -C "seu_email@example.com"
```

**O que acontece:**

- Pede para confirmar local (pressione Enter)
- Pede passphrase (senha da chave - deixe vazio ou coloque)
- Cria 2 arquivos:
    - `~/.ssh/id_ed25519` (chave privada - SECRETA!)
    - `~/.ssh/id_ed25519.pub` (chave pública - compartilha)
    - ambos em um lugar qeu vai ser falado mas normalmente em .ssh

---

## Passo 2: Iniciar SSH Agent

```bash
eval "$(ssh-agent -s)"
```

**O que faz:**

- Inicia programa que guarda sua chave na memória
- Não precisa digitar senha toda vez

---

## Passo 3: Adicionar Chave Privada ao Agent

```bash
ssh-add ~/.ssh/id_ed25519
```

**Pronto!** Sua chave privada agora está no Agent.

---

## Passo 4: Copiar Chave Pública

```bash
cat ~/.ssh/id_ed25519.pub
```

Copia a saída (começa com `ssh-ed25519...`)

---

## Passo 5: Adicionar no GitHub

1. Acesse: https://github.com/settings/keys
2. Clique em **"New SSH key"**
3. Dê um título (ex: "Meu Computador")
4. **Cole** a chave pública (a que você copiou)
5. Clique em **"Add SSH key"**

**GitHub pedirá sua senha - digite e confirme**

---

## Passo 6: Verificar Conexão

```bash
ssh -T git@github.com
```

**Se funcionar, mostra:**

```
Hi seu_usuario! You've successfully authenticated...
```

---

## Passo 7: Configurar Git para Usar SSH
 
**Por que:** Quando você clonar repositórios, Git usa HTTPS por padrão. Precisa configurar para usar SSH.
 
### Opção A: Configuração Global (recomendado)
 
```bash
git config --global url."git@github.com:".insteadOf "https://github.com/"
```
**insteadOf **Substituição automática HTTPS → SSH

**O que faz:** Sempre que Git ver `https://github.com/`, substitui por `git@github.com:`
 
### Opção B: Verificar Configuração
 
```bash
git config --global --list
```
 
Procure por: `url.git@github.com:.insteadof=https://github.com/`
 
---
 
## Passo 8: Clonar Repositório com SSH
 
### Quando você clona um repo no GitHub
 
Tem dois formatos:
 
**HTTPS** (padrão):
```bash
git clone https://github.com/usuario/repo.git
```
❌ Pede senha toda vez que push/pull
 
**SSH** (com chave):
```bash
git clone git@github.com:usuario/repo.git
```
 Usa sua chave privada automaticamente
 
### Qual usar?
 
Se configurou SSH corretamente, ambas funcionam. Mas SSH é:
- Mais seguro
- Não pede senha
- Recomendado
---
 
## Passo 9: Fluxo de Uso Diário
 
Depois de tudo configurado, seu fluxo fica:
 
```bash
# 1. Clone (SSH automático)
git clone git@github.com:usuario/repo.git
 
# 2. Entre na pasta
cd repo
 
# 3. Faça mudanças
echo "código novo" > app.js
 
# 4. Commit (normal)
git add .
git commit -m "Adicionar feature"
 
# 5. Push (usa SSH automaticamente!)
git push
```
 
Sem pedir senha! 
 
---
 
## Troubleshooting
 
### Erro 1: "Permission denied (publickey)"
 
**Significado:** SSH Agent não está rodando ou chave não foi adicionada.
 
**Solução:**
 
```bash
# Verifique quais chaves estão ativas
ssh-add -l
 
# Se vazio ou erro, reinicie tudo
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
 
# Teste novamente
ssh -T git@github.com
```
 
### Erro 2: "No such file or directory"
 
**Significado:** As chaves SSH não foram criadas.
 
**Solução:**
 
Verifique se existem:
```bash
ls -la ~/.ssh/
```
 
Deve mostrar:
```
-rw------- id_ed25519       (chave privada)
-rw-r--r-- id_ed25519.pub   (chave pública)
```
 
Se não tiver, crie novamente:
```bash
ssh-keygen -t ed25519 -C "seu_email@example.com"
```
 
### Erro 3: "git@github.com: command not found"
 
**Significado:** Git não reconhece formato SSH.
 
**Solução:** Verifique a configuração:
```bash
git config --global url."git@github.com:".insteadOf "https://github.com/"
```
 
Se não ajudar, use o comando completo:
```bash
git clone git@github.com:usuario/repo.git
```
 
### Erro 4: SSH funciona mas Git ainda pede senha
 
**Significado:** Você tem passphrase na chave e pode ser necessário ativar no Agent.
 
**Solução:**
 
```bash
# Ative com passphrase
ssh-add ~/.ssh/id_ed25519
# Digita a passphrase
 
# Verifique
ssh-add -l
```
 
