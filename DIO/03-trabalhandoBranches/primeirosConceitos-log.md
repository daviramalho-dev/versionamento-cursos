### Definição: git log

O [[git log]] exibe o histórico de [[Commit|commits]] em ordem cronológica reversa — do mais recente ao mais antigo. Cada entrada mostra o hash [[Sha-1]], autor, data e mensagem. O output abre num paginador interativo: `q` para sair, `:` para navegar linha a linha, `/` para buscar texto.

bash

```bash
git log
```

#### Filtrando o Histórico

Para restringir o log a um arquivo ou diretório específico, passe o caminho após `--`:

bash

```bash
git log -- caminho/do/arquivo.txt  # histórico de um arquivo
git log -- src/                    # histórico de um diretório
```

#### Flags Essenciais

**`--oneline`** comprime cada commit em uma linha: hash abreviado e primeira linha da mensagem. **`--graph`** renderiza a estrutura de branches e merges como árvore ASCII. Os dois combinados são a forma mais rápida de ler a topologia do repositório.

bash

```bash
git log --oneline
git log --graph --oneline
git log --graph --oneline --all  # inclui todas as branches, não só a atual
```

> Sem `--all`, o log mostra apenas commits acessíveis a partir do [[HEAD]] atual — branches divergentes ficam ocultas.

|Flag|Efeito|
|---|---|
|`--oneline`|Uma linha por [[Commit]] — hash curto + mensagem|
|`--graph`|Topologia de [[git branch\|branches]] em ASCII|
|`--all`|Inclui commits de todas as branches|
|`--follow`|Rastreia renomeações de arquivo|

#### GUIs

**GitKraken** e **GitHub Desktop** renderizam o `--graph` visualmente e facilitam a leitura de históricos com muitas branches. O GitHub Desktop — antes restrito a macOS e Windows — possui hoje suporte oficial a Linux. Para consultas específicas com filtros, o terminal ainda oferece mais flexibilidade.