### Definição: Snapshot

Snapshot é a fotografia do estado completo do projeto em um momento específico. A cada [[git commit|commit]], o Git não salva apenas o que mudou — ele registra o estado de **todos** os arquivos rastreados naquele instante, identificado por um [[Sha-1]] único.

Isso é o que diferencia o Git de sistemas que guardam só diffs. Cada snapshot é autossuficiente: você pode voltar a qualquer ponto do histórico sem precisar recalcular mudanças incrementais.

---

### Como funciona na prática

Considere três commits seguidos:

|Snapshot|Estado do projeto|
|---|---|
|Commit 1|`index.js` v1|
|Commit 2|`index.js` v2 + `app.js` novo|
|Commit 3|todos os arquivos editados|

Cada linha é um snapshot independente. O Git não guarda "o que mudou do 1 para o 2" — guarda o projeto inteiro em cada estado, com eficiência via [[Blob]] compartilhados para arquivos que não mudaram.

---

### Cascata/Efeitos

|Ação|O que o Git registra no snapshot|
|---|---|
|[[git commit]]|[[Tree]] com todos os arquivos + [[Sha-1]] único|
|Arquivo não alterado|Reusa o [[Blob]] existente — sem duplicação|
|Arquivo alterado|Novo [[Blob]] com novo [[Sha-1]]|

> 💡 Como cada snapshot tem um [[Sha-1]] único, qualquer alteração retroativa no histórico é detectável — o hash não bate mais.