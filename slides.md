---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
---
# Que es Next

### Es un framework para el desarrollo web 

<v-click>

Usa la librería de React

</v-click>
---
class: 'text-white'
---

# Y que nos aporta ?

<v-clicks>

- enrutamiento
- renderizado
- fetching
- optimización
- ...

</v-clicks>

---
---
# renderizado
## componentes

existen 2 formas para renderizar componentes en una aplicacion desarrollada con next:

- del lado del cliente, ***client side***
- del lado del servidor, ***server side***

por defecto next trata todos los componentes como ```server side```

<v-click>

<h2>
🤔
</h2>

</v-click>

<v-click>

next no discrima el **comportamiento** por nosotros

somos nosotros los que decidimos que tipos de componentes usar

</v-click>

---
---
# renderizado
### y como identifico que debo usar ? 🤓

segun la docu de next, es facil deducir los componentes de cliente por el hecho de que vamos a usar un hook.

<v-click>

<div>

  <h3> la clave </h3> 
  El comportamiento

</div>

</v-click>

---
---
# renderizado
### Client side

primero creamos nuestro componente

```tsx 
export default function Counter() {
 
  return (
    <div>
      <p>You clicked n times</p>
      <button>Click me</button>
    </div>
  )
}
```

pero este componente counter no cuenta necesita funcionalidad, un comportamiento
---
---
# renderizado
### Client side

le damos un comportamiento

```tsx
import { useState } from 'react'
export default function Counter() {
    const [count, setCount] = useState(0)

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
    )
}
```
---
---
# renderizado
### Client side

le indicamos a next que es un componente de client

```tsx
'use client'
import { useState } from 'react'
export default function Counter() {
    const [count, setCount] = useState(0)

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
    )
}
```
---
---
# renderizado
### Client side

tips:

<v-clicks>

- estudia el comportamiento del componente
- si necesitas usar un Hook, es un claro indicativo
- puedes extraer comportamientos en CustomsHooks
- esto te puede ayudar a ir reduciendo los componentes de cliente

</v-clicks>


---
---
# renderizado

### Server side

como sabemos cuando un componente es de servidor ?

1. es informacion que no va a cambiar, indenpendientemente de lo que haga el cliente

<v-click>

- FAQ
- los header, footers...

</v-click>

2. es informacion que consulta el cliente, traernos informacion de la bbdd para mostrarla

<v-click>

  - muchas veces esa llamada siempre es la misma, podemos crear ese componente en el servidor y enviarlo al cliente

</v-click>

---
---
# renderizado
### Server side -- using pages routes

#### tecnicas

- SSR : Server Side Rendering, La página es generada en cada petición.

- SSG : Static Site Generation, la página se genera en build time. Admite hacerlo con o sin parametros, los datos de estas paginas no cambian muy a menudo.

- ISR: Incremental Static Regeneration, es similar a la anterior pero esta tiene una estrategia de revalidación en el tiempo.

---
---
# renderizado
### Server side -- using app routes

la forma en la que definimos como se comportara nuestra página depende de como definamos la ruta, estática o dinámica

<v-click>


#### static


generamos la página ```in build time```, este contenido estara cacheado y se reutilzara en todas las peticiones de esta página.

</v-click>

<v-click>

#### dynamic
los componentes son renderizados en cada petición.

</v-click>

---
---
# renderizado
### Server side -- using app routes

pintar una pagina suele necesitar unos datos que usualmente tenemos que solicitar a un tercero, recopilar estos datos se conoce como ***fetch***

#### fetch

<v-click>

por defecto cualquier peticion fetch, fuerza el cacheo de los datos

```ts
fetch('https://...') // cache: 'force-cache' is the default
```

</v-click>

<v-click>

puede que necesitemos revalidar datos

```ts
fetch('https://...', { next: { revalidate: 10 } })
```

</v-click>

<v-click>

o que nuestra pagina sea completamente dinamica

```ts
fetch('https://...', { cache: 'no-store' })
```

</v-click>

---
---
# renderizado

### tips

<v-click>

- define bien el comportamiento de tus rutas
```
<!-- static -->
some/route/page.tsx

<!-- dynamic -->
some/[route]/page.tsx
```

</v-click>


<v-click>

- piensa como quieres tratar el cache

</v-click>

<v-click>

- estudia los patrones de diseño, para un uso eficaz del framework

</v-click>
