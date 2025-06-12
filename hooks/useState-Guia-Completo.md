# 🔧 Guia Definitivo do `useState` – React / React Native

---

## 📌 O que é `useState`

`useState` é o hook fundamental do React para **armazenar estado local em componentes funcionais**.

```tsx
const [state, setState] = useState(initialValue)
```

- Armazena e atualiza valores reativos
- Cada chamada a `setState` **dispara um re-render**
- Pode armazenar qualquer tipo de valor: `string`, `number`, `object`, `array`, etc.

---

## ⚙️ Como funciona

```tsx
const [count, setCount] = useState(0)

setCount(prev => prev + 1)
```

- A função `setCount` atualiza o valor e **reativa o render** do componente
- Se você passar uma função para o setter, ela recebe o valor anterior (`prev`)

---

## 🧠 O que preciso saber tecnicamente

- Estado é **encapsulado por componente** – cada instância tem seu próprio valor
- Atualizações de estado são **assíncronas** e podem ser **agrupadas (batched)**
- O estado **não é imediatamente atualizado** após `setState`

---

## 📌 Estado inicial com função

Evite reexecutar código pesado no render:

```tsx
const [data, setData] = useState(() => fetchInitialData())
```

A função é chamada **apenas na montagem**, não em todo render.

---

## ✅ Checklist de uso do `useState`

- [ ] Este valor pertence **somente a este componente**?
- [ ] A mudança nesse estado **deve disparar uma nova renderização**?
- [ ] Evitei modificar objetos/arrays diretamente (imutabilidade)?
- [ ] Considerei usar `useReducer` se o estado ficou muito complexo?

---

## 🔁 Quando usar `useState` vs `useReducer`

| Situação                         | Recomendação       |
|----------------------------------|---------------------|
| Estado simples                   | `useState` ✅        |
| Muitos campos relacionados       | `useReducer` 🔁     |
| Transições de estado previsíveis | `useReducer` 🔁     |
| Atualização baseada no valor anterior | Ambos são bons (usar função no setter) |

---

## 🧱 Composição de estados

Evite fazer múltiplos `useState` para campos relacionados:

```tsx
const [form, setForm] = useState({ name: '', email: '' })
```

---

## ⚠️ Cuidados

- **Não mutar diretamente** objetos ou arrays:

```tsx
// errado
state.items.push(newItem)

// certo
setState(prev => ({ ...prev, items: [...prev.items, newItem] }))
```

- **Evite dependência circular de efeitos que atualizam o próprio estado**
- **Evite loops infinitos** por atualizar estado dentro do render

---

## ❗ Anti-patterns

| Padrão                                     | Correção                                  |
|--------------------------------------------|--------------------------------------------|
| Atualizar estado com valor mutável         | Use cópias imutáveis                       |
| Achar que o estado atualiza imediatamente  | `setState` é assíncrono                    |
| Chamar `setState` fora de handlers ou efeitos | Envolver em lógica controlada            |

---

## 📚 Conclusão

`useState` é a base da reatividade no React:

✅ Simples, direto e eficaz  
✅ Ideal para valores locais e simples  
✅ Atualizações disparam re-renders automaticamente

Mas **quanto mais cresce a lógica**, mais faz sentido evoluir para `useReducer` ou `context`. Use com clareza de escopo e imutabilidade!

