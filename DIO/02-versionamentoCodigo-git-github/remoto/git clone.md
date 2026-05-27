### Definição: Git Clone

**`git clone`** copia um repositório remoto inteiro para sua máquina — histórico completo, branches e configuração automática do remote `origin`.

Quando você clona, Git cria um diretório local, baixa todos os [[Commit]], cria uma referência automática chamada `origin` apontando para o repositório remoto.

---

### Como Fazer

bash

```bash
# Clonar repositório (HTTPS)
git clone https://github.com/usuario/repositorio.git

# Clonar com nome customizado (ao invés de usar nome do repo)
git clone https://github.com/usuario/repositorio.git meu-projeto

# Clonar via SSH (mais seguro, sem senha)
git clone git@github.com:usuario/repositorio.git
```

Depois de clonar, você pode verificar o remote:

bash

```bash
cd repositorio
git remote -v
# Saída: origin https://github.com/usuario/repositorio.git
```

---

### Exemplo 1: Clonar e Começar a Trabalhar

bash

```bash
git clone https://github.com/seu-usuario/projeto.git
cd projeto

# Fazer mudanças
echo "conteúdo" > arquivo.txt
git add arquivo.txt
git commit -m "primeira mudança"
git push origin main
```

---

### Exemplo 2: Clonar com Nome Customizado

bash

```bash
# Ao invés de criar pasta "projeto"
git clone https://github.com/usuario/projeto.git meu-novo-nome

cd meu-novo-nome
git remote -v  # origin ainda aponta para o repo original
```

---

### Exemplo 3: Clonar via SSH

bash

```bash
git clone git@github.com:usuario/projeto.git

# Não pede senha se SSH key está configurada
# Depois de clonar: git push, git pull funcionam sem credenciais
```

---

### Troubleshooting

|Problema|Solução|
|---|---|
|`fatal: could not read Username`|Use SSH ou reconfigure credenciais HTTPS|
|`Repository not found`|URL incorreta ou repositório privado (sem acesso)|
|Clona mas quer mudar URL depois|Use `git remote set-url origin <nova-URL>`|