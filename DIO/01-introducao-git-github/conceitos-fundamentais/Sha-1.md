
 
**Secure Hash Algorithm** - Função criptográfica que gera chave de 40 caracteres.
 
- Todo arquivo no Git tem um SHA-1
- Mesmo conteúdo = mesma chave
- Conteúdo diferente = chave diferente
- Cada mudança muda a chave
- Comando pra ver o sha1 puro [[Navegaçao Basica]]

## Comandos Essenciais

```bash
git hash-object <arquivo>    # SHA-1 de um arquivo e header do git
git ls-files -s              # SHA-1 de todos os arquivos
git rev-parse HEAD           # SHA-1 do último commit
git log --oneline            # Histórico com SHA-1 abreviado
git ls-tree -r <SHA>         # Estrutura de um commit
```
