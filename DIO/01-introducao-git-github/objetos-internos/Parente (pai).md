**Pai (Parente)** é o **commit anterior** ao commit atual.

Cria uma **corrente/histórico** de commits:

```
Commit 1 (sem pai - primeira vez)
  ↓ (pai)
Commit 2 (pai = Commit 1)
  ↓ (pai)
Commit 3 (pai = Commit 2)
  ↓ (pai)
Commit 4 (pai = Commit 3)
```

**Por quê é importante:**

- ✅ Rastreia a sequência de mudanças
- ✅ Permite voltar no tempo
- ✅ Base para branches e merges
- ✅ `git log` mostra a cadeia completa