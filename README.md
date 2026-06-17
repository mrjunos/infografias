# 🎨 Infografías — Design System & Knowledge Lab

> Un sistema vivo para crear infografías que no solo informan, sino que **sellan el conocimiento** en quien las ve.

---

## 🧠 La Visión

Este repositorio es dos cosas a la vez:

1. **Una colección de infografías** sobre temas que me apasionan — tecnología, ciencia, aprendizaje, sistemas complejos, diseño, IA y más.
2. **Un sistema de diseño completo** para fabricar esas infografías con coherencia visual, intención pedagógica y animación de alto impacto.

La premisa central: una infografía bien diseñada no es solo estética — es una **herramienta cognitiva**. Cada decisión de color, tipografía, jerarquía y movimiento existe para que el cerebro procese, retenga y conecte información de forma más eficiente.

---

## ⚡ Stack Tecnológico

| Capa | Tecnología | Rol |
|------|-----------|-----|
| **Animación** | [Motion.dev](https://motion.dev/) | Motor principal — spring physics, scroll-linked reveals, gestures |
| **Renderizado** | React 18 + Vite | Componentes reutilizables del sistema de diseño |
| **Estilos** | CSS Custom Properties | Tokens de diseño y theming dinámico (sin librerías externas) |
| **Tipografía** | Bricolage Grotesque · Spectral · JetBrains Mono | Google Fonts CDN; auto-hosteable con `@font-face` |
| **Exportación** | html-to-image / Puppeteer | De componente React a PNG/SVG estático |
| **Contenido** | JSON / MDX | Separación total entre contenido y presentación |

---

## 🎨 Sistema de Diseño — Fundamentos Visuales

### 1. Paleta Semántica — Warm Pastel Edition

La paleta es **semántica**: cada color tiene un **rol cognitivo fijo** y no es decorativa.  
Cada hue tiene tres pasos: `tint` (fondo suave) · `base` (tono de trabajo) · `deep` (texto e ícono).

> **Nota de versión:** la paleta original del repo usaba colores saturados y dark-mode-first (Ultra Violet, Electric Blue, Neon Mint, Solar Yellow, Coral Fire sobre `#0D0D1A`). El design system evolucionó hacia una interpretación **warm pastel** — más elegante, fina y legible en modo claro — preservando los roles cognitivos de cada color.

| Rol | Nombre | Base | Tint | Deep | Cuándo usarlo |
|-----|--------|------|------|------|---------------|
| **Concepto** | Lilac | `#B59ED0` | `#EDE4F4` | `#6E5891` | Ideas abstractas, teoría, definiciones |
| **Dato** | Dusty Blue | `#92ABD0` | `#E4EAF3` | `#4F6489` | Estadísticas, hechos verificables, números |
| **Acción** | Sage | `#A0C4A8` | `#E6F0E6` | `#5C8266` | Pasos, métodos, qué hacer |
| **Atención** | Honey | `#E8C485` | `#F8EFD9` | `#A77F3C` | Puntos clave, advertencias, highlights |
| **Alerta** | Clay Coral | `#DD9A8B` | `#F6E2DC` | `#A65C4C` | Mitos, errores comunes, contrastes |

**Color de marca:** Concepto (lilac) `#B59ED0` / deep `#6E5891`.

**Neutrales cálidos** (nunca grises fríos):

```
--paper:      #FBF7F1   ← fondo primario (ivory cálido)
--surface:    #FFFDFA   ← superficie de tarjeta
--border:     #EBE3D7   ← hairline borders
--ink:        #3B3540   ← texto primario (warm plum-charcoal)
--ink-soft:   #6B636F   ← texto secundario
--ink-faint:  #9A9099   ← captions, disabled, meta
```

**Deep mode** (herencia dark-mode-first, calentado):
```
--deep:   #262029   ← warm "deep space"
--ghost:  #F3EDE4   ← texto sobre deep
```

### 2. Tipografía — Jerarquía en 4 Niveles

| Nivel | Fuente | Tamaño | Peso | Uso |
|-------|--------|--------|------|-----|
| **Hero** | Bricolage Grotesque | clamp(38–76px) | 800 | Títulos principales, números grandes |
| **Section** | Bricolage Grotesque | clamp(22–34px) | 700 | Títulos de sección |
| **Body** | Spectral | 16–17px | 400 | Cuerpo de texto, máx. 65ch |
| **Caption / Label** | JetBrains Mono | 11–12px | 500 | Eyebrows, datos, fuentes, uppercase + wide tracking |

- **Display:** tracking `−0.03em` a tamaños grandes; `text-wrap: balance`.
- **Body:** `line-height: 1.65`, serif cálida para lectura larga.
- **Mono:** `font-variant-numeric: tabular-nums`; siempre acompañado de texto (dual coding).

### 3. Cards y Superficies

- **Superficie:** `#FFFDFA` (surface-card) sobre fondo `#FBF7F1` (paper).
- **Borde:** hairline `1px #EBE3D7`.
- **Radio:** `22px` (lg) para cards grandes, `16px` (md) para chips y columnas, `999px` (pill) para badges.
- **Sombra:** siempre warm-tinted (`rgba(74,58,44,…)`), nunca gris neutro:
  ```
  shadow-sm: 0 2px 6px rgba(74,58,44,.06), 0 1px 2px rgba(74,58,44,.05)
  shadow-md: 0 6px 20px rgba(74,58,44,.08), 0 2px 6px rgba(74,58,44,.05)
  shadow-lg: 0 18px 48px rgba(74,58,44,.12), 0 6px 16px rgba(74,58,44,.06)
  ```
- **Accent edge:** borde izquierdo de 4px en el color semántico del contenido — siempre con significado, nunca decorativo.

### 4. Animación con Motion.dev — Filosofía

> "La animación no decora — **guía la atención** y **señala relaciones** entre elementos."

**Spring-first.** El preset base para todo reveal:

```js
{ type: 'spring', stiffness: 260, damping: 22 }
```

Presets del sistema:
```js
soft:   { type:'spring', stiffness:180, damping:22 }  // transiciones suaves
base:   { type:'spring', stiffness:260, damping:20 }  // reveal estándar
snappy: { type:'spring', stiffness:420, damping:30 }  // datos impactantes
loose:  { type:'spring', stiffness:120, damping:18 }  // cierre / feature card
```

**Scroll-linked reveal** (patrón base de toda infografía):

```jsx
function Reveal({ children, delay = 0, y = 24 }) {
  const ref = React.useRef(null);
  React.useEffect(() => {
    const el = ref.current;
    if (!el || !M.inView || !M.animate) { if (el) { el.style.opacity=1; el.style.transform='none'; } return; }
    const stop = M.inView(el, () => {
      M.animate(el,
        { opacity:[0,1], transform:[`translateY(${y}px)`,'translateY(0px)'] },
        { type:'spring', stiffness:260, damping:22, delay }
      );
    }, { margin:'-80px' });
    return stop;
  }, []);
  return <div ref={ref} style={{ opacity:0, transform:`translateY(${y}px)` }}>{children}</div>;
}
```

**Reglas:**
- **Stagger narrativo** — elementos aparecen en el orden de lectura; `delay` incremental de ~0.05–0.1s.
- **Alta tensión para datos** (stiffness alto) — baja tensión para transiciones suaves.
- **Siempre respetar `prefers-reduced-motion`** — collapsar duraciones a 0ms, mostrar estado final.
- **Easing curves solo para micro-interacciones** (hover, press), nunca para reveals de contenido.

**Hover/press:**
- Botones primary: `base → deep` + shadow en hover; `scale(0.97)` en press.
- Cards interactivas: `translateY(-2px)` en hover, shadow sube de sm a md.

### 5. Iconografía

No hay icon set bundled. El sistema usa:
- **Glifos geométricos:** `●◎ ◐` para el seal mark de marca y conceptos
- **Unicode tipográfico:** `✓ ✕ → ↓` para grids de contraste y navegación
- **Dual coding siempre:** un ícono nunca aparece solo — siempre junto a texto

Para sets más ricos: **Lucide** via CDN (stroke 1.5–2px, rounded) — tono cálido y fino.

### 6. Principios de Contenido

- **Idioma:** español, con términos técnicos en inglés donde es el estándar del campo.
- **Voz:** segunda persona, directa y cálida. Los títulos son preguntas cuando activan el sistema analítico.
- **Casing:** sentence case para headlines y body. UPPERCASE solo para eyebrows/labels con `letter-spacing: 0.14em`.
- **Sin emoji** en las piezas publicadas.
- **Números como personajes:** estadísticas grandes van en display font con la unidad en accent color.
- **Chunking:** máx. 5±2 ideas por sección, oraciones cortas, espacio generoso entre bloques.

---

## 🎮 Sistema de Diseño — Principios Pedagógicos

### Gamificación del Aprendizaje

Cada infografía aplica al menos uno de estos patrones:

- **Progressive Reveal** — la información aparece en capas conforme el usuario hace scroll.
- **Micro-achievements** — indicadores visuales al completar una sección o llegar al final.
- **Knowledge Checkpoints** — el usuario predice antes de ver la respuesta (efecto de generación).
- **Streaks & Series** — infografías agrupadas en series con progreso visual entre episodios.
- **Easter Eggs** — detalles ocultos que recompensan la atención.

### Técnicas de Sellado del Conocimiento

| Técnica | Implementación visual |
|---------|----------------------|
| **Codificación Dual** | Imagen + texto siempre juntos; el ícono acompaña al título de cada DataCard |
| **Efecto de Generación** | Checkpoints: el usuario responde antes de ver la respuesta |
| **Principio de Contraste** | ComparisonGrid: mito vs. realidad, antes vs. después |
| **Chunking** | Máx. 5±2 items por sección o lista |
| **Espaciado** | La estructura en series con episodios numerados |
| **Interrogación Elaborativa** | Títulos formulados como preguntas |

---

## 📁 Estructura del Repositorio

```
infografias/
├── design-system/           # Sistema de diseño base (próximo)
│   ├── tokens/              # CSS Custom Properties (colors, type, spacing, effects, fonts)
│   ├── components/          # Componentes React reutilizables
│   │   ├── core/            # Badge, Button, Card
│   │   └── infographic/     # StatBadge, DataCard, TimelineRow, ComparisonGrid,
│   │                        # Checkpoint, ProgressDots, DeltaExplainer
│   ├── layouts/             # Templates de layout
│   └── motion/              # Variantes de animación reutilizables
│
├── infografias/             # Las piezas publicadas
│   └── manifestacion/
│       └── index.html       # Infografía #001 — Manifestación (standalone HTML)
│
├── scripts/                 # Automatización (exportación, scaffolding)
└── docs/                    # Documentación del sistema
    ├── PRINCIPLES.md
    ├── COLOR.md
    └── MOTION.md
```

---

## 🗂️ Infografías publicadas

| # | Título | Serie | Archivo |
|---|--------|-------|---------|
| 01 | Manifestación: la ciencia detrás del deseo | Aprendizaje Acelerado | [`infografias/manifestacion/`](infografias/manifestacion/index.html) |

---

## 🚀 Roadmap

- [x] **Infografía #001** — Manifestación: la ciencia detrás del deseo
- [ ] **Design system v0** — tokens como archivos CSS, componentes React formales
- [ ] **Template export pipeline** — PNG/SVG desde componentes React
- [ ] **Storybook** — documentación visual interactiva del design system
- [ ] **Infografía #002** — Espaciado óptimo y memoria a largo plazo
- [ ] **Serie: Ecosistema IA** — mapa del estado actual de la IA

---

## 🧩 Filosofía de Diseño en Una Frase

> Diseñar para el cerebro, no para la pantalla. Cada pixel tiene que ganar su lugar justificando **por qué ayuda a entender mejor**.

---

*Hecho con Motion.dev, curiosidad sin límite y la convicción de que el conocimiento bien comunicado cambia el mundo.*
