# DEM · Dinámicas de Encuentros Matrimoniales

Sitio web corporativo para **DEM**, organización dedicada a encuentros vivenciales
que fortalecen la comunicación, el diálogo y el amor de las parejas.

Dos páginas construidas con **Astro**: una portada con hero animado que presenta el
movimiento y una página de **inscripción** con formulario que entrega cada registro
por correo electrónico a través de [FormSubmit.co](https://formsubmit.co).

---

## ✨ Características

- **Dos páginas**: portada (`/`) con hero de entrada animado y página de inscripción (`/inscripcion`).
- **Formulario funcional**: envía inscripciones a un correo configurable, con validación nativa de HTML5, honeypot anti-spam y mensajes de éxito/error sin recargar la página (AJAX).
- **Identidad propia**: insignia oficial (`public/Dem Icon.png`) en el hero, cabecera, pie y como favicon.
- **Diseño rojo y blanco** basado en variables CSS fáciles de cambiar.
- **Responsive**: adaptado a móvil y escritorio.
- **Scream Architecture**: la estructura de carpetas comunica el negocio (Inicio, Inscripcion, DEM), no la tecnología.
- **Renderizado estático**: rápido, SEO-friendly y desplegable en cualquier hosting estático o CDN.

---

## 🚀 Empezar

### Requisitos

- [Bun](https://bun.sh) ≥ 1.x (node ≥ 22.12)

### Instalación y desarrollo

```sh
bun install
bun run dev
```

Abre http://localhost:4321

---

## ✉️ Configurar el correo de recepción

Edita `src/config/sitio.ts` y cambia `correoDestino`:

```ts
export const sitio = {
	nombre: 'DEM',
	nombreCompleto: 'Dinámicas de Encuentros Matrimoniales',
	correoDestino: 'tu-correo@gmail.com', // ← aquí llegan las inscripciones
	icono: '/Dem%20Icon.png',
};
```

> **Primera activación de FormSubmit:** la primera vez que alguien envíe el
> formulario, FormSubmit.co mandará un correo al destino pidiendo confirmar la
> dirección (basta con pulsar el enlace de confirmación). Después, los envíos
> llegan automáticamente.

El formulario usa el endpoint AJAX (`https://formsubmit.co/ajax/<correo>`), por lo
que el usuario ve el resultado en la misma página, sin redirecciones.

---

## 🗂️ Estructura del proyecto

Los nombres de las carpetas **gritan el propósito del negocio**, no la tecnología:

```text
dem/
├── public/               # Estáticos: Dem Icon.png, favicon…
├── src/
│   ├── pages/            # Solo cableado de rutas
│   │   ├── index.astro        # /          → portada con hero
│   │   └── inscripcion.astro  # /inscripcion → formulario
│   ├── Inicio/           # Dominio de la portada
│   │   ├── Hero.astro        # Hero con insignia, entrada animada
│   │   └── Propuesta.astro   # Por qué participar
│   ├── Inscripcion/      # Dominio de la inscripción
│   │   └── Formulario.astro  # Formulario + envío AJAX a FormSubmit
│   ├── DEM/              # Identidad global de la organización
│   │   ├── Base.astro        # Layout base (html, head, cabecera, pie)
│   │   ├── Cabecera.astro
│   │   ├── Pie.astro
│   │   └── Estilo/global.css # Variables de color y estilos base
│   └── config/           # Configuración del sitio
│       └── sitio.ts         # Nombre, descripción, correo destino, icono
├── astro.config.mjs
├── bun.lock
├── package.json
└── tsconfig.json
```

### Cómo añadir una página nueva

1. Crea el dominio con sus componentes: `src/<Dominio>/…`.
2. Crea la ruta en `src/pages/mi-pagina.astro`, importa el componente y usa `<Base>`:

```astro
---
import Base from '../DEM/Base.astro';
import MiSeccion from '../MiDominio/MiSeccion.astro';
import { sitio } from '../config/sitio';
---

<Base title={`Mi página · ${sitio.nombreCompleto}`}>
	<MiSeccion />
</Base>
```

---

## 🎨 Personalizar la apariencia

Todos los colores viven como variables CSS en `src/DEM/Estilo/global.css`:

```css
:root {
	--rojo: #d22033;
	--rojo-oscuro: #8f1524;
	--rojo-claro: #e8546b;
	--blanco: #ffffff;
	--hueso: #f8f4f3;
	...
}
```

Cambia la insignia reemplazando `public/Dem Icon.png` (o la ruta en `src/config/sitio.ts`).

---

## 📦 Desplegar

El build genera un sitio **100% estático** en `dist/`, compatible con cualquier
plataforma (Netlify, Vercel, Cloudflare Pages, GitHub Pages, un servidor…).

```sh
bun run build     # genera dist/
bun run preview   # sirve localmente el build
```

Recomendación: en el servicio que uses, apunta el directorio de publicación a `dist`.

---

## 🧞 Comandos

| Comando            | Acción                                |
| :----------------- | :------------------------------------ |
| `bun install`      | Instala las dependencias              |
| `bun run dev`      | Servidor local en `localhost:4321`    |
| `bun run build`    | Build de producción en `./dist/`      |
| `bun run preview`  | Previsualiza el build localmente      |
| `bun run astro ...`| Ejecuta comandos CLI de Astro         |

---

## 🛠️ Stack

| Capa        | Tecnología                                      |
| :---------- | :---------------------------------------------- |
| Framework   | [Astro](https://astro.build) 7 (islas opcionales)|
| Lenguaje    | TypeScript                                      |
| Estilos     | CSS puro con variables                          |
| Envío email | FormSubmit.co (AJAX)                           |
| Runtime dev | Bun                                             |

---

## 📄 Licencia

Proyecto privado de DEM · Dinámicas de Encuentros Matrimoniales.