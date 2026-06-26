# Vestidor

App para llevar el inventario de tu ropa, registrar cuándo usás cada prenda
y recibir recomendaciones de qué regalar, reemplazar o comprar — basada en
tus datos, no en plantillas genéricas.

Funciona 100% en el navegador: no hay servidor, no hay cuentas, no hay
tracking. Todo se guarda en el `localStorage` de tu teléfono o computadora.
Por eso es clave exportar un respaldo de vez en cuando (ver más abajo).

## Qué incluye

- **Ropero**: catálogo de tus prendas (tipo, marca, color, talle, precio,
  estado, foto opcional) con búsqueda, filtros y orden por uso/precio/etc.
- **Registrar**: anotá qué te pusiste hoy (o cualquier día), para qué
  actividad, y con qué prendas — pueden ser varias a la vez (ej. remera +
  short).
- **Actividades editables**: Trabajo, Casa, Dormir, Sport, etc. — los
  nombres y códigos son tuyos, los editás en Ajustes.
- **Estadísticas**: resumen general, recomendaciones automáticas
  (prendas nunca usadas, dormidas hace mucho, caras por uso, muy
  desgastadas, huecos en tu ropero), ranking de más/menos usadas y
  calendario de uso.
- **¿Qué me pongo?**: sugerencia de outfit (arriba + abajo) según
  probabilidad de uso y rotación reciente, en la pantalla de Inicio.
- **Respaldo**: exportar/importar todo como `.json` (recomendado, fidelidad
  completa) o exportar a `.xlsx` para abrir en Excel. También podés
  reimportar tu Excel original (`Clothing.xlsx`) para sumar prendas sin
  perder lo que ya tengas cargado.
- **Instalable**: manifest + service worker, así que se puede "Agregar a
  pantalla de inicio" y funciona sin conexión.

La primera vez que abrís la app (con el `localStorage` vacío), se carga
automáticamente todo lo que ya tenías en tu Excel original — las 68 prendas
de la hoja "Vestimenta" y los registros de uso de la hoja "Frecuencia" — así
no arrancás de cero.

## Estructura de archivos

```
index.html       shell de la app y las 5 pantallas
style.css        sistema de diseño (paleta, tipografía, componentes)
app.js           toda la lógica: datos, estadísticas, recomendaciones, UI
seed-data.js     datos iniciales generados desde tu Clothing.xlsx
manifest.json    metadata de instalación (íconos, nombre, colores)
sw.js            service worker (caché offline)
icons/           íconos de la app (192, 512, 512 maskable)
```

## Publicar en GitHub Pages

1. Creá un repositorio nuevo en GitHub (puede ser público o privado con
   GitHub Pages habilitado en tu plan).
2. Subí estos archivos a la raíz del repo (o a una carpeta `/docs` si
   preferís) manteniendo la estructura de carpetas tal cual — especialmente
   `icons/`.
3. En **Settings → Pages**, elegí la rama y carpeta donde están los
   archivos, guardá, y esperá unos segundos a que se publique.
4. Abrí la URL que te da GitHub Pages desde el celular.

## Instalar en el celular

- **Android (Chrome)**: abrí la URL, tocá el menú (⋮) → **Agregar a
  pantalla de inicio** (o aparece un banner automático de instalación).
- **iPhone (Safari)**: abrí la URL, tocá el ícono de compartir → **Agregar
  a pantalla de inicio**. Safari no soporta el banner automático ni el
  service worker tan completo como Chrome, pero la app funciona igual.

## Actualizar la app después de cambios

Si editás `index.html`, `style.css`, `app.js` o `seed-data.js` y volvés a
subirlos a GitHub, **subí también `sw.js` y cambiá el valor de
`CACHE_VERSION`** (por ejemplo de `"v1"` a `"v2"`). Si no, el navegador
puede seguir mostrando la versión vieja desde la caché.

## Sobre el almacenamiento

Los datos viven solo en este dispositivo (`localStorage`). Si cambiás de
celular, reinstalás el navegador, o limpiás los datos del sitio, se
pierden — por eso la app te muestra cuánto espacio estás usando en
Ajustes, y por eso conviene exportar un respaldo `.json` cada tanto (por
ejemplo, después de cargar varias prendas nuevas). Si agregás fotos a las
prendas, el respaldo va a pesar más — las fotos se comprimen automáticamente
antes de guardarse, pero igual conviene revisar el uso de espacio si cargás
muchas.

## Privacidad

No hay backend, no hay analytics, no se envía nada a ningún servidor salvo
las fuentes (Google Fonts) y la librería SheetJS (para leer/escribir
Excel), que se cargan desde un CDN público la primera vez que tenés
conexión y después quedan cacheadas para uso sin conexión.
