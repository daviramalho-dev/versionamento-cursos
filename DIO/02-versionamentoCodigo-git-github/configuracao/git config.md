### Definição: git config

O `git config` gerencia as configurações do Git em três níveis hierárquicos. Cada nível tem escopo e arquivo próprios — e o mais específico sempre vence.

|Nível|Flag|Escopo|Arquivo|
|---|---|---|---|
|Sistema|`--system`|Toda a máquina, todos os usuários|`/etc/gitconfig`|
|Usuário|`--global`|Seu usuário do SO, qualquer repo|`~/.gitconfig`|
|Local|`--local`|Um repositório específico|`.git/config`|

Ordem de precedência: `sistema → usuário → local`. Se `user.name` está definido em `--global` e também em `--local`, o Git usa o valor local naquele repositório.

---

### Quando usar cada nível

`--global` é o mais usado no dia a dia — identidade, editor padrão, aliases, tudo que se aplica a todos os seus projetos.

`--local` quando um projeto precisa de configuração diferente: email corporativo num repo de trabalho, ou identidade específica num repo de demonstração.

`--system` é raro. Requer permissão administrativa e afeta todos os usuários da máquina.

---

### Como fazer

```bash
# Configurações essenciais (--global)
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
git config --global core.editor "code --wait"   # VS Code

# Inspecionar
git config --list                   # todas as configs ativas
git config --list --show-origin     # mostra de qual arquivo cada valor vem
git config user.email               # ver valor específico

# Editar arquivo diretamente
git config --global --edit
git config --local --edit
```

---

### Cascata/Efeitos

|Ação|Impacto|
|---|---|
|Alterar `--global`|Todos os repos da máquina, presentes e futuros|
|Alterar `--local`|Apenas o repo atual (`.git/config`)|
|Alterar `--system`|Todos os usuários e repos — requer `sudo`|

> ⚠️ Email global errado + 50 commits = problema. Corrigir o futuro é simples (`git config --global user.email "certo@email.com"`), mas corrigir o histórico já commitado exige reescrita com `git filter-branch` ou ferramentas similares. Verifique antes de começar a trabalhar num repositório novo.