# 🧱 Guia Definitivo do `useLayoutEffect` – React / React Native

---

## 📌 O que é `useLayoutEffect`

`useLayoutEffect` é um hook igual ao `useEffect`, mas com uma **diferença crítica de timing**:

- Ele é executado **sincronamente após todas as mutações no DOM/layout**, **antes da pintura da tela**.

```tsx
useLayoutEffect(() => {
  // executa antes do browser pintar
  return () => {
    // cleanup
  }
}, [deps])
```

Em React Native, o conceito se aplica de forma semelhante: é executado antes do layout ser aplicado visualmente.

---

## ⏱️ Diferença entre `useEffect` e `useLayoutEffect`

| Aspecto                  | `useEffect`               | `useLayoutEffect`            |
|--------------------------|---------------------------|-------------------------------|
| Momento de execução      | Após o paint (assíncrono) | Antes do paint (síncrono)     |
| Pode causar flickering   | Sim                       | Não                           |
| Uso ideal                | Efeitos não visuais       | Efeitos que afetam layout ou medida |
| Bloqueia renderização    | Não                       | Sim (cuidado com longos delays) |

---

## 📐 Casos em que `useLayoutEffect` é necessário

### ✅ 1. Medir dimensões de elementos antes da tela pintar
```tsx
useLayoutEffect(() => {
  const height = ref.current?.offsetHeight
  setHeight(height)
}, [])
```

### ✅ 2. Realinhar elementos dinamicamente antes do usuário ver
- Scroll automático
- Animações baseadas em layout
- Ajustes visuais sensíveis

### ✅ 3. Corrigir estado ou estilo com base no layout calculado

---

## ⚠️ Cuidados com `useLayoutEffect`

- **Executa sincronamente**: se fizer operações pesadas, bloqueia a UI
- **Evite chamadas assíncronas diretas** – use `requestAnimationFrame`, timers ou `queueMicrotask` se necessário
- **React 18 + StrictMode** executa `useLayoutEffect` duas vezes seguidas no DEV

---

## ✅ Checklist de uso do `useLayoutEffect`

- [ ] Preciso ler ou alterar dimensões/layout antes da tela ser exibida?
- [ ] Há algum "salto" visual que quero evitar ao montar o componente?
- [ ] Estou usando isso conscientemente no lugar de `useEffect` por causa do momento da execução?
- [ ] Evitei fazer tarefas longas dentro dele?

---

## 🔥 Anti-patterns

| Padrão                          | Correção                                  |
|----------------------------------|--------------------------------------------|
| Usar `useLayoutEffect` para lógica que não afeta o layout | Use `useEffect` normal |
| Fazer chamadas assíncronas diretas no `useLayoutEffect` | Use `useEffect` ou `requestAnimationFrame` |
| Misturar lógica visual e não-visual | Separe os efeitos em hooks distintos      |

---

## 🧠 Dica avançada

- Em React Native, `useLayoutEffect` também pode ajudar com medidas de `View`, `Text` ou ajustes de rolagem
- Pode ser usado com refs combinadas (`forwardRef`) para posicionar elementos antes da renderização

---

## 📚 Conclusão

`useLayoutEffect` é um **hook crítico para manipulações visuais precisas**:

✅ Ideal para leitura/ajuste de layout antes do usuário ver  
❌ Não deve ser usado para lógica geral, pois **bloqueia a pintura**

Use com moderação e sempre que o timing for crucial.

