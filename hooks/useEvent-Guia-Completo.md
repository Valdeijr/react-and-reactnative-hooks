# 🧵 `useEvent` – Controle de referências de função reativas (Experimental)

> **Status**: Experimental (React Canary)

## 🧠 O que é?

O `useEvent` é um hook introduzido nas versões experimentais do React (Canary) para **fornecer uma função com identidade estável**, mas que sempre aponta para a **implementação mais recente**.

Ele resolve o velho problema de _closures congeladas_ em handlers e efeitos, **sem exigir `useCallback` ou refatorações** complexas.

---

## ✅ Motivação

Imagine o seguinte padrão comum:

```tsx
const handler = () => {
  console.log(count); // pode capturar um valor desatualizado de count
};

useEffect(() => {
  window.addEventListener("resize", handler);
  return () => window.removeEventListener("resize", handler);
}, []);
```

O `handler` será congelado com o valor atual de `count`, porque o `useEffect` tem deps vazias.  
Soluções típicas envolvem `useRef`, `useCallback`, ou atualizações manuais — todas feias e propensas a bugs.

Com `useEvent`, esse problema desaparece:

```tsx
const onResize = useEvent(() => {
  console.log(count); // sempre atualizado!
});

useEffect(() => {
  window.addEventListener("resize", onResize);
  return () => window.removeEventListener("resize", onResize);
}, []);
```

---

## 🧪 Como funciona tecnicamente

- A função retornada **mantém a mesma identidade entre renders**.
- Internamente, ela referencia um `ref.current = última versão` da função passada.
- Permite que você use essa função em efeitos e callbacks **sem quebrar as regras de dependência**.

---

## 🛠️ Sintaxe

```tsx
const stableCallback = useEvent((args) => {
  // A lógica mais recente estará aqui em cada render
});
```

---

## 🔍 Quando usar

- ✅ Em listeners (`addEventListener`)
- ✅ Em efeitos que usam funções dependentes de estado
- ✅ Em callbacks passados para componentes de terceiros
- ✅ Em handlers de eventos que mudam com frequência
- ✅ Em hooks customizados para encapsular lógica estável

---

## 🚫 Quando **não** usar

- ❌ Não use em lugar de `useCallback` se a dependência for importante para *memoização*
- ❌ Não use fora do React Canary (ou apps que não suportam experimental builds)

---

## ✔️ Regras de ouro

| Situação | Usar `useEvent`? |
|----------|------------------|
| Você quer função estável com lógica sempre atualizada | ✅ Sim |
| Está trabalhando em projeto com React Canary | ✅ Sim |
| Está num app com React 18 stable | ❌ Ainda não suportado |
| Precisa de função memoizada com dependências claras | ❌ Use `useCallback` |
| Precisa escapar de closures congeladas em listeners | ✅ Sim |
| Está criando um hook customizado que escuta estado | ✅ Sim |

---

## 🧪 Exemplo prático

```tsx
const Component = () => {
  const [count, setCount] = useState(0);

  const handleResize = useEvent(() => {
    console.log("Latest count:", count);
  });

  useEffect(() => {
    window.addEventListener("resize", handleResize);
    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return <button onClick={() => setCount(c => c + 1)}>Increment</button>;
}
```

Sem `useEvent`, o `count` logado seria congelado. Com ele, está sempre sincronizado.
