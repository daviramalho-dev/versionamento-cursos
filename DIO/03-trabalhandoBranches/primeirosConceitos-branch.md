### Definição: Branches no Git

Uma branch é um ponteiro leve para um [[Snapshot]] do projeto. O Git não duplica arquivos — cria apenas um novo ponteiro que avança independentemente a cada [[git commit|commit]]. A branch padrão se chama `main` (ou `master` em repos mais antigos) e deve sempre representar um estado estável. **Qualquer trabalho novo vive em outra branch.**

---

### Como fazer

**1. Verificar onde você está**

bash

```bash
git branch          # branch ativa aparece com *
```

**2. Criar e entrar na nova branch**

bash

```bash
git checkout -b nova-funcionalidade
```

O `-b` cria e já muda para ela em um passo. A branch nasce do commit atual — herda todo o histórico da `main` até aquele ponto.

**3. Trabalhar e commitar normalmente**

bash

```bash
git add .
git commit -m "adicionando nova funcionalidade"
```

Esses commits existem **só nessa branch**. A `main` não é afetada.

**4. Publicar no remoto**

bash

```bash
git push origin nova-funcionalidade
```

O GitHub vai sugerir a abertura de um Pull Request automaticamente.

**5. Integrar de volta à `main`**

bash

```bash
git checkout main
git merge nova-funcionalidade
git push origin main
```

Se a `main` não teve novos commits enquanto você trabalhava, o Git faz um **fast-forward** — apenas avança o ponteiro sem criar um commit de merge extra.

**6. Renomear uma branch**

bash

```bash
git branch -m novo-nome              # estando NA branch
git branch -m nome-antigo novo-nome  # estando em outra branch
```

O histórico é preservado — só o ponteiro muda de nome.

**7. Deletar uma branch**

bash

```bash
git branch -d nome-da-branch   # seguro: recusa se não foi integrada
git branch -D nome-da-branch   # força mesmo sem merge
```

> ⚠️ Renomear ou deletar localmente **não atualiza o remoto**. Se a branch foi publicada, sincronize manualmente:
> 
> bash
> 
> ```bash
> git push origin --delete nome-antigo
> git push origin novo-nome
> ```

---

### Cascata/Efeitos

|Ação|O que acontece|
|---|---|
|`git checkout -b nome`|Cria o ponteiro no commit atual; [[HEAD]] passa a apontar para ela|
|Commitar na branch|Só o ponteiro da branch avança; `main` fica onde estava|
|`git merge` fast-forward|`main` avança até o último commit da branch; histórico linear|
|`git push origin nome`|Branch passa a existir no remoto|
|`git branch -m novo-nome`|Ponteiro renomeado localmente; remoto não é afetado|
|`git branch -d nome`|Branch local removida; commits permanecem acessíveis por outras branches|
|`git branch -D nome`|Força remoção; commits órfãos ficam inacessíveis|

> ⚠️ Arquivos **não commitados** (untracked ou staged) viajam com você ao trocar de branch. Commite ou use [[primeirosConceitos-stash]] antes de mudar.