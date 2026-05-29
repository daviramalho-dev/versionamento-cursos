### Definição: SHA-1

SHA-1 é uma função criptográfica que gera um hash de 40 caracteres hexadecimais a partir de qualquer conteúdo. O Git usa esse hash como identidade de tudo — arquivos, árvores e commits. A regra é absoluta: **mesmo conteúdo sempre gera o mesmo hash; qualquer mudança gera um hash completamente diferente.**

Isso é o que torna o Git confiável. Você não precisa confiar no nome ou no caminho de um arquivo — o SHA-1 garante que o conteúdo é exatamente o que deveria ser.

---

### Como fazer

bash

```bash
git hash-object <arquivo>   # SHA-1 do arquivo + header interno do Git
git ls-files -s             # SHA-1 de todos os arquivos rastreados
git rev-parse HEAD          # SHA-1 do commit mais recente
git log --oneline           # histórico com SHA-1 abreviado
git ls-tree -r <SHA>        # estrutura completa de um commit
```

---

### Cascata/Efeitos

|O que muda|Resultado|
|---|---|
|Conteúdo do arquivo|Novo SHA-1 no [[Blob]]|
|Blob dentro da [[Tree]]|Nova SHA-1 da Tree|
|Tree dentro do [[Commit]]|Novo SHA-1 do Commit|

Uma mudança num único caractere de um arquivo propaga novos hashes em cascata por toda a cadeia — [[Blob]] → [[Tree]] → [[Commit]]. É assim que o Git detecta qualquer alteração no histórico, intencional ou não.