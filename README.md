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
