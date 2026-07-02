# Fluyo — diagramas que fluyen

Editor de diagramas de arquitectura **animados**, con exportación a **GIF, PNG, JPG y SVG** directamente desde el navegador. Sin cuenta, sin backend, sin que tus diagramas salgan de tu máquina: todo (edición, animación y codificación del GIF) ocurre 100% en el cliente.

## Funcionalidades

- Formas clásicas (caja, cilindro/BD, rombo, círculo, hexágono, texto) + iconos cloud (GCP, AWS, Azure, Kafka, K8s…)
- Conexiones estilo draw.io: flechas direccionales al pasar el mouse, anclaje por lado, ruteo ortogonal y codos editables
- Selección múltiple con marco, copiar / cortar / pegar / duplicar (`Ctrl+C/X/V/D`, `Ctrl+A`)
- Páginas múltiples con pestañas; guardar y abrir archivos `.fluyo.json`
- Pegar imágenes externas con `Ctrl+V` o arrastrándolas al lienzo
- Animación de flujo en las flechas, pulso por nodo y aparición secuencial
- Export GIF con loop perfectamente cíclico, PNG con fondo transparente, JPG y SVG, hasta 1920×1080
- Exportación a SVG editable para documentación y herramientas vectoriales
- Autoguardado local con recuperación de sesión
- Soporte básico para instalación/offline mediante PWA
- Tema oscuro y crema, tipografía Georgia, paleta semántica

## Exportación

Fluyo permite exportar diagramas como GIF, PNG, JPG y SVG.

SVG es útil cuando necesitas conservar el diagrama como gráfico vectorial editable para documentación, presentaciones o herramientas de diseño.

## Privacidad y almacenamiento local

Fluyo no requiere cuenta ni backend. Los diagramas se procesan localmente en el navegador.

Si el autoguardado está activo, la última sesión se almacena en `localStorage` del navegador del usuario.

## Uso offline

Fluyo incluye una base PWA para cargar la aplicación como experiencia local/offline. Algunas funciones pueden depender de recursos externos si se mantienen dependencias vía CDN.

La exportación GIF usa [gif.js](https://github.com/jnordberg/gif.js) desde CDN. El service worker intenta precachear `gif.js` y `gif.worker.js` en la primera visita online; si no están en caché, la exportación GIF puede fallar offline. PNG, JPG, SVG y el resto de la app funcionan sin conexión una vez cargada.

## Stack

HTML + CSS + JavaScript vanilla sobre Canvas 2D. Una sola dependencia externa: [gif.js](https://github.com/jnordberg/gif.js) vía CDN para codificar el GIF en web workers. No hay build, no hay framework, no hay servidor.

## Desplegar en Vercel

### Opción A — GitHub (recomendada)

1. Crea un repositorio en GitHub y sube esta carpeta (`index.html`, `manifest.webmanifest`, `sw.js` y `README.md`).
2. En [vercel.com](https://vercel.com) → **Add New → Project** → importa el repo.
3. Framework Preset: **Other**. No cambies nada más (no hay build command ni output directory).
4. **Deploy**. Listo: cada push a `main` redespliega automáticamente.

### Opción B — CLI

```bash
npm i -g vercel      # una sola vez
cd fluyo
vercel               # primer deploy (preview)
vercel --prod        # deploy a producción
```

### Dominio propio

En el dashboard de Vercel → Settings → Domains puedes apuntar `fluyo.app`, `fluyo.dev` o el que registres. Vercel gestiona el certificado SSL automáticamente.

## Desarrollo local

Puedes abrir `index.html` directamente en el navegador. Para probar la PWA y el service worker hace falta servir los archivos por HTTP:

```bash
npx serve .
```

## Licencia

Decide la tuya antes de publicar el repo. Sugerencia: MIT si quieres que la comunidad contribuya libremente.
