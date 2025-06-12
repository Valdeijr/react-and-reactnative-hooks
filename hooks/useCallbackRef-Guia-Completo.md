# 🪝 Guia Definitivo do `useCallbackRef` – Custom Hook (React)

---

## 📌 O que é `useCallbackRef`

`useCallbackRef` **não é um hook nativo do React**, mas sim um **padrão popular de custom hook** usado para:

- Manter a **última versão de uma função**
- Evitar **closures obsoletas** dentro de `useEffect`, `setTimeout`, `eventListener`, etc.

---

## 🎯 Por que ele existe

Quando você passa uma função para um `setTimeout` ou `eventListener`, ela **"congela" a referência do momento da criação** (por causa de closures).  
Isso causa bugs quando a função depende de `state` ou `props` atualizados.

`useCallbackRef` resolve isso armazenando a versão mais recente da função numa `ref`.

---

## ⚙️ Implementação típica

```tsx
import { useRef, useCallback } from 'react'

export function useCallbackRef(fn) {
  const ref = useRef(fn)
  ref.current = fn

  const stableCallback = useCallback((...args) => {
    return ref.current(...args)
  }, [])

  return stableCallback
}
```

---

## ✅ Exemplo de uso

```tsx
function MyComponent() {
  const [count, setCount] = useState(0)

  const handle = useCallbackRef(() => {
    console.log('count atual:', count)
  })

  useEffect(() => {
    const id = setInterval(() => {
      handle()
    }, 1000)
    return () => clearInterval(id)
  }, []) // 🔁 não precisa colocar `count` aqui
}
```

✅ O `handle()` sempre usará a versão mais atual de `count`, sem precisar colocar `count` em `useEffect`.

---

## 🧠 Benefícios

- Evita bugs com closures obsoletas
- Permite dependências mais enxutas nos hooks (`[]`)
- Ideal para callbacks de timers, eventos e libs externas

---

## ✅ Checklist de uso do `useCallbackRef`

- [ ] Preciso acessar o valor atualizado de uma função dentro de um efeito ou callback estável?
- [ ] Estou usando `setTimeout`, `eventListener`, `requestAnimationFrame`, etc.?
- [ ] Quero evitar adicionar estados nas dependências apenas para manter a função atualizada?

---

## ⚠️ Cuidados

- O hook assume que você **sempre quer a versão mais recente** da função
- Se você **precisa da versão congelada de um valor**, esse padrão **não é o ideal**
- Pode esconder bugs se usado sem intenção clara

---

## ❗ Anti-patterns

| Padrão                                | Correção                                    |
|----------------------------------------|----------------------------------------------|
| Criar nova função dentro do efeito     | Use `useCallbackRef` para manter referência  |
| Colocar `state` nas deps só para a função funcionar | Remova e use `useCallbackRef`           |
| Usar função "congelada" sem perceber   | Verifique se você precisa de versão reativa |

---

## 📚 Conclusão

`useCallbackRef` é um padrão poderoso para:

✅ Manter a função sempre atualizada sem recriar efeitos  
✅ Evitar bugs com timers/eventos que usam dados desatualizados  
✅ Reduzir dependências desnecessárias em `useEffect`

Use sempre que quiser **executar a versão mais recente de uma função, sem reescrever os efeitos toda hora**.

