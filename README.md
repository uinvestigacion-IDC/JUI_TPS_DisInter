# Generador ESP — Diseño de Interiores (IDC)

Aplicación web de un solo archivo (`index.html`) para elaborar el **Examen de Suficiencia Profesional (ESP)** del Programa de Estudios de Diseño de Interiores del Instituto de Educación Superior Público «Diseño y Comunicación» (IDC). El egresado completa un formulario de 8 pasos y descarga:

- el **portafolio académico preliminar** en Word (`.docx`);
- la **presentación de sustentación** en PowerPoint (`.pptx`), de 15 diapositivas 16:9.

El contenido sigue el *Manual de uso y redacción académica – Generador del Examen de Suficiencia Profesional (ESP) – Diseño de Interiores* (Jefatura de la Unidad de Investigación, IDC, 2026).

> El archivo Word es un portafolio **preliminar**. Según el apartado 1.4 del manual, no se entrega como versión final sin (1) la confirmación de la Coordinación Académica y (2) la ampliación y aprobación del docente orientador.

---

## Archivos

| Archivo | Descripción |
|---|---|
| `index.html` | Aplicación completa: HTML, CSS, JavaScript y plantillas Word y PowerPoint embebidas en base64 (471 KB). |
| `Logo_IDC sin fondo.png` | Logo de la cabecera. No está incluido en el HTML; debe ubicarse en la misma carpeta. |
| `Logo_IDCblanco.png` | Logo del pie de página. Mismo requisito. |
| `sw.js` | Service worker para uso sin conexión. El HTML lo registra solo bajo HTTPS; si no existe, el registro falla sin afectar al resto de la aplicación. |
| `ejemplo_salida/PortafolioESP_ejemplo.docx` | Word generado con el botón «Rellenar con ejemplo». |
| `ejemplo_salida/SustentacionESP_ejemplo.pptx` | PPTX generado con los mismos datos de ejemplo. |

## Publicación

1. Copiar `index.html`, los dos logos y `sw.js` (si existe) en la raíz del repositorio o del servidor.
2. En GitHub Pages, la URL documentada en el manual es: `https://uinvestigacion-idc.github.io/JUI_TPS_DisInter/`.
3. La primera generación de Word o PPTX descarga la librería JSZip 3.10.1 desde `cdnjs.cloudflare.com`. Después queda en la caché del navegador.

---

## Uso

1. Abrir la página y completar los pasos en orden. Los campos con `*` son obligatorios.
2. La barra de pasos muestra el estado de cada paso: pendiente, parcial, completo o error. La barra de progreso indica el porcentaje de campos obligatorios completos.
3. El botón **✨ IA** de cada campo abre tres pestañas: *Requisitos*, *Prompt* (plantilla guiada) y *Ejemplo*. Los textos son referencias y deben sustituirse por la experiencia real.
4. El botón **📚 Citar / APA** abre el generador de referencias APA 7.ª: libro, artículo, web, tesis e IA generativa.
5. **⚡ Rellenar con ejemplo** carga un caso completo: cafetería de especialidad de 85 m² en Barranco, Lima.
6. **📄 Descargar Word** y **📊 Descargar PPTX** generan los archivos.
7. El borrador se guarda en el `localStorage` del navegador con la clave `esp-idc-interiores-data`. Borrar los datos del navegador elimina el borrador.

### Pasos del formulario

| Paso | Contenido | Campos obligatorios |
|---|---|---|
| 1. Carátula y datos institucionales | Título (máx. 25 palabras), autor, DNI, correo institucional (se completa automáticamente), docente orientador, año de titulación, año de egreso, promoción, módulo formativo (I, II o III) | Título, autor, DNI (8 dígitos), docente orientador, años, módulo |
| 2. Dedicatoria y agradecimiento | Textos de protocolo | — |
| 3. Presentación y objetivos | Presentación (200–400 palabras), objetivo general, objetivos específicos (uno por línea) | Presentación, objetivo general, mín. 3 objetivos específicos |
| 4. Capítulo I — Aspectos teóricos | Fundamentación teórica; ficha descriptiva A (10 datos generales), B a M, N (9 etapas); 1.2 presupuesto por partidas; 1.3 contrato, supervisión y acta de conformidad | Los 10 datos generales y al menos 1 partida de presupuesto |
| 5. Capítulo II — Aspectos prácticos | 2.1 Planos a–f y tecnología empleada; 2.2 demostración práctica (objetivo, descripción, procedimiento, materiales) | Los 6 planos y los 4 apartados de la demostración |
| 6. Capítulo III — Anexos y fuentes | Anexos (uno por línea) y fuentes de información APA 7.ª | Mín. 8 referencias |
| 7. Conclusiones y recomendaciones | Síntesis de resultados, 3 conclusiones, recomendaciones en 4 niveles | Conclusiones y las 4 recomendaciones |
| 8. Declaración de uso de IA | Uso de IA (sí/no), nivel AIAS 1–5, herramientas, tareas | Uso de IA; si la respuesta es «Sí», también nivel, herramientas y tareas |

Para descargar el Word se exigen como mínimo: título, autor, DNI, docente orientador y módulo. Si el progreso es menor de 90 %, se muestra el aviso del apartado 6.1 del manual y el archivo se genera igualmente.

---

## Salidas

### Portafolio Word (`PortafolioESP_DisInteriores_<APELLIDO>_<año>.docx`)

Formato del checklist 6.1 del manual: Calibri 11 pt, interlineado 1,5, márgenes superior e inferior de 2,5 cm, izquierdo de 3 cm y derecho de 2,5 cm.

Orden del documento:

1. Carátula (sin encabezado ni pie): institución, licencia, logo, título, programa, módulo, autor, DNI, correo, docente orientador, año de egreso.
2. Declaración de uso de inteligencia artificial (solo si se marcó «Sí»).
3. Dedicatoria y agradecimiento.
4. Índice automático (campo TOC). Word solicita actualizar los campos al abrir el archivo.
5. Presentación y objetivos.
6. Capítulo I: fundamentación, ficha descriptiva A–N, presupuesto con subtotales y total general calculados, contrato y documentación.
7. Capítulo II: tabla de planos 2D y 3D, tecnología empleada, tabla de demostración práctica.
8. Capítulo III: anexos numerados y fuentes de información ordenadas alfabéticamente con sangría francesa.
9. Conclusiones y recomendaciones.

Los campos vacíos aparecen como texto guía gris entre corchetes.

### Presentación PPTX (`SustentacionESP_DisInteriores_<APELLIDO>_<año>.pptx`)

Distribución del apartado 5.1 del manual:

| Diapositiva | Contenido |
|---|---|
| 1 | Portada |
| 2 | Índice de la sustentación |
| 3 | Introducción y contexto |
| 4 | Aspectos teóricos — Objetivos |
| 5 | Aspectos teóricos — Fundamentación |
| 6 | Ficha descriptiva — Datos generales |
| 7 | Ficha descriptiva — Necesidades, estilo y materiales |
| 8–10 | Desarrollo del proyecto — 9 etapas (3 por diapositiva) |
| 11 | Producto final |
| 12 | Presupuesto y documentación |
| 13 | Evaluación y hallazgos |
| 14 | Conclusiones y recomendaciones |
| 15 | Cierre y agradecimientos |

Los textos largos se recortan en el límite de palabra y terminan en «…», porque las cajas de la plantilla no ajustan el tamaño del texto (`noAutofit`).

---

## Arquitectura técnica

- **Archivo único:** todo el código y las dos plantillas están dentro de `index.html`.
- **Word:** la plantilla embebida (`TPL_DOCX_B64`) conserva estilos, logo, encabezado («EXAMEN DE SUFICIENCIA PROFESIONAL (ESP)») y pie de página con numeración. El JavaScript reemplaza dos marcadores de `word/document.xml`:
  - `{{COVER}}`: contenido de la carátula, insertado después del logo.
  - `{{BODY}}`: cuerpo del documento, insertado después del salto de sección.
- **PowerPoint:** la plantilla embebida (`TPL_PPTX_B64`) aporta 15 diapositivas con logo, barras de color y pies. El objeto `SRC` indica qué diapositiva de la plantilla se usa como base para cada diapositiva final. Los textos se sustituyen **por posición** del elemento `<a:t>` (función `pptxSlideReplacements`).
- **Validación:** el objeto `SCHEMA` define paso, obligatoriedad y validador de cada campo (`required`, `minWords`, `maxWords`, `minLines`, `anio`, `siIA`).
- **Campos generados por código:** las 9 etapas (`ETAPAS`) y los 6 planos (`PLANOS`) se crean al cargar la página.
- **Tabla dinámica:** presupuesto (`TABLES.presupuesto`) con columnas partida, descripción, cantidad y precio unitario.
- **Asistente:** `AI_DATA` almacena, por campo, los textos de las pestañas Requisitos, Prompt y Ejemplo.

### Modificar las plantillas embebidas

```python
import re, base64
h = open('index.html', encoding='utf-8').read()
docx = base64.b64decode(re.search(r'const TPL_DOCX_B64="([^"]+)"', h).group(1))
pptx = base64.b64decode(re.search(r'const TPL_PPTX_B64="([^"]+)"', h).group(1))
open('plantilla.docx', 'wb').write(docx)
open('plantilla.pptx', 'wb').write(pptx)
```

Después de editar una plantilla, se vuelve a codificar con `base64.b64encode(...).decode()` y se reemplaza la cadena correspondiente. En la plantilla Word deben conservarse los párrafos `{{COVER}}` y `{{BODY}}`. En la plantilla PPTX, cualquier cambio en el número u orden de los textos de una diapositiva obliga a revisar los índices de `pptxSlideReplacements`.

---

## Cambios respecto de la versión anterior (Generador TSP)

- Se reemplazó la estructura del Trabajo de Suficiencia Profesional (resumen ejecutivo, 4 capítulos, manual de funciones, hallazgos, plan de mejora) por la estructura ESP del manual.
- Se eliminó el segundo autor: el ESP es individual.
- Se agregaron el módulo formativo, la promoción, la ficha descriptiva A–N, las 9 etapas, el presupuesto, los planos, la demostración práctica y la declaración AIAS.
- **Corrección de error:** la versión anterior descargaba una plantilla Word fija, con textos de Diseño de Modas y sin datos del formulario. La versión actual genera el documento con los datos ingresados.
- Se cambió la clave de almacenamiento a `esp-idc-interiores-data`. Los borradores de la versión TSP no se cargan.
- Se agregó la sección «Evaluación y sustentación del ESP»: rúbrica de 20 puntos, tiempos (20, 40 y 15 min), plazos, formato y enlaces de apoyo.
- El service worker se registra solo bajo HTTPS.

## Decisiones no especificadas en el manual

- **Fundamentación teórica (Capítulo I):** el manual la menciona en el primer objetivo específico y en las diapositivas 4–5, pero no la incluye como campo.
- **Síntesis de resultados (Paso 7):** alimenta la diapositiva 13 («Evaluación y hallazgos») y el primer párrafo de las conclusiones.
- **Nombres de los niveles AIAS:** el manual menciona la escala 1–5 sin definirla. Se usan los de la versión revisada: Sin IA, Planificación con IA, Colaboración con IA, IA completa, Exploración con IA.
- **Datos del ejemplo:** el proyecto es ficticio. El autor y el DNI son los del ejemplo del manual. Las referencias provienen de la bibliografía del manual.

## Verificación realizada

- Sintaxis JavaScript: `node --check` sin errores.
- Prueba en Chromium (Playwright):
  - el ejemplo completa los 8 pasos al 100 %;
  - Word y PPTX se descargan;
  - el borrador se restaura al recargar la página;
  - la validación condicional de IA funciona;
  - con 390 px de ancho no hay desplazamiento horizontal.
- Archivos generados: 0 errores de XML. Ambos se leen con `python-docx` y `python-pptx`.

## Limitaciones conocidas

- Los archivos generados no se abrieron en Microsoft Word, PowerPoint ni LibreOffice durante la verificación. Deben revisarse en Office antes de distribuir la herramienta.
- El ajuste del texto en las diapositivas se estimó por tamaño de caja y de fuente; no se comprobó visualmente.
- La generación requiere conexión la primera vez, para descargar JSZip.
- Los botones ✨ IA ocupan la esquina superior derecha de cada campo y pueden cubrir parte del texto escrito.

## Base normativa

Ley N.º 28044; D.S. N.º 011-2012-ED; Ley N.º 30512; Ley N.º 31653; D.S. N.º 010-2017-MINEDU; RVM N.º 064-2019-MINEDU; D.U. N.º 017-2020; D.S. N.º 016-2021-MINEDU; RVM N.º 049-2022-MINEDU (numeral 15.2.2); RVM N.º 103-2022-MINEDU; RVM N.º 140-2021-MINEDU; RVM N.º 085-2025-MINEDU; RVM N.º 164-2025-MINEDU; Reglamento IA IDC (2026); Memorando Múltiple N.º 05/JUI/IDC/2025-II; Guía Académica para la Elaboración y Evaluación de las Modalidades de Titulación en Diseño de Interiores (IDC, 2026); APA 7.ª edición (2020).

## Créditos

- Coordinación del Programa de Estudios de Diseño de Interiores: Dis. María Quintana Vera Tudela.
- Jefatura de la Unidad de Investigación: Mg. Mario Quiroz Martinez.
- Instituto de Educación Superior Público «Diseño y Comunicación», Lima, Perú, 2026.
