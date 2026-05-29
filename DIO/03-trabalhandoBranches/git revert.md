### Definição: git revert

`git revert` cria um **novo [[git commit]]** que desfaz as mudanças introduzidas por um commit anterior. Diferente do [[git reset]], ele não reescreve o histórico — o commit original permanece intacto, e a reversão é registrada como um evento explícito na linha do tempo do projeto.

Isso é o que torna o `git revert` seguro para branches compartilhadas: como o [[Sha-1]] dos commits existentes nunca muda, outros desenvolvedores que já fizeram [[git pull]] não terão conflitos de histórico.

---

### Quando usar

Use `git revert` quando precisar desfazer um commit que **já foi publicado** via [[git push]] para um repositório remoto ([[git remote]]). Em branches locais privadas, [[git reset]] pode ser mais direto — mas assim que outros colaboradores têm acesso ao histórico, `git revert` é a escolha correta.

Casos concretos:

- Um bug foi introduzido em um commit específico e precisa ser revertido sem afetar commits posteriores
- Um deploy quebrou produção e o rollback precisa ser auditável
- É necessário desfazer uma mudança mantendo o registro de que ela existiu

---

### Como fazer

**Reverter um commit único:**

```bash
# Identifica o hash do commit alvo
git log --oneline

# Cria um novo commit que desfaz as mudanças
git revert abc1234

# Confirma sem abrir o editor
git revert abc1234 --no-edit
```

O Git abre o editor para a mensagem do commit de reversão. O padrão gerado é `Revert "mensagem original"`, que geralmente é suficiente.

**Reverter sem commitar imediatamente** (útil para revisar antes):

```bash
git revert abc1234 --no-commit
# As mudanças ficam no staging; revise com git diff ou git status
git commit -m "revert: remove funcionalidade X por quebra no módulo Y"
```

**Reverter um merge commit:**

Merge commits têm dois [[Parente (pai)|pais]]. É preciso indicar qual lado do merge representa a linha principal do histórico:

```bash
git revert -m 1 abc1234
# -m 1 = mantém o primeiro pai (geralmente a branch principal)
```

---

### Tabela comparativa

| Comando | Reescreve histórico? | Seguro em branches públicas? | Caso de uso |
|---|---|---|---|
| `git revert` | Não | ✅ Sim | Desfazer commit já publicado |
| [[git reset]] `--soft` | Sim | ❌ Não | Desfazer localmente, manter mudanças |
| [[git reset]] `--hard` | Sim | ❌ Não | Descartar mudanças completamente |
| [[git restore]] | Não (não cria commit) | ✅ Sim | Restaurar arquivo específico |

---

### Troubleshooting

**Conflito durante o revert:**

O Git pode encontrar conflito se commits posteriores modificaram as mesmas linhas do commit sendo revertido.

```bash
# O revert para e indica os arquivos conflitantes
git status

# Após resolver os conflitos manualmente:
git add arquivo-resolvido.txt
git revert --continue

# Para abortar e voltar ao estado anterior:
git revert --abort
```

**Revert acidental — como desfazer:**

Se o commit de revert foi criado mas ainda não foi publicado, use [[git reset]]:

```bash
git reset --soft HEAD~1
# O commit de revert é removido, mas as mudanças voltam ao staging
```

Se já foi publicado, a solução é fazer um `git revert` do próprio revert — o que restaura o commit original. Isso é perfeitamente válido e mantém o histórico completo e auditável via [[git log]].