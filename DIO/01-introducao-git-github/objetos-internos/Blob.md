### Definição: Blob

Blob (Binary Large Object) é como o Git armazena o conteúdo de um arquivo. Ao executar [[git add]], o Git lê o arquivo, calcula o [[Sha-1]] do conteúdo e salva um blob no repositório interno. O nome e o caminho do arquivo não fazem parte do blob — isso é responsabilidade da [[Tree]].

A regra central: **mesmo conteúdo = mesmo [[Sha-1]] = mesmo blob**. O Git nunca duplica blobs idênticos, independente de quantos commits referenciem aquele conteúdo.

---

### Exemplo prático

Três commits com o mesmo vídeo em estados diferentes:

|Commit|Arquivo|Blob|Espaço adicionado|
|---|---|---|---|
|1|`video.mp4` (500MB)|`abc123` — novo|+500MB|
|2|`meu_video.mp4` (mesmo conteúdo)|`abc123` — reutilizado|+0MB|
|3|`meu_video.mp4` (450MB, comprimido)|`xyz789` — novo|+450MB|

**Total no Git: 950MB** — e não 1.45GB, porque o commit 2 só renomeou o arquivo sem alterar o conteúdo. O blob `abc123` foi reaproveitado.

---

### Cascata/Efeitos

|Situação|Resultado|
|---|---|
|Conteúdo igual, nome diferente|Mesmo blob, mesmo [[Sha-1]] — zero espaço extra|
|Qualquer alteração no conteúdo|Novo blob, novo [[Sha-1]]|
|Blob referenciado por uma [[Tree]]|[[Commit]] aponta para a Tree, que aponta para o blob|

> ⚠️ O Git rastreia **conteúdo**, não arquivos. Renomear não cria blob novo — modificar sim.