# 🧵 Guia Definitivo do `useInsertionEffect` – React 18+

---

## 📌 O que é `useInsertionEffect`

`useInsertionEffect` é um hook especial introduzido no React 18, projetado para **injeção de estilos antes da pintura do DOM**.  

> É o hook com a execução **mais antecipada** de todos: antes do `useLayoutEffect` e `useEffect`.

```tsx
useInsertionEffect(() => {
  // lógica de injeção de estilos
}, [deps])
```

---

## 🧠 Para que serve

- Evita **flickers visuais** causados por estilos que chegam tarde demais
- Permite bibliotecas de CSS-in-JS (como Emotion, styled-components) **injetarem estilos com prioridade**
- Ideal para **inserção de regras de CSS diretamente no DOM**, antes de qualquer layout

---

## 🧪 Ordem de execução dos hooks

```text
useInsertionEffect → useLayoutEffect → useEffect
```

- `useInsertionEffect`: antes da renderização visual (estilo)
- `useLayoutEffect`: após layout, antes do paint
- `useEffect`: após o paint

---

## ⚠️ Restrições importantes

- Só pode ser usado para **injeção de estilos**
- **Não é para lógica de DOM, dados ou timers**
- Funciona apenas em ambientes **client-side** (não SSR-safe)

---

## ⚙️ Exemplo de uso (simulado)

```tsx
useInsertionEffect(() => {
  const style = document.createElement('style')
  style.textContent = '.custom { color: red }'
  document.head.appendChild(style)

  return () => {
    document.head.removeChild(style)
  }
}, [])
```

---

## ✅ Checklist de uso do `useInsertionEffect`

- [ ] Estou injetando estilos no DOM antes da pintura?
- [ ] Preciso evitar flickers visuais em componentes CSS-in-JS?
- [ ] O código depende da criação de `<style>` ou regras de CSS?
- [ ] Estou ciente de que não posso fazer chamadas assíncronas aqui?

---

## 🚫 Anti-patterns

| Padrão                                     | Correção                                 |
|--------------------------------------------|-------------------------------------------|
| Usar para fetch, timers ou efeitos visuais | Use `useEffect` ou `useLayoutEffect`      |
| Usar para manipulação de layout DOM        | Use `useLayoutEffect`                     |
| Esperar SSR-safe                           | Evite — este hook **não é compatível com SSR** |

---

## 📚 Conclusão

`useInsertionEffect` é uma **ferramenta especializada para bibliotecas de estilo**:

✅ Insere CSS no tempo mais precoce possível  
✅ Elimina flickers causados por estilos que aparecem tarde  
❌ Não substitui nenhum outro hook para lógica comum

Só use se **você está controlando a renderização de estilos no nível mais baixo do React**.

