# ⏳ Guia Definitivo do `useTransition` – React 18+

---

## 📌 O que é `useTransition`

`useTransition` é um hook do React 18 que permite **marcar atualizações de estado como “não urgentes”**, dando prioridade a interações mais importantes, como digitação ou cliques.

```tsx
const [isPending, startTransition] = useTransition()
```

- `startTransition(fn)` executa `fn` como uma **atualização com baixa prioridade**
- `isPending` indica se há uma transição ainda sendo processada

---

## 🧠 Qual o problema que ele resolve?

Atualizações que são **pesadas ou lentas** podem travar a interface se tratadas com prioridade normal.

Exemplo clássico: digitação em um campo que filtra uma lista com milhares de itens.

Com `useTransition`, o React **prioriza a UI interativa** e **deixa o pesado para depois**.

---

## ⚙️ Exemplo prático

```tsx
const [query, setQuery] = useState('')
const [filtered, setFiltered] = useState([])
const [isPending, startTransition] = useTransition()

const handleChange = (e) => {
  const value = e.target.value
  setQuery(value)

  startTransition(() => {
    const result = expensiveFilter(value)
    setFiltered(result)
  })
}
```

- `setQuery` é imediato (alta prioridade)
- `setFiltered` é feito de forma adiada (baixa prioridade)

---

## 🔁 Diferença: `useTransition` vs `useDeferredValue`

| Hook              | O que faz                                       | Ideal para...                         |
|------------------|--------------------------------------------------|---------------------------------------|
| `useTransition`  | Marca uma **atualização de estado** como lenta   | Controlar *quando* atualizar o estado |
| `useDeferredValue` | Deixa o valor **ser atualizado mais tarde**   | Controlar *quando* consumir um valor  |

---

## ✅ Checklist de uso do `useTransition`

- [ ] Tenho múltiplas atualizações de estado, mas apenas uma precisa ser rápida?
- [ ] Quero que a UI continue fluida durante uma atualização pesada?
- [ ] Quero exibir um `isPending` para mostrar loading apenas durante transições lentas?

---

## 🔬 Benefícios técnicos

- Permite priorizar ações que afetam diretamente a interação do usuário
- Melhora fluidez e UX em grandes listas, formulários ou UIs dinâmicas
- Garante consistência no React Concurrent sem flickers

---

## ❗ Anti-patterns

| Padrão                                | Correção                                        |
|----------------------------------------|-------------------------------------------------|
| Usar `startTransition` em tudo         | Só use quando realmente precisa de prioridade |
| Achar que é um debounce ou delay       | Não é — ele **não espera tempo**, apenas muda a prioridade |
| Usar com `useEffect` ou async direto   | `startTransition(() => setState())` só funciona com `setState` síncrono |

---

## 💡 Dica de UX

Combine com indicadores de carregamento:

```tsx
{isPending && <span>Atualizando...</span>}
```

---

## 📚 Conclusão

`useTransition` é o seu aliado para:

✅ Melhorar experiência do usuário em atualizações pesadas  
✅ Garantir que interações como digitação nunca sejam travadas  
✅ Permitir que o React gerencie a **prioridade de atualização**

Use quando você quiser **separar UI imediata de atualizações pesadas** — e manter sua aplicação suave.

