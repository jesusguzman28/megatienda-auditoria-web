# 🛒 MegaTienda: laboratorio de calidad de experiencia web

> **Curso:** Calidad de Software
> **Tema:** Calidad de experiencia web: WCAG, heurísticas de Nielsen, Core Web Vitals y accesibilidad
> **Duración sugerida:** 2 a 3 horas (una sesión de laboratorio)
> **Modalidad:** individual o en grupos de 3 a 5 personas

---

## ⚠️ Antes de empezar: lee esto

La página `index.html` de este proyecto **está mal hecha a propósito**.

Es una tienda en línea ficticia, *MegaTienda*, construida con **decenas de errores intencionales** de:

- **Rendimiento:** tarda en cargar, se congela y los elementos "saltan".
- **Accesibilidad:** personas ciegas, con baja visión, daltonismo o que solo usan teclado **no pueden usarla bien**.
- **Usabilidad:** confunde, no avisa lo que pasa y deja que cometas errores graves.

**Tu trabajo es ser el auditor.** Tienes que encontrar la mayor cantidad posible de problemas, **medirlos, clasificarlos y priorizarlos**, como lo haría un equipo de QA real antes de salir a producción.

> 💡 **No corrijas el código** (salvo que tu docente lo pida como actividad extra). La meta de esta sesión es **encontrar, justificar y priorizar**, no arreglar.

---

## 🎯 Objetivo de aprendizaje

Al finalizar la sesión, podrás:

1. **Auditar** una interfaz web según las pautas **WCAG 2.2** y las **10 heurísticas de Nielsen**.
2. **Medir** los **Core Web Vitals** (LCP, INP, CLS) e interpretar los resultados.
3. **Priorizar** los hallazgos según su severidad e impacto.
4. **Ponerte en el lugar** de usuarios con discapacidad y de usuarios con conexiones o equipos lentos.

---

## 📁 Archivos del proyecto

```
fff/
├── index.html                                ← La página "mala" que vas a auditar (todo en un solo archivo HTML)
├── README.md                                 ← Esta guía
└── Plantilla_Informe_Auditoria_MegaTienda.docx ← 📝 El informe que debes LLENAR y entregar
```

> 📝 **No tienes que armar el informe desde cero.** Abre `Plantilla_Informe_Auditoria_MegaTienda.docx` en Word y llénalo sección por sección mientras haces las actividades. Las **celdas amarillas** son para escribir, las **cajas azules** te explican qué hacer y ☐ se marca como ☒.

La página usa **solo HTML**, con el CSS y el JavaScript dentro del mismo archivo. No hace falta instalar Node, frameworks ni bases de datos.

> 🌐 **Se necesita internet:** la página descarga imágenes y fuentes de servidores externos (eso también es parte del problema de rendimiento).

---

## 🧰 Requisitos

| Herramienta | ¿Obligatoria? | Para qué sirve | Dónde conseguirla |
|---|---|---|---|
| **Google Chrome** (o Edge) | ✅ Sí | Abrir la página y usar DevTools/Lighthouse | https://www.google.com/chrome |
| **Lighthouse** | ✅ Sí (ya viene en Chrome) | Medir rendimiento y accesibilidad | DevTools → pestaña *Lighthouse* |
| **axe DevTools** (extensión) | ✅ Recomendada | Detectar errores de accesibilidad | Chrome Web Store → "axe DevTools" |
| **WAVE** (extensión) | ✅ Recomendada | Ver los errores de accesibilidad dibujados sobre la página | Chrome Web Store → "WAVE Evaluation Tool" |
| **NVDA** (lector de pantalla) | ⭐ Opcional | Escuchar la página como una persona ciega | https://www.nvaccess.org (gratis, Windows) |
| **Narrador de Windows** | ⭐ Alternativa a NVDA | Lector de pantalla que ya viene en Windows | `Ctrl + Win + Enter` |
| **VoiceOver** | ⭐ Si usas Mac | Lector de pantalla de macOS | `Cmd + F5` |
| **VS Code + Live Server** | ⭐ Opcional | Servir la página localmente | Extensión "Live Server" |
| **Python** | ⭐ Opcional | Otra forma de servir la página | https://www.python.org |

---

## 🚀 Cómo abrir la página

### ⭐ Opción rápida: la página ya está publicada

👉 **https://jesusguzman28.github.io/megatienda-auditoria-web/**

Ábrela en Chrome y ya puedes usar **Lighthouse** (F12 → Lighthouse) y **PageSpeed Insights**:
👉 https://pagespeed.web.dev/analysis?url=https://jesusguzman28.github.io/megatienda-auditoria-web/

Si prefieres trabajar con tu propia copia, usa las opciones A, B o C.

### Opción A: doble clic (la más fácil)

1. Descarga o clona esta carpeta.
2. Haz **doble clic** en `index.html`.
3. Se abrirá en tu navegador con una dirección parecida a `file:///C:/Users/.../index.html`.

✔️ Sirve para explorar la página y hacer la evaluación heurística.
⚠️ **Para medir con Lighthouse es mejor usar la opción B o C**, porque algunas métricas no se miden bien con `file://`.

### Opción B: VS Code + Live Server (recomendada)

1. Abre la carpeta en VS Code.
2. Instala la extensión **Live Server** (de Ritwick Dey).
3. Clic derecho en `index.html` → **"Open with Live Server"**.
4. Se abrirá `http://127.0.0.1:5500/index.html`.

### Opción C: servidor de Python

Abre una terminal **dentro de la carpeta** del proyecto y ejecuta:

```bash
python -m http.server 8000
```

Luego abre en Chrome: **http://localhost:8000**

Para detener el servidor presiona `Ctrl + C` en la terminal.

### Opción D (extra): publicar tu propia copia en internet

**PageSpeed Insights** (https://pagespeed.web.dev) solo funciona con páginas públicas. Puedes usar el enlace de la opción rápida o subir tu propia copia gratis a:

- **Netlify Drop:** https://app.netlify.com/drop (arrastras la carpeta y listo)
- **GitHub Pages:** subes el repositorio y activas Pages en *Settings → Pages*

---

## 📚 Conceptos clave (repaso rápido)

### 1. WCAG: Pautas de Accesibilidad para el Contenido Web

Las WCAG (*Web Content Accessibility Guidelines*) son el estándar internacional de accesibilidad web, publicado por el W3C. La versión actual es la **2.2**.

Se organizan en **4 principios**, que se recuerdan con la sigla **POUR** (en español, **POCR**):

| Principio | Pregunta clave | Ejemplo de falla |
|---|---|---|
| **P**erceptible | ¿Todos pueden **percibir** el contenido? | Imagen sin texto alternativo; texto gris claro sobre blanco |
| **O**perable | ¿Todos pueden **usar** la interfaz? | Un botón que no funciona con teclado |
| **U**nderstandable (Comprensible) | ¿Todos pueden **entender** el contenido? | Mensajes de error como "ERR_0x8F" |
| **R**obusto | ¿Funciona con **tecnologías de apoyo**? | Un `<div>` que actúa como botón pero el lector de pantalla no lo anuncia |

Cada criterio tiene un **nivel de conformidad**:

| Nivel | Significado |
|---|---|
| **A** | Lo mínimo. Si falla, algunas personas **no pueden** usar la página. |
| **AA** | El nivel que exigen la mayoría de leyes y empresas. **Es la meta habitual.** |
| **AAA** | El nivel más alto; no siempre es posible cumplirlo en todo el sitio. |

📖 Referencia rápida oficial: https://www.w3.org/WAI/WCAG22/quickref/

### 2. Las 10 heurísticas de Nielsen

Son 10 principios generales de usabilidad propuestos por **Jakob Nielsen** (1994). Se usan para hacer una **evaluación heurística**: expertos revisan la interfaz y anotan dónde se rompe cada principio.

| # | Heurística | En palabras simples |
|---|---|---|
| H1 | **Visibilidad del estado del sistema** | El sistema siempre me dice qué está pasando (cargando, guardado, error). |
| H2 | **Relación entre el sistema y el mundo real** | Habla mi idioma, no el del programador. |
| H3 | **Control y libertad del usuario** | Puedo deshacer, cancelar o salir fácilmente. |
| H4 | **Consistencia y estándares** | Lo mismo se ve y se llama igual en toda la página. |
| H5 | **Prevención de errores** | El diseño evita que me equivoque (sobre todo en acciones graves). |
| H6 | **Reconocer antes que recordar** | No me obliga a memorizar cosas; me las muestra. |
| H7 | **Flexibilidad y eficiencia de uso** | Sirve tanto para novatos como para expertos (atajos, filtros). |
| H8 | **Diseño estético y minimalista** | Sin ruido: solo lo que necesito. |
| H9 | **Ayudar a reconocer, diagnosticar y recuperarse de errores** | Los errores dicen qué pasó y cómo solucionarlo. |
| H10 | **Ayuda y documentación** | Si necesito ayuda, la encuentro fácilmente. |

📖 Artículo original: https://www.nngroup.com/articles/ten-usability-heuristics/

### 3. Core Web Vitals

Son las **3 métricas de Google** que miden la experiencia real de carga, interactividad y estabilidad visual:

| Métrica | Qué mide | Pregunta del usuario | 🟢 Bueno | 🟡 Mejorable | 🔴 Malo |
|---|---|---|---|---|---|
| **LCP** (*Largest Contentful Paint*) | Cuánto tarda en aparecer el **elemento más grande** (imagen o texto principal) | "¿Ya cargó?" | ≤ 2.5 s | 2.5 – 4 s | > 4 s |
| **INP** (*Interaction to Next Paint*) | Cuánto tarda la página en **responder** cuando haces clic o escribes | "¿Me hizo caso?" | ≤ 200 ms | 200 – 500 ms | > 500 ms |
| **CLS** (*Cumulative Layout Shift*) | Cuánto **se mueven** los elementos mientras carga | "¿Por qué se movió el botón?" | ≤ 0.1 | 0.1 – 0.25 | > 0.25 |

Métricas de apoyo que también verás en Lighthouse:

| Métrica | Qué mide |
|---|---|
| **FCP** (*First Contentful Paint*) | Cuándo aparece **lo primero** en pantalla |
| **TBT** (*Total Blocking Time*) | Cuánto tiempo el hilo principal estuvo **bloqueado** (en el laboratorio sirve como aproximación del INP) |
| **Speed Index** | Qué tan rápido se "llena" visualmente la pantalla |
| **TTFB** (*Time To First Byte*) | Cuánto tarda el servidor en empezar a responder |

> 📝 **Importante:** Lighthouse, en su modo normal, **no mide INP**, porque nadie hace clic durante la prueba. Por eso muestra **TBT**. Para medir INP de verdad tienes que **interactuar tú** con la página (ver Actividad 2).

📖 Más información: https://web.dev/articles/vitals

---

## 🧪 Actividades paso a paso

> ⏱️ Los tiempos son una guía. Anota **todo** lo que encuentres en la [plantilla de hallazgos](#-plantilla-de-hallazgos).

### 🟦 Actividad 0: primera impresión (5 min)

Abre la página **como un usuario normal**, sin herramientas. Intenta:

1. Comprar la **cámara vintage**.
2. Buscar "laptop" en el buscador.
3. Registrarte con tus datos.
4. Averiguar cuánto cuesta el envío a provincias.
5. Encontrar la ayuda.

Anota tus **sensaciones**: ¿qué te molestó?, ¿qué no entendiste?, ¿en qué momento pensaste en irte a otra tienda?

---

### 🟩 Actividad 1: medir con Lighthouse (20 min)

1. Abre la página (preferiblemente con la **opción B o C**).
2. Abre una **ventana de incógnito** (`Ctrl + Shift + N`), para que las extensiones no alteren la medición.
3. Abre DevTools: `F12` o `Ctrl + Shift + I` (en Mac: `Cmd + Opt + I`).
4. Ve a la pestaña **Lighthouse** (si no la ves, búscala en el menú `»`).
5. Configura:
   - **Mode:** `Navigation`
   - **Device:** primero `Mobile`, después repite con `Desktop`
   - **Categories:** marca `Performance`, `Accessibility` y `Best practices`
6. Haz clic en **"Analyze page load"** y espera.
7. Anota los resultados en esta tabla:

| Métrica | Mobile | Desktop | ¿🟢 / 🟡 / 🔴? |
|---|---|---|---|
| Puntaje de Performance | | | |
| Puntaje de Accessibility | | | |
| FCP | | | |
| LCP | | | |
| TBT | | | |
| CLS | | | |
| Speed Index | | | |

8. Baja hasta **"Diagnostics"** y **"Opportunities"**. Anota al menos **5 problemas** que reporta Lighthouse y, con tus palabras, **explica por qué afectan al usuario**.
9. En la sección de LCP, busca **"Largest Contentful Paint element"**: ¿qué elemento es? ¿Por qué tarda tanto?
10. En la sección de CLS, busca **"Avoid large layout shifts"**: ¿qué elementos se mueven?

> 💡 **Tip:** repite la medición 2 o 3 veces. Los resultados cambian un poco cada vez; usa el valor intermedio (la mediana).

---

### 🟨 Actividad 2: medir INP y ver los "congelamientos" (15 min)

Lighthouse no mide INP en modo navegación, así que lo vas a medir tú:

**Método 1: métricas en vivo (el más fácil)**

1. DevTools → pestaña **Performance**.
2. Verás un panel con **"Local metrics"**: LCP, CLS e INP en tiempo real.
3. Interactúa con la página: haz clic en los botones de compra, escribe en el buscador, envía el formulario.
4. Observa cómo cambia el **INP**. ¿Qué interacción es la peor? ¿Cuántos milisegundos tarda?

**Método 2: grabar una traza**

1. Pestaña **Performance** → botón **Record** (⏺).
2. Haz clic en "Comprar" y escribe algo en el buscador.
3. Detén la grabación.
4. Busca los bloques con **triángulo rojo** en la fila *Main*: son **tareas largas** (*long tasks*, más de 50 ms).
5. Haz clic en una y mira en la parte de abajo qué función de JavaScript la causa.

**Método 3: Lighthouse en modo Timespan**

1. Lighthouse → **Mode: `Timespan`** → **Start timespan**.
2. Interactúa con la página por 20 segundos.
3. **End timespan** y revisa el INP y el TBT.

❓ **Pregunta:** aunque no hagas nada, ¿la página se "traba" sola? Graba 10 segundos **sin tocar nada** y revisa si hay tareas largas. ¿Qué crees que las provoca?

---

### 🟥 Actividad 3: empatía con conexiones y equipos lentos (15 min)

No todos tienen fibra óptica y una computadora gamer. Muchas personas navegan con **datos móviles 3G/4G** y **celulares de gama baja**.

1. DevTools → pestaña **Network** → cambia **"No throttling"** por **"Slow 4G"** y luego por **"3G"**.
2. Marca **"Disable cache"**.
3. Recarga la página (`Ctrl + Shift + R`).
4. Ahora ve a **Performance** → ⚙️ (engranaje) → **CPU: 6x slowdown** (simula un celular barato).
5. Vuelve a intentar las tareas de la Actividad 0.

Anota:

- ¿Cuántos **segundos** pasaron hasta que pudiste ver algo útil?
- ¿Cuántos **MB** descargó la página? (mira la barra inferior de la pestaña Network: *transferred*)
- ¿Qué archivo pesa más? ¿Tiene sentido que pese tanto para mostrarse en un cuadrito pequeño?
- Si pagaras tus datos móviles por MB, ¿cuánto te costaría abrir esta página?

> 🧠 **Reflexiona:** una persona que vive en una zona rural con mala señal, ¿podría comprar en esta tienda?

---

### 🟪 Actividad 4: accesibilidad con herramientas automáticas (20 min)

1. **Lighthouse → Accessibility:** revisa la lista de fallas.
2. **axe DevTools:** DevTools → pestaña **axe DevTools** → **Scan all of my page**.
   - Anota cada problema, su **impacto** (*critical, serious, moderate, minor*) y el **criterio WCAG** que indica.
3. **WAVE:** haz clic en el ícono de WAVE en la barra del navegador.
   - Los íconos **rojos** son errores; los **amarillos**, alertas.
   - Revisa la pestaña **"Contrast"** para ver los errores de contraste.
   - Revisa **"Structure"** para ver la jerarquía de encabezados (h1, h2...).

> ⚠️ **Muy importante:** las herramientas automáticas detectan solo una **parte** de los problemas de accesibilidad (se estima que entre el **30 % y el 40 %**). **Una página con 100 en Lighthouse puede ser inaccesible.** Por eso existe la Actividad 5.

---

### 🟫 Actividad 5: accesibilidad manual, ponte en sus zapatos (30 min)

#### 5.1 ⌨️ Solo teclado (personas con discapacidad motriz o que no pueden usar mouse)

**Desconecta o no toques el mouse.** Usa solo:

| Tecla | Acción |
|---|---|
| `Tab` | Ir al siguiente elemento |
| `Shift + Tab` | Ir al anterior |
| `Enter` | Activar enlace o botón |
| `Espacio` | Activar botón o casilla |
| `Esc` | Cerrar ventanas emergentes |

Intenta:

- [ ] ¿Puedes ver **dónde** está el foco en cada momento?
- [ ] ¿El orden del foco es **lógico** (de arriba hacia abajo, de izquierda a derecha)?
- [ ] ¿Puedes **comprar** un producto?
- [ ] ¿Puedes usar el **menú** superior?
- [ ] ¿Puedes **enviar** el formulario?
- [ ] Cuando aparece la ventana de **newsletter**, ¿puedes cerrarla?

#### 5.2 🔊 Lector de pantalla (personas ciegas)

1. Activa **NVDA** o el **Narrador** (`Ctrl + Win + Enter`).
2. Cierra los ojos o tapa la pantalla.
3. Navega con `Tab` y con las flechas.
4. Con NVDA, presiona `H` para saltar entre encabezados y `Insert + F7` para ver la lista de enlaces.

Preguntas:

- ¿Qué dice el lector cuando llega a una **imagen de producto**?
- ¿Anuncia los botones de compra como **"botón"**?
- En la lista de enlaces, ¿se entiende a dónde lleva cada uno?
- ¿Qué pasa con el **captcha**?
- ¿En qué **idioma** pronuncia el texto? ¿Lo pronuncia bien?

#### 5.3 🔍 Zoom y baja visión

1. Presiona `Ctrl` + `+` hasta llegar al **200 %** y luego al **400 %**.
   - ¿Aparece una **barra de desplazamiento horizontal**? ¿Se corta el contenido?
2. Abre DevTools → **Toggle device toolbar** (`Ctrl + Shift + M`) → elige un celular (por ejemplo, iPhone SE).
   - ¿La página se adapta a la pantalla? ¿Se puede hacer zoom con los dedos?
3. Mide el **contraste** de algunos textos:
   - DevTools → selecciona el texto con la herramienta de inspección (`Ctrl + Shift + C`) → en el panel **Styles** haz clic en el cuadrito de color → verás el **"Contrast ratio"**.
   - O usa https://webaim.org/resources/contrastchecker/
   - La WCAG AA pide al menos **4.5:1** para texto normal y **3:1** para texto grande.

#### 5.4 🎨 Daltonismo y otras condiciones visuales

1. DevTools → `Ctrl + Shift + P` → escribe **"Rendering"** → abre la pestaña.
2. Busca **"Emulate vision deficiencies"** y prueba:
   - `Protanopia` (no distingue el rojo)
   - `Deuteranopia` (no distingue el verde)
   - `Achromatopsia` (no ve colores)
   - `Blurred vision` (visión borrosa)
3. Envía el formulario **vacío**. Con cada simulación, ¿puedes saber **qué campo** tiene error?

#### 5.5 🧠 Discapacidad cognitiva, atención y movimiento

- ¿Hay cosas que se **mueven solas** o **parpadean**? ¿Se pueden detener?
- ¿Hay algún **límite de tiempo**? ¿Qué pasa cuando llega a cero? (pista: llena el formulario y espera… mira abajo del todo)
- ¿Los textos son claros o usan **jerga técnica**?

---

### 🟧 Actividad 6: evaluación heurística de Nielsen (30 min)

1. **Individual (15 min):** recorre la página **heurística por heurística** (H1 a H10). Para cada una, busca al menos **un** problema.
2. **En grupo (15 min):** junten sus listas, **eliminen duplicados** y pónganse de acuerdo en la severidad.

> 📊 **Dato:** Nielsen demostró que **un solo evaluador** encuentra en promedio solo el **35 %** de los problemas, y que **entre 3 y 5 evaluadores** encuentran alrededor del **75 %**. ¡Por eso se trabaja en grupo!

Preguntas guía por heurística:

| Heurística | Preguntas guía |
|---|---|
| H1 Estado del sistema | Al agregar al carrito, ¿te enteras? ¿La barra de carga dice cuánto falta? |
| H2 Mundo real | ¿Entiendes todos los textos? ¿Hay palabras técnicas o en otro idioma? |
| H3 Control y libertad | ¿Puedes quitar productos del carrito? ¿Puedes cerrar fácilmente las ventanas emergentes? |
| H4 Consistencia | ¿Todos los botones de compra se ven y se llaman igual? |
| H5 Prevención de errores | ¿Qué botón está al lado de "Enviar"? ¿Te pide confirmación? ¿El formato de la fecha es claro? |
| H6 Reconocer vs. recordar | ¿Algún campo te pide recordar algo que ya no ves en pantalla? |
| H7 Flexibilidad | ¿El buscador tiene filtros o sugerencias? ¿Hay atajos? |
| H8 Minimalismo | ¿Cuántos elementos compiten por tu atención al mismo tiempo? |
| H9 Recuperarse de errores | ¿Los mensajes de error explican **qué** pasó y **cómo** solucionarlo? |
| H10 Ayuda | ¿Encontraste ayuda útil? |

---

### ⬛ Actividad 7: priorizar los hallazgos (20 min)

Encontrar problemas es solo la mitad del trabajo. **En un proyecto real no hay tiempo para arreglar todo a la vez**, así que hay que decidir **qué se arregla primero**.

#### Paso 1: asigna la severidad (escala de Nielsen)

| Nivel | Nombre | Significado |
|---|---|---|
| **0** | No es problema | No estoy de acuerdo con que sea un problema |
| **1** | Cosmético | Se arregla solo si sobra tiempo |
| **2** | Menor | Prioridad baja |
| **3** | Mayor | Importante; prioridad alta |
| **4** | Catastrófico | **Hay que arreglarlo antes de lanzar**; impide completar la tarea |

La severidad depende de 3 factores:

- **Frecuencia:** ¿pasa seguido o raramente?
- **Impacto:** ¿el usuario puede superarlo o se queda bloqueado?
- **Persistencia:** ¿se supera una vez o molesta siempre?

> 🦽 **Regla práctica para accesibilidad:** si un problema **impide por completo** que un grupo de personas complete una tarea (por ejemplo, alguien que solo usa teclado no puede comprar), es **severidad 4**, aunque "la mayoría" de usuarios no lo note.

#### Paso 2: estima el esfuerzo de corrección

| Esfuerzo | Ejemplo |
|---|---|
| **Bajo** | Agregar un atributo (`alt`, `lang`, `<label>`), cambiar un color |
| **Medio** | Cambiar `<div>` por `<button>` en varios lugares, rediseñar mensajes de error |
| **Alto** | Rehacer la estrategia de carga, cambiar el diseño de toda la página |

#### Paso 3: ubica cada hallazgo en la matriz impacto/esfuerzo

```
                    ESFUERZO
                 Bajo          Alto
            ┌─────────────┬─────────────┐
      Alto  │ 1️⃣ HACER YA  │ 2️⃣ PLANIFICAR│
 IMPACTO    │ (quick wins) │ (proyectos) │
            ├─────────────┼─────────────┤
      Bajo  │ 3️⃣ SI HAY    │ 4️⃣ DESCARTAR │
            │   TIEMPO     │  / POSPONER │
            └─────────────┴─────────────┘
```

#### Paso 4: arma tu **Top 10**

Ordena tus hallazgos y elige los **10 más urgentes**. Justifica cada posición en una línea.

---

## 📝 Plantilla de hallazgos

Copia esta tabla en Excel, Google Sheets o Word y llénala:

| ID | Ubicación en la página | Descripción del problema | Tipo | Criterio WCAG / Heurística / Métrica | Usuarios afectados | Evidencia | Severidad (0-4) | Esfuerzo (B/M/A) | Recomendación |
|---|---|---|---|---|---|---|---|---|---|
| H-01 | | | | | | | | | |

**Ejemplo resuelto** (este puedes usarlo; ¡los demás los encuentras tú!):

| Campo | Ejemplo |
|---|---|
| **ID** | H-01 |
| **Ubicación** | Etiqueta `<html>` (inicio del código) |
| **Descripción** | La página no declara su idioma. |
| **Tipo** | Accesibilidad |
| **Criterio** | WCAG 3.1.1 Idioma de la página (Nivel A) |
| **Usuarios afectados** | Personas ciegas que usan lector de pantalla: el lector puede leer el texto en español con pronunciación de inglés y volverlo incomprensible. |
| **Evidencia** | Captura de Lighthouse: *"`<html>` element does not have a `[lang]` attribute"*. |
| **Severidad** | 3 (Mayor) |
| **Esfuerzo** | Bajo |
| **Recomendación** | Cambiar `<html>` por `<html lang="es">`. |

### ¿Qué cuenta como buena "evidencia"?

- 📸 Captura de pantalla (marcando el problema con un recuadro).
- 📊 Captura del reporte de Lighthouse / axe / WAVE.
- 🔢 Números medidos: "El LCP fue 8.4 s en Mobile".
- 🎥 Video o GIF corto (por ejemplo, mostrando cómo el foco "desaparece").
- 💬 Cita textual: "El error dice: `ERR_VALIDATION_0x8F`".

---

## 📦 Entregable

La **plantilla de Word llena** (`Plantilla_Informe_Auditoria_MegaTienda.docx`), guardada como `Grupo_N_Auditoria_MegaTienda.docx` o en PDF. La plantilla ya trae todas estas partes:

1. **Portada:** nombres del equipo, fecha y herramientas usadas.
2. **Resumen ejecutivo** (máximo media página): ¿cuál es el estado general de la página? ¿Se puede lanzar así?
3. **Resultados de medición:** tablas de Lighthouse (Mobile y Desktop) y Core Web Vitals.
4. **Tabla de hallazgos** completa (usando la plantilla).
5. **Top 10 priorizado** con la matriz impacto/esfuerzo.
6. **Reflexión de empatía** (ver preguntas abajo).
7. **Conclusiones.**

### Rúbrica sugerida

| Criterio | Peso | Excelente | Suficiente | Insuficiente |
|---|---|---|---|---|
| Cantidad y variedad de hallazgos | 20 % | 25 o más, de rendimiento, accesibilidad y usabilidad | 15-24 | Menos de 15 o de un solo tipo |
| Correcta clasificación (WCAG / Nielsen / CWV) | 20 % | Todos con criterio correcto y nivel | Algunos errores | Sin clasificar o mal clasificados |
| Evidencia y medición | 20 % | Capturas y números en todos | En algunos | Sin evidencia |
| Priorización justificada | 20 % | Severidad + esfuerzo + matriz coherentes | Severidad sin justificar | Sin priorizar |
| Recomendaciones | 10 % | Concretas y técnicamente correctas | Generales | Ausentes |
| Reflexión de empatía | 10 % | Profunda, conecta con usuarios reales | Superficial | Ausente |

---

## 💭 Preguntas de reflexión (empatía)

Responde en tu informe:

1. ¿Qué **tarea** no pudiste completar usando **solo el teclado**? ¿Cómo te sentiste?
2. Escuchando el **lector de pantalla**, ¿cuál fue el momento más frustrante?
3. Con la conexión **3G**, ¿cuánto esperaste? ¿Habrías esperado ese tiempo en la vida real?
4. En el Perú y en Latinoamérica, millones de personas tienen alguna discapacidad y muchas más navegan con planes de datos limitados. ¿A cuántos clientes **pierde** MegaTienda por estos problemas?
5. Muchos de estos problemas se arreglan con **una línea de código**. ¿Por qué crees que siguen apareciendo en sitios reales?
6. ¿Quién es responsable de la accesibilidad en un equipo: el diseñador, el programador, QA o todos? Justifica.

---

## 🧭 Consejos y errores comunes

- ✅ **Describe el impacto en el usuario**, no solo el error técnico. Mal: *"Falta alt"*. Bien: *"Una persona ciega no sabe qué producto está comprando porque la imagen no tiene texto alternativo"*.
- ✅ **Un hallazgo por fila.** Si 6 imágenes no tienen `alt`, es **un** hallazgo que afecta a 6 elementos, no 6 hallazgos distintos.
- ✅ **Un mismo problema puede violar WCAG y Nielsen a la vez.** Anótalo una vez e indica ambos criterios.
- ✅ **Mira el código fuente** (`Ctrl + U`) o inspecciona los elementos (`F12`). Muchos problemas solo se ven ahí.
- ❌ **No confíes solo en Lighthouse.** Un 100 no significa "accesible".
- ❌ **No midas con extensiones activas**: pueden empeorar el rendimiento. Usa incógnito.
- ❌ **No te quedes en la parte de arriba**: ¡baja hasta el pie de página!
- ⏳ **Espera unos 10 segundos** en la página: algunas cosas aparecen con retraso.

---

## ❓ Preguntas frecuentes

**La página se queda en blanco o "congelada" unos segundos al abrir. ¿Está rota?**
No, es intencional. Es parte de lo que tienes que detectar y explicar. 😉

**Las imágenes no cargan.**
Revisa tu conexión a internet: las imágenes vienen de `picsum.photos`. Si tu red las bloquea, igual puedes hacer casi todo el laboratorio; anótalo en tu informe.

**No encuentro la pestaña Lighthouse.**
En DevTools, haz clic en `»` (más pestañas). Si usas otro navegador, cámbiate a Chrome o Edge.

**Me salió un puntaje distinto al de mi compañero.**
Es normal: depende de tu computadora, tu red y lo que tengas abierto. Por eso se recomienda medir varias veces y usar la mediana.

**Lighthouse no me muestra INP.**
Correcto: en modo *Navigation* muestra TBT en su lugar. Revisa la Actividad 2.

**Me apareció una ventana de "alerta" del navegador.**
Ciérrala con "Aceptar". También es parte de lo que se evalúa (¿ayuda de verdad?).

**¿Puedo modificar el `index.html`?**
Para la auditoría, **no**. Si tu docente propone la actividad extra de corrección, haz una **copia** (`index-corregido.html`) y compara los puntajes de antes y después.

---

## 🏆 Reto extra (opcional)

1. Haz una copia del archivo: `index-corregido.html`.
2. Corrige los problemas de tu **Top 10**.
3. Vuelve a medir con Lighthouse y axe.
4. Presenta una tabla **antes vs. después**:

| Métrica | Antes | Después | Mejora |
|---|---|---|---|
| Performance | | | |
| Accessibility | | | |
| LCP | | | |
| CLS | | | |
| TBT / INP | | | |
| Errores axe | | | |

---

## 📖 Glosario

| Término | Significado |
|---|---|
| **Accesibilidad (a11y)** | Que la web pueda ser usada por **todas** las personas, incluidas las que tienen discapacidad. "a11y" = a + 11 letras + y. |
| **Lector de pantalla** | Programa que lee en voz alta lo que hay en la pantalla (NVDA, JAWS, VoiceOver, TalkBack). |
| **Texto alternativo (`alt`)** | Descripción de una imagen que leen los lectores de pantalla. |
| **Foco** | Indicador del elemento seleccionado cuando navegas con teclado. |
| **Contraste** | Diferencia de luminosidad entre el texto y el fondo. Se expresa como relación, por ejemplo 4.5:1. |
| **ARIA** | Atributos (`aria-label`, `role`, etc.) que dan información extra a las tecnologías de apoyo. *Regla 1 de ARIA: si existe un elemento HTML nativo, úsalo en vez de ARIA.* |
| **HTML semántico** | Usar cada etiqueta para lo que fue creada (`<button>` para botones, `<nav>` para navegación, `<label>` para etiquetas). |
| **Hilo principal (*main thread*)** | Donde el navegador ejecuta JavaScript y dibuja la página. Si está ocupado, la página no responde. |
| **Tarea larga (*long task*)** | Trabajo de JavaScript que ocupa el hilo principal por más de 50 ms. |
| **Recurso bloqueante (*render-blocking*)** | Archivo CSS o JS que el navegador debe descargar antes de poder mostrar la página. |
| **Throttling** | Simular una red o un procesador más lentos. |
| **Layout shift** | Cuando un elemento visible cambia de posición inesperadamente. |
| **Evaluación heurística** | Método de inspección en el que expertos revisan una interfaz contra principios reconocidos. |
| **Dark pattern** | Diseño que manipula al usuario para que haga algo que no quería (por ejemplo, avergonzarlo por rechazar una oferta). |

---

## 🔗 Recursos

- WCAG 2.2 (referencia rápida): https://www.w3.org/WAI/WCAG22/quickref/
- WCAG en español (W3C): https://www.w3.org/Translations/WCAG21-es/
- Heurísticas de Nielsen: https://www.nngroup.com/articles/ten-usability-heuristics/
- Escala de severidad de Nielsen: https://www.nngroup.com/articles/how-to-rate-the-severity-of-usability-problems/
- Core Web Vitals: https://web.dev/articles/vitals
- Documentación de Lighthouse: https://developer.chrome.com/docs/lighthouse
- Verificador de contraste WebAIM: https://webaim.org/resources/contrastchecker/
- Cómo usar NVDA para probar páginas: https://webaim.org/articles/nvda/
- PageSpeed Insights: https://pagespeed.web.dev

---

> 🙌 **Recuerda:** detrás de cada hallazgo hay una persona real que no pudo comprar, informarse o hacer un trámite. **La calidad de software también es inclusión.**
