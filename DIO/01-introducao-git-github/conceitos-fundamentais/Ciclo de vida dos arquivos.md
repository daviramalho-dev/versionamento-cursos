Entender em qual estado um arquivo está é fundamental para usar Git com confiança. Todo arquivo em um repositório passa por diferentes estados — rastreando mudanças desde criação até consolidação no histórico.

### Definição

O ciclo de vida no Git é o fluxo que cada arquivo segue até virar parte do histórico. Cada arquivo passa por **4 estados principais**:

|Estado|O que é|Commitável?|
|---|---|---|
|**Untracked**|Git desconhece este arquivo|❌ Não|
|**Unmodified**|Arquivo rastreado, sem mudanças|❌ Não precisa|
|**Modified**|Arquivo alterado, não preparado|❌ Não|
|**Staged**|Arquivo preparado para commit|✅ Sim|

Quando você commita, o Git cria um [[Commit]] que aponta para uma [[Tree]] (representação da estrutura). Essa TREE contém [[Blob]] para cada arquivo e Sha-1 para rastrear mudanças.

### Por que/Quando usar

Você **precisa** dominar isso porque:

- Evita commitar arquivos errados ou temporários
- Permite organizar mudanças logicamente em commits separados
- Corrige erros **antes** de historicizar (bem mais fácil que reverter depois)
- Melhora legibilidade do histórico — cada commit é uma mudança lógica

**Caso real:** Você trabalhou em 3 coisas (bug fix, feature, docs). Com git add seletivo, faz 3 commits claros. Sem isso, tudo vira "mudanças aleatórias" — inútil para debug.

### O ciclo passo a passo

#### 1. Untracked → Staged (Novo arquivo)

Arquivo criado? Git não o rastreia ainda.

```bash
# Ver arquivos untracked
git status

# Adicionar arquivo específico
git add main.js

# Adicionar todos
git add .
```

**O que acontece:** Arquivo sai de Untracked direto para Staged. Git prepara um [[Blob]] com seu conteúdo.

#### 2. Unmodified → Modified (Editar arquivo rastreado)

Você editou um arquivo que já estava no repositório.

```bash
# Ver quais arquivos mudaram
git status

# Ver mudanças específicas (antes de add)
git diff main.js
```

**Internamente:** Conteúdo mudou = novo Sha-1 para o arquivo = a [[Tree]] que contém esse arquivo mudará quando você commitar.

#### 3. Modified → Staged (Preparar mudanças)

Você decide quais mudanças entram neste commit.

```bash
# Adicionar arquivo específico
git add main.js

# Ver o que será commitado
git diff --staged

# Adicionar mudanças linha por linha
git add -p main.js
```

**Dica técnica:** `git add -p` te mostra cada hunk (bloco de mudança) e pergunta se você quer stagar. Perfeito para dividir mudanças lógicas em commits separados.

#### 4. Staged → Commit (Criar snapshot)

Tudo pronto? Commite.

```bash
git commit -m "Refatora validação de email"
```

**O que Git faz:**

1. Calcula [[Sha-1]] de cada [[Blob]] (arquivo modificado)
2. Calcula [[Sha-1]] da [[Tree]] (estrutura + Shas dos arquivos)
3. Cria [[Commit]] que aponta para essa TREE
4. Arquivo volta a Unmodified

Depois do commit, até você editar novamente, o arquivo fica em Unmodified.

**Regra de ouro:** Quando em dúvida, `git status`. Ele sempre te diz onde você está no ciclo e o que fazer.