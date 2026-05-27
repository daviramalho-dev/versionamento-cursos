### Hierarquia de Configuração: Os Três Níveis

|Nível|Flag|Escopo|Arquivo|
|---|---|---|---|
|**Sistema**|`--system`|Toda máquina, todos os usuários|`/etc/gitconfig` (Linux/Mac) ou `%ProgramFiles%\Git\etc\gitconfig` (Windows)|
|**Usuário**|`--global`|Seu usuário do SO, qualquer repo|`~/.gitconfig` (Linux/Mac) ou `%APPDATA%\.gitconfig` (Windows)|
|**Local**|`--local`|Um repositório específico|`.git/config` dentro do repo|

**Ordem de precedência** (última vence):

```
sistema → usuário → local
```

Se você define `user.name` em `--global` e depois em `--local`, Git usa o valor local naquele repositório.

---

### Por Quê e Quando Usar Cada Nível

**Use `--system`** quando trabalha em máquina compartilhada e quer padrões para todos os usuários (raro). Requer permissões administrativas.

**Use `--global`** para sua identidade pessoal (`user.name`, `user.email`), editor padrão, aliases — tudo que se aplica a todos seus projetos em uma máquina.

**Use `--local`** quando um projeto específico precisa de configurações diferentes: email corporativo em repo de trabalho, identidade falsa em repo de demonstração, ou branches padrão customizados.

---

### Para Editar Diretamente

```bash
# Abrir em editor
git config --global --edit
git config --local --edit

# Ver caminho sem abrir
git config --list --show-origin
```

**Localizações exatas:**

- **Linux/Mac**: `~/.gitconfig` (global) e `.git/config` (local no repo)
- **Windows**: `C:\Users\SeuUsuário\.gitconfig` (global) e `.git\config` (local)
- **Sistema**: `/etc/gitconfig` (não disponível em Windows)

---

### Cascata e Efeitos Colaterais

Quando você altera uma configuração, ela afeta:

- **`--global`**: Todos os repositórios existentes e novos naquela máquina
- **`--local`**: Apenas esse repositório (arquivo `.git/config`)
- **`--system`**: Todos os usuários e repositórios (requere `sudo`)

⚠️ **Armadilha comum:** Você define email global incorreto, faz 50 commits, depois descobre. A solução é:

```bash
# Corrigir futuro
git config --global user.email "correto@email.com"

# Passado: necessário reescrever histórico (git filter-branch, etc.)
```

A cascata de leitura funciona assim:

```
Início do comando git
        ↓
Verifica .git/config (local)
        ↓
Verifica ~/.gitconfig (global)
        ↓
Verifica /etc/gitconfig (sistema)
        ↓
Usa primeiro valor encontrado
```