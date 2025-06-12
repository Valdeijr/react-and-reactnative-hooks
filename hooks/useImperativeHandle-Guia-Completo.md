# 🕹️ Guia Definitivo do `useImperativeHandle` – React / React Native

---

## 📌 O que é `useImperativeHandle`

`useImperativeHandle` é um hook que permite **personalizar os métodos e propriedades expostas via `ref`** quando um componente é usado com `forwardRef`.

```tsx
useImperativeHandle(ref, () => ({
  metodoExposto: () => { ... }
}))
```

Ele é usado **em conjunto com `forwardRef`**, permitindo que componentes encapsulem sua implementação mas exponham uma API controlada para o pai.

---

## 🔍 Quando usar `useImperativeHandle`

| Situação                                          | Deve usar `useImperativeHandle`? |
|--------------------------------------------------|-----------------------------------|
| Precisa expor métodos de controle para o pai     | ✅ Sim                             |
| Componente interno encapsula lógica de foco, scroll ou animação | ✅ Sim              |
| Está usando `ref` apenas para ler um DOM element | ❌ Não — use `ref` direto          |

---

## ⚙️ Exemplo completo

```tsx
import React, { forwardRef, useImperativeHandle, useRef } from 'react'

const MyInput = forwardRef((props, ref) => {
  const inputRef = useRef()

  useImperativeHandle(ref, () => ({
    focus: () => inputRef.current?.focus(),
    clear: () => inputRef.current.value = ''
  }))

  return <input ref={inputRef} {...props} />
})
```

Uso externo:

```tsx
const inputRef = useRef()
<MyInput ref={inputRef} />
<Button onClick={() => inputRef.current.focus()} />
```

---

## 🧠 O que ele faz por trás

Sem `useImperativeHandle`, o `ref` apontaria para o componente inteiro (`MyInput`).  
Com `useImperativeHandle`, você **controla explicitamente** o que está disponível externamente.

---

## ✅ Checklist de uso do `useImperativeHandle`

- [ ] Estou usando `forwardRef` para expor um componente?
- [ ] Preciso controlar funcionalidades internas do componente a partir do pai?
- [ ] Quero limitar a API exposta e evitar que a ref acesse o DOM completo?
- [ ] Evitei expor diretamente o `ref` interno do componente?

---

## ⚠️ Cuidados

- Só deve ser usado quando o encapsulamento é necessário
- Pode **violar o paradigma declarativo** se abusado
- Torna o componente mais **imperativo** — use com cautela e propósito

---

## 🔬 Casos reais de uso

- **Inputs customizados** com foco automático
- **Componente de scroll** com método `scrollToTop()`
- **Componentes de animação** com `startAnimation()`
- **Exposição de validação manual**, ex: `form.validate()`

---

## ❗ Anti-patterns

| Padrão                               | Correção                                 |
|--------------------------------------|-------------------------------------------|
| Usar `useImperativeHandle` em componente sem `forwardRef` | Não funciona |
| Expor o DOM completo diretamente     | Encapsule e exponha apenas o necessário   |
| Expor lógica mutável sem controle    | Mantenha consistência e estabilidade      |

---

## 📚 Conclusão

`useImperativeHandle` é uma **ponte imperativa dentro do React declarativo**:

✅ Permite controle refinado de APIs internas  
✅ Excelente para componentes reutilizáveis e focados em UX  
❌ Pode criar acoplamento se não usado com disciplina

Use para **dar poder ao pai sem violar o encapsulamento do filho**.
