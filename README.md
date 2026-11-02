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
