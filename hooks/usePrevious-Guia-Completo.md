# 🔁 Guia Definitivo do `usePrevious` – Custom Hook (React)

---

## 📌 O que é `usePrevious`

`usePrevious` é um **hook personalizado** (não nativo) que armazena o **valor anterior de uma variável entre renderizações**.

```tsx
const previousValue = usePrevious(currentValue)
```

- Usa internamente `useRef` para guardar o valor antigo
- Muito útil para **comparar valores entre renders**, animar transições ou detectar mudanças

---

## ⚙️ Implementação típica

```tsx
import { useEffect, useRef } from 'react'

function usePrevious(value) {
  const ref = useRef()
  useEffect(() => {
    ref.current = value
  }, [value])
  return ref.current
}
```

---

## ✅ Exemplo de uso

```tsx
function MyComponent({ count }) {
  const prevCount = usePrevious(count)

  useEffect(() => {
    if (prevCount !== undefined && prevCount !== count) {
      console.log('Count mudou de', prevCount, 'para', count)
    }
  }, [count, prevCount])
}
```

---

## 🔍 Quando usar

- Comparar valores atuais vs. anteriores
- Animar mudanças de props/estado
- Detectar transições ou alterações em `boolean`, `number`, `object`, etc.
- Criar lógica de “efeitos condicionais com histórico”

---

## ✅ Checklist de uso do `usePrevious`

- [ ] Preciso comparar um valor com sua versão anterior?
- [ ] Estou usando `useEffect` que depende de saber o valor anterior?
- [ ] Quero evitar bugs causados por valores que mudam entre renders?

---

## ⚠️ Cuidados

- O valor retornado será `undefined` na **primeira renderização**
- Não serve para armazenar histórico múltiplo — apenas **1 valor anterior**
- Depende de `useEffect`, então o valor “atualizado” só estará disponível no **próximo render**

---

## ❗ Anti-patterns

| Padrão                                  | Correção                                     |
|------------------------------------------|----------------------------------------------|
| Esperar que `usePrevious` funcione logo no primeiro render | Ele será `undefined` inicialmente |
| Usar para armazenar múltiplos estados passados | Use array/ref customizado para isso         |
| Recriar a lógica do zero em cada componente | Reutilize `usePrevious` como hook centralizado |

---

## 🧠 Dica avançada

Quer manter múltiplos valores anteriores?

```tsx
function usePreviousMultiple(value, count = 2) {
  const ref = useRef([])

  useEffect(() => {
    ref.current = [value, ...ref.current.slice(0, count - 1)]
  }, [value])

  return ref.current
}
```

---

## 📚 Conclusão

`usePrevious` é a memória curta dos componentes React:

✅ Ajuda a detectar mudanças  
✅ Evita bugs em efeitos que precisam de histórico  
✅ Facilita lógica condicional entre renders

Simples, eficiente e indispensável quando você **precisa saber de onde veio o valor atual**.

