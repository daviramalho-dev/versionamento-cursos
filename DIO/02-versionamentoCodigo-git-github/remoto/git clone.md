### Definição: Git Clone

**`git clone`** copia um repositório remoto inteiro para sua máquina — histórico completo, branches e configuração automática do remote `origin`.

Internamente, Git cria o diretório local, baixa todos os commits e objetos ([[Blob]], [[Tree]], [[Snapshot]]), configura o [[git remote]] `origin` apontando para a URL de origem e faz checkout automático do branch padrão (geralmente `main`).

---

### Como Fazer

bash

```bash
# Clonar via HTTPS
git clone https://github.com/usuario/repositorio.git

# Clonar via SSH (sem senha após configurar chave [[Ssh]])
git clone git@github.com:usuario/repositorio.git

# Clonar com nome de pasta customizado
git clone https://github.com/usuario/repositorio.git meu-projeto
```

Após clonar, verifique o remote configurado automaticamente:

bash

```bash
cd repositorio
git remote -v
# origin  https://github.com/usuario/repositorio.git (fetch)
# origin  https://github.com/usuario/repositorio.git (push)
```

---

### Opções Úteis

#### Clonar um branch específico

Por padrão, `git clone` baixa todos os branches mas faz checkout apenas do padrão. Para iniciar direto em outro branch:

bash

```bash
git clone -b nome-do-branch https://github.com/usuario/repositorio.git

# Exemplo: clonar e entrar direto na branch de desenvolvimento
git clone -b develop git@github.com:usuario/repositorio.git
```

O histórico completo ainda é baixado — o `-b` apenas define qual branch recebe o checkout inicial.

#### Shallow clone (histórico parcial)

Útil quando o repositório tem histórico longo e você só precisa do estado atual — pipelines de CI, por exemplo:

bash

```bash
# Baixa apenas o último commit (sem histórico)
git clone --depth 1 https://github.com/usuario/repositorio.git

# Baixa os últimos N commits
git clone --depth 10 https://github.com/usuario/repositorio.git

# Shallow de um branch específico
git clone --depth 1 -b main https://github.com/usuario/repositorio.git
```

> ☐ Shallow clones não trazem o histórico completo — comandos como `git log` e `git blame` mostrarão menos informação. Para "aprofundar" depois: `git fetch --unshallow`.

#### Clonar apenas um branch (sem os outros)

Se quiser economizar espaço e ignorar todos os outros branches:

bash

```bash
git clone --single-branch -b develop https://github.com/usuario/repositorio.git
```

Combinado com `--depth 1`, é a forma mais leve de clonar:

bash

```bash
git clone --depth 1 --single-branch -b main https://github.com/usuario/repositorio.git
```

---

### Tabela Comparativa

|Situação|Comando|
|---|---|
|Clone padrão completo|`git clone <url>`|
|Entrar direto em outro branch|`git clone -b <branch> <url>`|
|Repositório muito grande, só precisa do estado atual|`git clone --depth 1 <url>`|
|CI/CD pipeline|`git clone --depth 1 --single-branch -b main <url>`|
|Trocar de HTTPS para SSH depois|`git remote set-url origin <nova-url>`|

---

### Troubleshooting

|Problema|Solução|
|---|---|
|`fatal: could not read Username`|Use [[Ssh]] ou reconfigure credenciais com [[Personal Access Token (https)]]|
|`Repository not found`|URL incorreta ou repositório privado sem acesso|
|`warning: You appear to have cloned an empty repository`|O repositório existe mas não tem commits ainda — comportamento normal|
|Branch clonado não aparece localmente|Use `git branch -a` para ver branches remotos; `git checkout nome-do-branch` para criar o local|
|Quer mudar a URL do remote depois|`git remote set-url origin <nova-url>`|