# Portfolio Personal — María del Rosario Presedo Valenzuela

**Materia:** Diseño y Desarrollo Web · UADE  
**Agencia simulada:** [Nexo Studio](https://mrosariopresedo.github.io/nexo-studio/)  
**Año:** 2026

---

## Descripción general

Este repositorio contiene mi portfolio personal, desarrollado como parte de la **Actividad 1** de la materia Diseño y Desarrollo Web. El sitio presenta mi perfil como Desarrolladora Front-end con formación en seguridad informática, y mi rol dentro de la agencia académica **Nexo Studio**.

El sitio está compuesto por tres páginas:

- `index.html` — Inicio: presentación, competencias y vínculo con Nexo Studio
- `intereses.html` — Intereses personales con fotografías ilustrativas
- `contacto.html` — Canales de contacto y disponibilidad

---

## Estructura de archivos

```
/
├── index.html
├── intereses.html
├── contacto.html
├── styles/
│   └── styles.css
└── img/
    └── infografia.jpg
```

---

## Paleta de colores y tipografía

### Paleta: *Teal & Terracota sobre Crema*

| Variable CSS | Valor | Rol en el diseño |
|---|---|---|
| `--accent` | `#1f7a8c` Teal/Petróleo | Color primario de acción, bordes y etiquetas |
| `--accent-2` | `#e07a5f` Terracota | Calidez, estados hover, acentos secundarios |
| `--bg` | `#f6f2ea` Crema | Fondo general — más cálido y humano que el blanco puro |
| `--bg-alt` | `#ece3d6` Arena | Fondo alternado en secciones para crear profundidad visual |
| `--ink` | `#1a2333` Azul marino | Texto principal — máxima legibilidad y autoridad |
| `--ink-soft` | `#4c5a6a` Gris azulado | Texto secundario, párrafos descriptivos |
| `--card` | `#ffffff` Blanco | Fondo de tarjetas — emerge sobre la crema (Figura-Fondo) |

**Por qué esta paleta:** El teal transmite confianza y profesionalismo tecnológico. La terracota aporta calidez y diferencia el sitio de los portfolios genéricos del sector. La base crema evita la frialdad clínica del blanco puro y crea una sensación de identidad propia.

### Tipografía

- **Sora** (Google Fonts, pesos 400/600/700): Titulares, nav, labels, botones. Geométrica y moderna, transmite precisión.
- **Source Sans 3** (Google Fonts): Cuerpo de texto. Alta legibilidad en pantalla a cualquier tamaño.

Ambas familias se importan con `@import` en el CSS y como `<link>` en el `<head>` de cada página.

---

## Estructura HTML semántica

Se aplicó HTML5 semántico en toda la estructura del sitio:

| Etiqueta | Uso en el sitio |
|---|---|
| `<header>` | Contiene el `<nav>` y el `<section>` del hero o page-header |
| `<nav>` | Barra de navegación con los tres enlaces del sitio |
| `<main>` | Contenido principal de cada página |
| `<section>` | Cada bloque temático (sobre mí, competencias, CTA) |
| `<article>` | Tarjetas individuales de competencias e intereses |
| `<aside>` | Bloques de información complementaria (nexo-card) |
| `<figure>` / `<figcaption>` | Imágenes con pie de foto |
| `<footer>` | Cierre del documento con créditos y contacto |

**Jerarquía de títulos:** Cada página tiene exactamente un `<h1>`. Los subtítulos de sección usan `<h2>`, los de tarjetas `<h3>`, y los bloques aside `<h4>`. Nunca se salta un nivel de jerarquía.

**Seguridad aplicada al HTML:** Todos los enlaces externos usan `rel="noopener noreferrer"` para prevenir el ataque *reverse tabnapping*, donde una pestaña abierta podría manipular la página de origen. Este es un ejemplo concreto de cómo la formación en seguridad informática se aplica directamente en el código front-end.

---

## Maquetado: `display: inline-block` y Modelo de Caja

Todos los layouts de columnas múltiples se construyeron con `display: inline-block`, sin usar Flexbox ni CSS Grid.

### Técnica anti-espacio-fantasma

Cuando se colocan elementos `inline-block` uno al lado del otro, el espacio en blanco entre etiquetas HTML genera un hueco visual no deseado. La solución aplicada en todo el sitio:

```css
.hero-inner {
    font-size: 0; /* elimina el espacio fantasma */
}

.hero-text {
    display: inline-block;
    width: 56%;
    font-size: 1rem; /* restaura el tamaño dentro del hijo */
}
```

### Layouts aplicados

**Hero — 2 columnas (texto + imagen circular):**
```css
.hero-text   { display: inline-block; width: 56%; vertical-align: middle; }
.hero-visual { display: inline-block; width: 40%; margin-left: 4%; vertical-align: middle; }
```

**Sobre mí — 2 columnas (texto + infografía):**
```css
.about-text  { display: inline-block; width: 55%; vertical-align: top; }
.about-media { display: inline-block; width: 40%; margin-left: 5%; vertical-align: top; }
```

**Tarjetas de competencias — 3 columnas:**
```css
.card { display: inline-block; width: 30%; margin: 0 1.6% 24px; vertical-align: top; }
```

**Tarjetas de intereses — 2 columnas:**
```css
.interest-card { display: inline-block; width: 46%; margin: 0 2% 28px; vertical-align: top; }
```

**Nexo Studio card — 2 columnas sobre fondo oscuro:**
```css
.nexo-left  { display: inline-block; width: 56%; vertical-align: middle; }
.nexo-right { display: inline-block; width: 40%; margin-left: 4%; vertical-align: middle; }
```

### Altura uniforme entre tarjetas

Para que todas las tarjetas de una fila tengan el mismo alto sin usar Flexbox ni JavaScript, se aplica `min-height` fijo. Es la técnica clásica pre-flexbox: cada tarjeta respeta el mínimo, y las que tienen más contenido simplemente crecen hacia abajo.

```css
.card { min-height: 230px; }
.interest-body { min-height: 180px; }
```

El **Modelo de Caja** se controla con `padding` interno (espacio entre borde y contenido) y `margin` externo (separación entre tarjetas), creando la "respiración" que hace legible cada componente.

---

## Navegación: `position: sticky`

```css
.site-nav {
    position: sticky;
    top: 0;
    z-index: 100;
    background-color: rgba(246, 242, 234, 0.95);
    backdrop-filter: blur(8px);
}
```

La barra de navegación permanece fija en la parte superior durante el scroll. Se usa `position: sticky` en lugar de `fixed` porque respeta el flujo del documento y no requiere compensación de espacio. El `backdrop-filter: blur` agrega un efecto de vidrio esmerilado.

La navegación usa `float: left` para el logo y `float: right` para los enlaces, con un clearfix para limpiar el flujo:

```css
.nav-logo  { float: left; }
.nav-links { float: right; }
.nav-inner::after { content: ''; display: block; clear: both; }
```

---

## Imágenes responsivas

Todas las imágenes aplican la regla de imágenes fluidas:

```css
img {
    max-width: 100%;
    height: auto;
    display: block;
}
```

Esto garantiza que ninguna imagen desborde su contenedor en pantallas pequeñas.

**Imágenes del sitio:**

- `img/infografia.jpg` — Aparece en el hero (recortada en círculo con `border-radius: 50%`) y en la sección "Sobre mí" como documento completo con `<figcaption>`.
- Fotografías de intereses — Cuatro imágenes en las tarjetas de `intereses.html`, cada una dentro de un `<figure class="interest-img">` con `object-fit: cover` para mantener proporciones.

---

## Leyes de la Gestalt aplicadas

### Ley de Semejanza

Las seis tarjetas de competencias (`.card`) son visualmente idénticas: mismo `border-radius`, misma `box-shadow`, mismo `padding`, mismo `border-top: 3px solid var(--accent)`. El ojo las percibe automáticamente como un grupo relacionado sin necesidad de texto que lo indique.

Lo mismo aplica para las cuatro tarjetas de intereses: mismas dimensiones, mismo overflow con imagen en la cabecera, misma estructura interna.

### Ley de Proximidad

Los tres bloques de stats dentro de "Sobre mí" están agrupados con `padding` interno que los une visualmente, separados del resto del contenido por un `border-top` y `margin`. Elementos cercanos se perciben como relacionados.

### Ley de Figura-Fondo

Las tarjetas blancas (`#ffffff`) emergen sobre el fondo crema (`#f6f2ea`). La sección de competencias usa `background-color: var(--bg-alt)` como franja alternada, creando diferencia de profundidad entre bloques y ayudando al ojo a segmentar el contenido.

### Ley de Continuidad

La barra de navegación con `position: sticky` genera una línea horizontal persistente durante el scroll. El ojo sigue esa línea como guía visual constante, reduciendo la carga cognitiva de navegación.

### Ley de Cierre

El avatar circular en el hero (`border-radius: 50%`) sugiere una figura completa y cerrada. El anillo exterior generado con `box-shadow: 0 0 0 12px rgba(...)` refuerza ese efecto de cierre sin agregar elementos HTML extra.

---

## Diseño Responsive: `@media` queries

Se definieron dos puntos de quiebre:

### 900px — tableta / laptop pequeña

Las columnas múltiples se reducen. Las tarjetas de competencias pasan de 3 columnas a 2. El hero apila texto arriba e imagen abajo. La nexo-card apila sus columnas verticalmente.

```css
@media (max-width: 900px) {
    .hero-text  { display: block; width: 100%; }
    .hero-visual { display: block; width: 100%; margin-left: 0; }
    .card { width: 46%; margin: 0 2% 22px; }
}
```

### 600px — móvil

Todo pasa a una sola columna. Las tarjetas ocupan `width: 100%`. El nav apila el logo y los enlaces. Los botones del hero se apilan verticalmente.

```css
@media (max-width: 600px) {
    .card,
    .interest-card,
    .contact-card,
    .stat { width: 100%; margin: 0 0 18px; }

    .hero h1 { font-size: 30px; }
    .nav-logo { float: none; display: block; text-align: center; }
    .nav-links { float: none; text-align: center; }
}
```

---

## Front-end y seguridad informática: mi diferencial

Como desarrolladora front-end con formación en seguridad, aplico criterios de seguridad directamente en el código que escribo:

| Concepto de seguridad | Aplicación concreta en este sitio |
|---|---|
| Reverse tabnapping | `rel="noopener noreferrer"` en todos los links externos |
| Información mínima expuesta | Sin datos sensibles en el DOM ni en atributos HTML |
| HTML semántico | Estructura clara que reduce superficie de ataque y mejora accesibilidad |
| Atributos `alt` descriptivos | Accesibilidad para lectores de pantalla — protege a usuarios vulnerables |
| Sin dependencias externas de JS | Menor superficie de ataque por bibliotecas de terceros |

---

## Herramientas utilizadas

- **Editor:** Visual Studio Code
- **Control de versiones:** Git + GitHub
- **Fuentes:** Google Fonts (Sora, Source Sans 3)
- **Imágenes de intereses:** [Unsplash](https://unsplash.com) (reemplazables con fotos propias)
- **Sin frameworks:** No se usó Bootstrap, Tailwind, ni ninguna librería de CSS o JavaScript
