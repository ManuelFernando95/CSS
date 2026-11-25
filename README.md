# 🕹️ Especificidad en CSS

Notas rápidas sobre cómo el navegador calcula el peso de los selectores para decidir qué estilo gana en pantalla.

---

## 👾 Niveles de Peso

### 🟥 Selector de Etiqueta (`1 punto`)
La base de la estructura. Tiene la prioridad más baja.

```html
<ul>
  <li><a href="#">Inicio</a></li>
</ul>
```
```css
ul {
    list-style-type: none; /* 1 punto */
}
```

### 🟨 Selector de Clase (`10 puntos`)
El estándar para maquetar de forma limpia y reutilizable.

```html
<a href="#" class="btn-comprar">Comprar ahora</a>
```
```css
.btn-comprar {
    background-color: #2563eb; /* 10 puntos (gana a la etiqueta) */
}
```

### 🟩 Selector de ID (`100 puntos`)
Fuerza bruta. Pisa la cascada y rompe la flexibilidad del archivo.

```html
<a href="#" class="btn-comprar" id="btn-destacado">Comprar ahora</a>
```
```css
#btn-destacado {
    background-color: #ea580c; /* 100 puntos (aplasta a la clase) */
}
```

---

## ⚔️ Tabla de Prioridades

| Icono | Selector | Ejemplo | Puntos | Comportamiento |
| :---: | :--- | :--- | :---: | :--- |
| 🟥 | Etiqueta | `ul`, `nav`, `h2` | **1** | Se aplica por defecto si no hay clases. |
| 🟨 | Clase | `.btn-comprar` | **10** | El estándar ideal para el proyecto. |
| 🟩 | ID | `#btn-destacado` | **100** | Bloquea la cascada. Eliminado en refactorización. |

---

## 📌 Conclusión del Taller
Se eliminaron todos los selectores por `#id` de la hoja de estilos, reemplazándolos por un sistema plano de clases y etiquetas. Esto permite resolver colisiones visuales de forma orgánica sin recurrir a malas prácticas como `!important`.


# 📦 Práctica: Modelo de Caja y Estilos CSS

## 🚀 Implementación Técnica
* **Segmentación:** Colores de fondo (`background-color`) distintos en `<header>`, `<main>`, `<aside>` y `<footer>`.
* **Contenedores de Productos (`<article>`):**
  * `padding`: Aire interior para separar textos y enlaces de los bordes.
  * `margin`: Campo de fuerza exterior para evitar colisiones entre tarjetas.
* **Encabezado:** Imagen de fondo en `<header>` con `background-image`, optimizada con `background-size: cover` y `background-position: center`.
* **Auditoría:** Verificación matemática de los valores usando las **DevTools** (pestaña *Computed*).

---

## 🔍 Hallazgos: El Modelo de Caja

### 1. Diferencia entre Margin y Padding
* **Padding:** Espacio interno que empuja el contenido hacia adentro desde el borde.
* **Margin:** Espacio externo que empuja a otras cajas para crear separación entre elementos.

### 2. Importancia de `box-sizing: border-box`
Es obligatorio porque incluye el `padding` y el `border` dentro del ancho total (`width`) del elemento. Esto evita que las cajas se expandan de más y rompan la maquetación.

### 3. Efecto entre Elementos Hermanos
Un margen grande en un elemento empuja físicamente a sus hermanos en el flujo de la página, lo que puede provocar saltos de línea o reacomodos si el espacio del contenedor padre se agota.

---

## 💾 Respaldo y Despliegue
```bash
git add .
git commit -m "feat(ui): implementar modelo de caja y backgrounds"
git push origin feature/modelo-caja
```

## 🎨 Hallazgos: Centralización de Identidad Visual y Espaciado

En esta fase trabajé en la rama `feature/identidad-visual` para limpiar y organizar el código CSS del Catálogo de Productos. La idea principal fue dejar de repetir colores y medidas a mano en cada etiqueta y juntar todo en un solo lugar usando `:root`.

### 📋 1. Variables que declaré en mi CSS

Para que toda la página tuviera el mismo estilo y orden, creé estas variables al principio de mi hoja de estilos:

**Colores 🎨**
* `--color-primario`: Es el color principal de la página, lo usé en los botones importantes, títulos destacados y enlaces.
* `--color-secundario`: Es un tono de apoyo para detalles como bordes, etiquetas o cuando pasas el mouse por encima de un botón.
* `--color-fondo`: El color base que cubre el fondo general de la pantalla y los contenedores.
* `--color-texto`: El color oscuro que usé para que todos los textos y precios se lean bien y sin cansar la vista.

**Tipografía ✍️**
* `--fuente-principal`: La letra que traje desde Google Fonts para que toda la web use exactamente el mismo estilo de texto.

**Espaciados 📏**
* `--espaciado-pequeno: 8px;` Para separaciones cortas, como el espacio entre un ícono y su texto.
* `--espaciado-medio: 16px;` Es el relleno (`padding`) estándar que le puse por dentro a las tarjetas de los productos.
* `--espaciado-grande: 24px;` Lo usé para los márgenes (`margin`) grandes que separan una sección de otra.

### 💡 2. ¿Por qué es mejor reutilizar medidas que inventarlas cada vez?

* **Todo se ve alineado y parejo:** Al usar siempre las mismas tres medidas, todas las tarjetas y botones respiran igual. No queda un cuadro más pegado que otro ni nada se ve torcido.
* **Ahorras tiempo:** No tienes que ponerte a adivinar cuántos píxeles ponerle a cada caja nueva; simplemente eliges entre pequeño, medio o grande y listo.
* **Cambios sin dolor de cabeza:** Si mañana decido que las tarjetas necesitan un poco más de espacio por dentro, solo cambio el número en `:root` y toda la página se actualiza sola en un segundo.

### 🛡️ 3. ¿Cómo evita el `:root` que el diseño se dañe cuando el proyecto crece?

Cuando un archivo CSS se vuelve muy largo, es muy fácil perder el control. Tener todo en `:root` me ayuda por varias razones:

* **Evita el desorden de valores parecidos:** Antes pasaba que en un lado ponía `15px` y en otro `16px` por descuido, o usaba dos tonos de azul casi iguales sin darme cuenta. Con las variables eso se acaba.
* **Un solo lugar manda:** Como todos los elementos toman su estilo de `:root` usando `var()`, cualquier tarjeta o sección nueva que agregue en el futuro va a mantener automáticamente los mismos colores y tamaños sin romper el diseño que ya funciona.


## 📝 Hallazgos: Pseudoclases y Pseudoelementos

### 1. Diferencia entre pseudoclases y pseudoelementos 🔍
Aunque se escriben parecido, cumplen funciones muy distintas en la página:
* Las pseudoclases como :hover, :active o :focus reaccionan a lo que hace el usuario 🖱️. No agregan nada nuevo al código, simplemente cambian el estilo de un elemento de forma temporal cuando alguien pasa el mouse por encima, hace clic o se mueve con el teclado.
* Los pseudoelementos como ::before y ::after sirven para insertar contenido visual extra desde el CSS (como viñetas, líneas o etiquetas) antes o después del contenido real ✨, sin tener que escribir ese texto o adorno en el HTML.

### 2. Importancia de :focus para la accesibilidad ♿
No todas las personas navegan por internet usando un ratón; muchas usan el teclado (con la tecla Tab ⌨️) o herramientas de asistencia. Aplicar estilos claros en el estado :focus, como un borde o contorno visible, permite que el usuario sepa exactamente en qué enlace o botón está parado. Si quitamos o ignoramos este estado, la persona se pierde en la pantalla y la página deja de ser accesible.

### 3. Por qué usar ::before y ::after en lugar de llenar el HTML de etiquetas vacías 🧹
Inyectar adornos desde CSS es una buena práctica porque mantiene el código ordenado y fácil de mantener:
* El archivo HTML queda limpio y solo se encarga de la estructura y el contenido real, sin llenarse de etiquetas div o span vacías que solo sirven para decorar 📄.
* Si más adelante quiero cambiar el texto de una etiqueta de "Oferta" por "Nuevo" en veinte productos distintos, solo cambio una línea en el CSS en lugar de editar tarjeta por tarjeta en el HTML ⚡.
* Los lectores de pantalla no se confunden leyendo elementos que son puramente decorativos.

## Hallazgos: Arquitectura BEM y Modularidad 🧩

### 1. ¿Qué significa BEM y cómo se escribe?
BEM significa Bloque, Elemento y Modificador (por sus siglas en inglés: Block, Element, Modifier). Es una forma de nombrar las clases en CSS para que el código sea ordenado, fácil de leer y reutilizable.

Así es como se escribe en el código:
* **Bloque (`.bloque`):** Es el componente principal e independiente, el que tiene sentido por sí mismo. Por ejemplo: `.card` o `.btn`.
* **Elemento (`.bloque__elemento`):** Es una pieza interna que forma parte del bloque y no funciona sola. Se une al nombre del bloque usando dos guiones bajos (`__`). Por ejemplo: `.card__image`, `.card__title` o `.card__price`.
* **Modificador (`.bloque--modificador`):** Sirve para darle una variación visual o un estado diferente a un bloque o elemento. Se separa usando dos guiones medios (`--`). Por ejemplo: `.card--destacada` o `.btn--secundario`.

### 2. ¿Por qué dividir el CSS facilita el trabajo en equipo? 🤝
Separar un archivo de estilos enorme en archivos más pequeños por cada componente (como `tarjeta.css` o `botones.css`) ayuda mucho cuando varias personas programan al mismo tiempo:
* **Evita choques en Git:** Si una persona está arreglando los botones y otra está diseñando las tarjetas, cada quien trabaja en su propio archivo sin pisar el código del otro.
* **Encontrar errores es más rápido:** Si algo se ve mal en una tarjeta, vas directo a `tarjeta.css` en lugar de perder tiempo buscando entre cientos o miles de líneas de código.
* **Orden al crecer:** Si el proyecto necesita componentes nuevos, simplemente se crean archivos nuevos sin desordenar lo que ya estaba funcionando.

### 3. ¿Cómo evita BEM la "guerra de especificidad"? 🎯
Cuando escribimos CSS tradicional, solemos encadenar muchas etiquetas juntas (como `.catalogo .producto div h2`). Esto hace que los selectores pesen demasiado y, si luego queremos cambiar un estilo, terminamos forzándolo con `!important` o escribiendo selectores todavía más largos.

BEM soluciona este problema manteniendo una especificidad plana:
* **Todo pesa lo mismo:** Como cada pieza tiene su propia clase (ej. `.card__title` en vez de `.card h2`), casi todas las reglas dependen de una sola clase y tienen el mismo peso básico (10 puntos).
* **Sin sorpresas en la cascada:** Al no tener selectores anidados, los estilos de un componente no afectan por accidente a otro, y aplicar una variación como `.card--destacada` funciona de forma limpia y predecible.
