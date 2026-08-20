# Generador TSP - Diseño Publicitario · IDC

> Aplicación web progresiva (PWA) para la generación del **Trabajo de Suficiencia Profesional (TSP)** del Programa de Estudios de **Diseño Publicitario** del Instituto de Educación Superior Público «Diseño y Comunicación» (IDC).

---

## Descripción

Este generador permite a los egresados del IDC completar un formulario académico paso a paso y descargar su informe TSP en formato **Word (.docx)** con todos los estilos tipográficos institucionales aplicados automáticamente, así como una presentación **PowerPoint (.pptx)** de 15 diapositivas para la sustentación oral ante el Jurado Calificador.

La aplicación funciona **100% offline** una vez cargada, incluye generador de citas **APA 7.ª edición**, asistente de **IA integrado** con sugerencias contextuales por campo, y validación en tiempo real del progreso del formulario.

---

## Características principales

| Característica | Descripción |
|---|---|
| **Formulario guiado en 8 pasos** | Carátula, dedicatoria, resumen, capítulos 1-4, conclusiones y recomendaciones |
| **Exportación Word (.docx)** | Informe completo con carátula institucional, índice, capítulos, referencias APA y firmas |
| **Exportación PPTX (15 slides)** | Presentación 16:9 alineada con la estructura oficial del TSP para sustentación oral |
| **Generador APA 7.ª** | Citas de libro, artículo, web, tesis e IA generativa con inserción directa en campos |
| **Asistente IA integrado** | 3 pestañas por campo: Requisitos, Prompt guiado y Ejemplo adaptado a Diseño Publicitario |
| **Demo data incluido** | Botón "Rellenar con ejemplo" con campaña publicitaria integrada completa |
| **100% Offline** | PWA instalable; funciona sin conexión después de la primera carga |
| **Validación en tiempo real** | Contador de palabras, campos obligatorios, chips de progreso por paso |
| **Autosave** | Persistencia automática en localStorage con namespace por carrera |

---

## Arquitectura técnica

```
index.html                          # Aplicación completa (HTML + CSS + JS inline)
├── Templates embebidos en base64
│   ├── TPL_DOCX_B64              # Plantilla Word institucional IDC
│   └── TPL_PPTX_B64              # Plantilla PowerPoint 15 diapositivas
├── Motor de generación ZIP        # makeZip() - Algoritmo CRC32 puro en JS
├── Motor de generación DOCX       # Construcción OOXML manual (OpenXML)
├── Motor de generación PPTX       # Sustitución posicional <a:t> via JSZip
├── Generador APA 7.ª              # Modal con 5 tipos de fuente
├── Asistente IA                   # _aiBank con sugerencias por campo
├── Validación SCHEMA              # v.required/minWords/maxWords/anio
└── Service Worker                 # Soporte PWA (requiere HTTPS)
```

**Tecnologías:** Vanilla JS, CSS3 con variables, JSZip (CDN), OpenXML manual. Sin frameworks.

---

## Uso

### Opción 1: Abrir directamente

1. Abre `index.html` en cualquier navegador web moderno (Chrome, Firefox, Edge, Safari).
2. Presiona **"⚡ Rellenar con ejemplo"** para cargar el demo de Diseño Publicitario.
3. Edita los campos con tu propia experiencia profesional.
4. Usa el botón **✨ IA** en cada campo para obtener sugerencias contextuales.
5. Descarga el informe en **Word (.docx)** o la presentación en **PPTX**.

### Opción 2: Instalar como PWA

1. Abre `index.html` en un servidor con HTTPS.
2. Haz clic en **"⬇ Instalar app"** (aparece automáticamente en navegadores compatibles).
3. La aplicación se instala como app nativa y funciona offline.

---

## Estructura del formulario (8 pasos)

| Paso | Sección | Contenido |
|:---:|:---|:---|
| 1 | **Carátula · Datos institucionales** | Título, autor(es), DNI, correo, asesor, año, línea de investigación |
| 2 | **Dedicatoria y agradecimiento** | Textos personales |
| 3 | **Resumen ejecutivo · Introducción** | Síntesis profesional (máx. 250 palabras), palabras clave, introducción |
| 4 | **Cap. 1 — Marco Teórico** | Bases teóricas, antecedentes, marco conceptual |
| 5 | **Cap. 2 — Contexto Laboral** | Descripción de la organización, organigrama, manual de funciones |
| 6 | **Cap. 3 — Descripción de la Actividad** | Target/Insight/Objetivo comunicacional, detalles técnicos, 4 fases |
| 7 | **Cap. 4 — Evaluación y Plan de Mejora** | Hallazgos relevantes, plan de mejora |
| 8 | **Conclusiones · Recomendaciones · Referencias** | 3 conclusiones (OE1-OE3), 4 recomendaciones, referencias APA |

---

## Etiquetas del Capítulo 3 (carrera-específicas)

Adaptadas específicamente para el Programa de **Diseño Publicitario**:

**Propósito del proyecto (Slide 9)**
- Target / Perfil del consumidor
- Insight / Investigación de mercado
- Objetivo comunicacional / estratégico

**Detalles técnicos (Slide 10)**
- Concepto creativo
- Estrategia de comunicación
- Medios y canales
- Formatos y piezas
- Elementos gráficos
- Tecnología empleada

**Fases del proceso (Slide 11)**
1. Brief y Conceptualización Creativa
2. Diseño y Desarrollo Gráfico
3. Producción e Implementación
4. Medición y Lanzamiento de Campaña

---

## Demo data incluido

El ejemplo precargado corresponde a una **campaña publicitaria integrada** para el lanzamiento de una marca de café orgánico en Lima Metropolitana, desarrollada en Agencia Creativa Néctar:

- **Concepto creativo:** "Origen que Inspira"
- **Alcance:** 850,000 usuarios en redes sociales
- **Engagement:** 6.2% (vs. 3.8% benchmark sectorial)
- **ROAS:** 4.2:1 en pauta digital
- **Incremento de ventas:** 34%

---

## Archivos del proyecto

```
output/
├── index.html                          # Generador TSP PWA (HTML completo)
├── InformeTSP_DisenioPublicitario.pptx  # Template de 15 diapositivas
├── INFORME_TSP_DisenioPublicitario.docx # Plantilla Word institucional
└── README.md                           # Este archivo
```

---

## Personalización técnica

### Cambiar el coordinador del programa

Busca en `index.html` la sección del footer (línea ~580):

```javascript
// Coordinación del Programa de Estudios
p.ft-name = "Javier Mendivez Laura";
```

### Cambiar colores institucionales

Las variables CSS están definidas en `:root` al inicio del `<style>`:

```css
:root{
  --turquesa: #009ad3;       /* Color principal (hero, botones, enlaces) */
  --turquesa-dark: #0077aa;  /* Hover y estados activos */
  --turquesa-light: #b8e0f5; /* Fondos sutiles y badges */
  --naranja: #f3a100;        /* Acentos, stats, install button */
  --azul: #0072b9;           /* Headers secundarios */
  --azul-dark: #004f80;      /* Títulos y texto principal */
}
```

### Cambiar líneas de investigación

Edita el `<select id="linea">` en el paso 1 del formulario:

```html
<option>Branding y comunicación visual</option>
<option>Estrategia publicitaria digital</option>
<option>Diseño de campañas integradas</option>
<!-- Añade o modifica opciones según necesidad -->
```

---

## Requisitos del sistema

| Requisito | Especificación |
|---|---|
| Navegador | Chrome 90+, Firefox 88+, Edge 90+, Safari 14+ |
| JavaScript | Habilitado (requerido) |
| Conexión | Solo para primera carga; funciona offline después |
| HTTPS | Requerido para instalación PWA y Service Worker |
| Almacenamiento | ~500 KB (HTML) + datos del formulario en localStorage |

---

## Marco normativo

- **Ley Nº 30512** - Ley Universitaria
- **D.S. Nº 010-2017-MINEDU** - Reglamento de la Ley Universitaria
- **Memorando Múltiple Nº 05/JUI/IDC/2025-II**
- **Normas APA 7.ª edición** para citas y referencias bibliográficas
- **Licencia MINEDU** - RVM N° 164-2025

---

## Créditos institucionales

| Rol | Nombre |
|:---|:---|
| Coordinación del Programa de Estudios | Javier Mendivez Laura |
| Jefatura de la Unidad de Investigación | Mg. Mario Quiroz Martinez |
| Institución | Instituto de Educación Superior Público «Diseño y Comunicación» (IDC) |
| Ubicación | Lima, Perú |
| Año | 2026 |

---

## Licencia

Todos los derechos reservados © IDC - Lima, Perú 2026.

Este generador es un instrumento académico oficial del Instituto de Educación Superior Público «Diseño y Comunicación». El contenido generado por el asistente IA constituye referencias guía; el egresado debe reemplazarlos por su propia experiencia laboral real.

---

## Solución de problemas

| Problema | Solución |
|---|---|
| Los botones de descarga no funcionan | Verifica que JSZip se cargó correctamente (requiere conexión la primera vez) |
| El formulario se ve vacío al recargar | Los datos se guardan en localStorage; verifica que no esté deshabilitado |
| La PWA no se instala | Requiere HTTPS; no funciona con `file://` |
| Las diapositivas PPTX muestran texto demo | Completa el formulario y presiona "Descargar PPTX" nuevamente |
| El JS muestra errores de sintaxis | El archivo usa comillas dobles en strings con tildes; no edites con procesadores de texto |

---

**Instituto de Educación Superior Público «Diseño y Comunicación» · Lima, Perú · 2026**
