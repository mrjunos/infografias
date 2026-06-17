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
| **Animación** | [Motion.dev](https://motion.dev/) | Motor principal de animación — spring physics, scroll-linked, gestures |
| **Renderizado** | React + Vite | Componentes reutilizables del sistema de diseño |
| **Estilos** | Tailwind CSS + CSS Custom Properties | Tokens de diseño y theming dinámico |
| **Tipografía** | Variable Fonts (Google Fonts / local) | Expresividad tipográfica con un solo archivo |
| **Exportación** | html-to-image / Puppeteer | De componente React a PNG/SVG estático |
| **Datos** | JSON / MDX | Separación total entre contenido y presentación |

---

## 🎮 Sistema de Diseño — Principios Fundacionales

### 1. Gamificación del Aprendizaje
Cada infografía aplica al menos **uno** de estos patrones:

- **Progressive Reveal** — la información aparece en capas conforme el usuario interactúa; no todo de golpe.
- **Micro-achievements** — indicadores visuales que premian completar una "lectura" o llegar al final de un scroll.
- **Knowledge Checkpoints** — preguntas cortas o elementos interactivos que confirman comprensión antes de seguir.
- **Streaks & Series** — infografías agrupadas en series temáticas con progreso visual entre episodios.
- **Easter Eggs** — detalles ocultos que recompensan la atención y la curiosidad.

### 2. Técnicas de Sellado del Conocimiento
Inspiradas en ciencias cognitivas y pedagogía:

| Técnica | Implementación visual |
|---------|----------------------|
| **Espaciado (Spaced Repetition)** | Elementos clave reaparecen con variación a lo largo de la pieza |
| **Efecto de Generación** | El usuario completa o predice antes de ver la respuesta |
| **Codificación Dual** | Imagen + texto siempre juntos; nunca uno sin el otro |
| **Chunking** | Información en bloques de máx. 5±2 elementos |
| **Elaborative Interrogation** | Títulos formulados como preguntas que activan el sistema analítico |
| **Principio de Contraste** | Lo más importante rompe el patrón visual para ser recordado |

### 3. Sistema de Color — Paleta Semántica

La paleta no es decorativa; **cada color tiene un rol cognitivo**:

```
🟣 Ultra Violet   #7B2FBE  → Conceptos abstractos, teoría, definiciones
🔵 Electric Blue  #2979FF  → Datos, estadísticas, hechos verificables  
🟢 Neon Mint      #00E5A0  → Acciones, pasos, "qué hacer"
🟡 Solar Yellow   #FFD600  → Atención, advertencias, puntos clave
🔴 Coral Fire     #FF4757  → Errores comunes, mitos, contrastes
⬜ Deep Space     #0D0D1A  → Background base (modo oscuro-first)
🤍 Ghost White    #F0F0FF  → Texto principal sobre fondo oscuro
```

Cada infografía puede tener su **accent color** temático, pero siempre sobre esta base semántica.

### 4. Tipografía — Jerarquía en 4 Niveles

```
Level 1 — HERO      : Variable font, 48–96px, peso 900, tracking tight
Level 2 — SECTION   : 24–36px, peso 700, mayúsculas con letter-spacing
Level 3 — BODY      : 14–16px, peso 400, line-height 1.6, max 65ch
Level 4 — CAPTION   : 11–12px, peso 300, italic, color secundario
```

### 5. Animación con Motion.dev — Filosofía

> "La animación no decora — **guía la atención** y **señala relaciones** entre elementos."

Principios de animación del sistema:

- **Spring first** — usar `type: "spring"` por defecto; curvas de easing solo para micro-interacciones
- **Stagger narrativo** — los elementos aparecen en el orden en que deben leerse
- **Scroll-linked reveals** — cada sección emerge conforme el usuario hace scroll, creando ritmo de lectura
- **Physics = emoción** — alta tensión (stiff spring) para datos impactantes; baja tensión para transiciones suaves
- **Reducir si es necesario** — respetar `prefers-reduced-motion` siempre

```jsx
// Patrón base de reveal para cualquier elemento
<motion.div
  initial={{ opacity: 0, y: 24 }}
  whileInView={{ opacity: 1, y: 0 }}
  transition={{ type: "spring", stiffness: 260, damping: 20 }}
  viewport={{ once: true, margin: "-80px" }}
/>
```

---

## 📁 Estructura del Repositorio

```
infografias/
├── design-system/           # Sistema de diseño base
│   ├── tokens/              # Colores, tipografía, espaciado como JSON/CSS vars
│   ├── components/          # Componentes React reutilizables
│   │   ├── DataCard/
│   │   ├── StatBadge/
│   │   ├── TimelineRow/
│   │   ├── ComparisonGrid/
│   │   └── AnimatedChart/
│   ├── layouts/             # Templates de layout por tipo de infografía
│   │   ├── vertical-scroll/ # Formato story/carrusel
│   │   ├── radial/          # Diagramas circulares / mindmaps
│   │   └── timeline/        # Cronologías y procesos
│   └── motion/              # Variantes de animación reutilizables
│
├── infografias/             # Las piezas publicadas
│   ├── [slug]/
│   │   ├── index.tsx        # Componente de la infografía
│   │   ├── data.json        # Contenido desacoplado
│   │   └── preview.png      # Imagen estática exportada
│   └── ...
│
├── scripts/                 # Automatización
│   ├── export.ts            # HTML → PNG/SVG export
│   └── new-infografia.ts    # CLI para scaffoldear una nueva pieza
│
└── docs/                    # Documentación del sistema de diseño
    ├── PRINCIPLES.md
    ├── COLOR.md
    └── MOTION.md
```

---

## 🚀 Roadmap — Primeras Infografías

- [ ] **Sistema de diseño v0** — tokens, componentes base, motion variants
- [ ] **Infografía #001** — *(tema por definir)*
- [ ] **Template export pipeline** — automatizar PNG/SVG desde componentes
- [ ] **Storybook** — documentación visual del design system
- [ ] **Serie: Aprendizaje Acelerado** — técnicas cognitivas con animación
- [ ] **Serie: Ecosistema IA** — mapa del estado actual de la IA

---

## 🧩 Filosofía de Diseño en Una Frase

> Diseñar para el cerebro, no para la pantalla. Cada pixel tiene que ganar su lugar justificando **por qué ayuda a entender mejor**.

---

*Hecho con Motion.dev, curiosidad sin límite y la convicción de que el conocimiento bien comunicado cambia el mundo.*
