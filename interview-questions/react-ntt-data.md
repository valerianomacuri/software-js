# Preguntas de entrevista Frontend con React por NTT Data

## 1. ¿Nuevas herramientas para desarrollo frontend y desarrollo de software en general?

- **Frontend:** Vite, Astro, Remix, Qwik, Next.js App Router, React Server Components, shadcn/ui, TanStack Router, Tailwind CSS v3+, Radix UI.
- **General:** Bun, Deno, TurboRepo, Nx, esbuild, SWC, Zod, Prisma, tRPC, Copilot, Codeium.

---

## 2. ¿Qué son los proxies y closures?

### Closures

Funciones que “cierran” sobre su contexto, accediendo a variables de su scope exterior aunque ya haya terminado de ejecutarse el contexto padre.

```js
function makeAdder(x) {
  return function(y) {
    return x + y; // x es closure aquí
  };
}
const add5 = makeAdder(5);
console.log(add5(3)); // 8
```

### Proxies

Objetos que permiten interceptar operaciones sobre otro objeto (get, set, delete, etc). Útil para validaciones, reactividad o APIs dinámicas.

```js
const target = { message: "hello" };
const proxy = new Proxy(target, {
  get(obj, prop) {
    return prop in obj ? obj[prop] : "no existe";
  }
});
console.log(proxy.message); // hello
console.log(proxy.age); // no existe
```

---

## 3. ¿Cómo haces compatible código ES6 con navegadores antiguos?

- Usando **Babel** para transpilar a ES5.
- Configurando **polyfills** (fetch, Promises, etc) con core-js o polyfill.io.
- Bundlers (Webpack, Vite, esbuild) con targets específicos.

---

## 4. ¿Cuándo usas Service Workers?

- Para **PWAs**, offline cache, push notifications, background sync.
- Ejemplo: estrategias cache-first o network-first.

---

## 5. ¿Qué ventajas te da TypeScript?

- Tipado estático detecta errores antes.
- Autocompletado y documentación mejorados.
- Refactors más seguros.
- Facilita el trabajo en equipo y reduce bugs.

---

## 6. ¿Cómo utilizamos una librería que no tiene tipado en un proyecto con TypeScript?

- Instalar types de DefinitelyTyped:

```bash
npm install @types/nombre-lib --save-dev
```

- Si no existen:

```ts
declare module 'nombre-lib';
```

- O crear tipos personalizados para su API.

---

## 7. ¿Cómo migrar una aplicación de Javascript a Typescript?

1. Cambiar extensión a `.ts` o `.tsx`.
2. Configurar `tsconfig.json`.
3. Habilitar `allowJs` y `checkJs` si es progresiva.
4. Migrar módulo por módulo, tipando entradas y props primero.
5. Reducir `any` gradualmente.

---

## 8. ¿Qué son los Higher Order Components?

Funciones que reciben un componente y retornan otro con lógica adicional. Ejemplo: `connect` de Redux.

```js
const withLoading = (Component) => (props) =>
  props.loading ? <Spinner /> : <Component {...props} />;
```

---

## 9. ¿Qué es la hidratación? ¿Qué cosas se enlazan cuando ocurre?

- React enlaza el HTML renderizado en servidor con el Virtual DOM y los listeners de eventos, habilitando interactividad.

---

## 10. ¿Cómo manejas los errores de renderizado?

- Con **Error Boundaries**:

```js
class ErrorBoundary extends React.Component {
  state = { hasError: false };
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  componentDidCatch(error, info) {
    // log error
  }
  render() {
    return this.state.hasError ? <h1>Error</h1> : this.props.children;
  }
}
```

- Con try/catch en efectos o APIs.

---

## 11. ¿Has usado las Core Web Vitals?

- Sí, LCP, FID, CLS.
- Herramientas: Lighthouse, PageSpeed Insights, Web Vitals de Next.js, reportWebVitals.

---

## 12. ¿Qué es Shift Left?

- Filosofía de aplicar calidad y seguridad **desde etapas tempranas**: testing, linting, CI/CD, code review.

---

## 13. ¿Has trabajado con microfrontends, módulos federados, singles spas?

- Sí, con:
  - **Module Federation (Webpack 5)**.
  - **Single SPA** como orquestador.
  - Next.js o Vite como base.

---

## 14. ¿Has trabajado con librerías Zero Runtime CSS?

- Sí, como **Vanilla Extract, Linaria, Astroturf**. Generan CSS en build time eliminando el runtime cost.

---

## 15. ¿Has trabajado con Design System?

- Sí, consumiendo Design Systems (Figma + Storybook) y creando componentes reutilizables siguiendo tokens de diseño y accesibilidad.

---

## 16. ¿Has utilizado middlewares para los estados?

- Sí, en Redux (thunk, saga) o Zustand (persistencia, logging, devtools).

---

## 17. ¿Conoces los side effects en el gestor de estado?

- Sí, operaciones que afectan el exterior (requests, timers, subscripciones). Se manejan con middlewares o useEffect.

---

## 18. ¿Has trabajado en la construcción de paquetes npm?

- Sí, creando librerías internas o publicadas con Rollup o tsup y semantic versioning.

---

## 19. ¿Conoces el semantic version?

- Sí, formato MAJOR.MINOR.PATCH:
  - **Major:** rompe compatibilidad.
  - **Minor:** nuevas features compatibles.
  - **Patch:** fixes sin cambios de API.

---

## 20. ¿Has trabajado con SonarQube?

- Sí, para análisis estático de código (bugs, code smells, duplicación, coverage).

---

## 21. ¿Qué es la métrica de coverage?

- Porcentaje de código ejecutado por tests. Ejemplo: 80% significa que el 80% de las líneas están cubiertas por tests.

---

## 22. ¿Para qué sirven git rebase, git cherry-pick y git stash?

- **git rebase:** reescribe historial moviendo commits encima de otra rama.
- **git cherry-pick:** aplica un commit específico de otra branch.
- **git stash:** guarda cambios no commiteados temporalmente.

---

## 23. ¿Has trabajado con patrones de diseño o clean code?

- Sí, aplicando **Factory, Singleton, Strategy, Observer**, además de SOLID, DRY, KISS, clean architecture y estructura modular.

---
