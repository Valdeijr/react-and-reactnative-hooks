# 🆔 Guia Definitivo do `useId` – React 18+

---

## 📌 O que é `useId`

`useId` é um hook introduzido no React 18 que gera um **ID único, estável e seguro para SSR (Server-Side Rendering)**.

```tsx
const id = useId()
```

- Garante **unicidade global no app**
- Funciona **consistente entre cliente e servidor**
- Ideal para **atributos HTML de acessibilidade** como `aria-labelledby`, `htmlFor`, etc.

---

## 🧠 Por que não usar `Math.random()` ou `Date.now()`?

Porque esses métodos:

- ❌ Geram IDs diferentes a cada render
- ❌ Causam **incompatibilidade entre SSR e CSR**
- ❌ Quebram o cache ou causam warning de hidratação

O `useId` resolve isso com IDs determinísticos e estáveis por componente/render.

---

## ⚙️ Exemplo prático

```tsx
const id = useId()

return (
  <>
    <label htmlFor={id}>Nome:</label>
    <input id={id} type="text" />
  </>
)
```

---

## 📚 Estrutura dos IDs

O React adiciona um prefixo automático ao ID, como:

```
:react-18:1234
```

Esse prefixo garante **não colisão entre componentes ou renders simultâneos**, inclusive no server.

---

## ✅ Checklist de uso do `useId`

- [ ] Preciso gerar um ID único e estável por render?
- [ ] Estou usando atributos como `htmlFor`, `aria-labelledby`, `aria-describedby`?
- [ ] Preciso garantir consistência entre SSR e cliente?

---

## ⚠️ Cuidados

- `useId` **gera o mesmo ID a cada render do componente**
- **Não use para dados dinâmicos ou identificadores únicos por item de lista** (use `uuid` ou banco)
- **Não é um substituto para chaves de listas (`key`)**

---

## ❗ Anti-patterns

| Padrão                                  | Correção                                      |
|------------------------------------------|-----------------------------------------------|
| Usar `useId` em lista dinâmica com `.map()` | Use `item.id` ou `uuid`                       |
| Usar para valores de banco               | `useId` não deve representar dados persistentes |
| Gerar novo ID manualmente por render     | `useId` já é determinístico e estável         |

---

## 💡 Dica extra

Você pode compor o ID com prefixos para contextos mais legíveis:

```tsx
const id = useId()
const inputId = `user-${id}`
```

---

## 📚 Conclusão

`useId` é a solução nativa do React para:

✅ Geração de IDs únicos, seguros e estáveis  
✅ Evitar conflitos de SSR e bugs de hidratação  
✅ Tornar componentes mais acessíveis e previsíveis

Use para **acessibilidade, form labeling e consistência**, não para lógica de negócios ou dados persistentes.

