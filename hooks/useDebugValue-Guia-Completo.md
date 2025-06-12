# 🐞 Guia Definitivo do `useDebugValue` – React

---

## 📌 O que é `useDebugValue`

`useDebugValue` é um hook usado **exclusivamente para depuração (debug)**.  
Ele permite que você **exiba valores customizados no React DevTools** quando estiver inspecionando um hook customizado.

```tsx
useDebugValue(value)
```

- Só funciona em **custom hooks**
- **Não afeta a execução nem o comportamento da aplicação**
- Só aparece no modo de desenvolvimento nas DevTools

---

## 🧠 Quando usar

Você usa `useDebugValue` **dentro de um custom hook**, para ajudar desenvolvedores (inclusive você no futuro!) a entenderem:

- O que o hook retorna
- Qual seu estado atual
- Ou formatar a saída de maneira amigável

---

## ⚙️ Exemplo básico

```tsx
function useOnlineStatus() {
  const [isOnline, setIsOnline] = useState(true)
  useDebugValue(isOnline ? 'Online' : 'Offline')
  return isOnline
}
```

Na React DevTools, ao inspecionar esse hook, você verá:

```
🔧 useOnlineStatus: "Online"
```

---

## 🧪 Com formatação de valor

Você também pode usar uma função de formatação:

```tsx
useDebugValue(date, (d) => d.toISOString())
```

---

## ✅ Checklist de uso do `useDebugValue`

- [ ] Estou escrevendo um **hook customizado** que será reutilizado?
- [ ] O hook possui estado interno ou lógica significativa?
- [ ] Quero facilitar a leitura dos valores no React DevTools?
- [ ] Evitei chamadas pesadas dentro do formatador (execução ocorre em toda render)?

---

## ⚠️ Cuidados

- `useDebugValue` **não deve conter lógica pesada**
- Só é útil para depuração — **não afeta a lógica do hook**
- Ignorado completamente em produção (zero custo)

---

## ❗ Anti-patterns

| Padrão                                     | Correção                                 |
|--------------------------------------------|-------------------------------------------|
| Usar `useDebugValue` em componentes normais | Use apenas em hooks                      |
| Gerar strings longas ou objetos complexos   | Prefira representações legíveis e curtas |
| Esperar que mude comportamento             | Não — é apenas visual para DevTools      |

---

## 📚 Conclusão

`useDebugValue` é o **console.log visual e limpo dos custom hooks**:

✅ Ajuda na inspeção com DevTools  
✅ Deixa hooks reutilizáveis mais transparentes  
✅ Não afeta produção nem performance

Use para tornar sua base de hooks mais **autoexplicativa e fácil de depurar** — especialmente em times.

