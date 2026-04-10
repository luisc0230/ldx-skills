# Contenido Detallado de Cada Fase

## FASE 1 — Plan de Tesis / Proyecto de Investigación
**Entregable:** `01_Plan_de_Tesis.docx`

**Búsquedas obligatorias antes de redactar:**
- Estadísticas del problema en el país/región (INEI, CEPAL, OMS, UNESCO, ministerios).
- 3–5 artículos científicos sobre el tema para fundamentar la situación problemática.
- Leyes, normas o políticas públicas relacionadas.

**Contenido:**
- Portada institucional completa (logo buscado en internet si no fue provisto).
- Índice automático (placeholder; actualizar con F9).
- **Cap. I — Planteamiento del Problema:**
  - Situación problemática: estadísticas reales + citas verificadas.
  - Problema general (pregunta) + problemas específicos (≥2).
  - Justificación: teórica, práctica, metodológica, social.
  - Objetivo general + objetivos específicos (verbo infinitivo + variable + unidad + contexto).
  - Hipótesis general + específicas (si aplica según tipo de investigación).
  - Delimitación espacial, temporal y temática.
  - Limitaciones anticipadas.
- **Matriz de consistencia** (tabla: problema ↔ objetivo ↔ hipótesis ↔ variable ↔
  dimensión ↔ indicador ↔ instrumento).
- **Operacionalización de variables** (variable → definición conceptual → definición
  operacional → dimensiones → indicadores → ítems → escala).
- **Cronograma de Gantt** (tabla con fases y semanas).
- **Referencias** (solo las verificadas en esta fase).

---

## FASE 2 — Marco Teórico
**Entregable:** `02_Marco_Teorico.docx`

**Búsquedas obligatorias (ver scientific-search.md para queries exactos):**
- Antecedentes internacionales: ≥5 artículos, últimos 5 años.
- Antecedentes nacionales: ≥5 artículos del país del tesista.
- Bases teóricas: autor fundador de cada teoría + artículos de aplicación recientes.
- Marco legal: leyes y normas vigentes relacionadas.

**Ficha de antecedente (estructura obligatoria):**
Autor(es) | Año | Título | País/Institución | Objetivo | Metodología (tipo/diseño/muestra) |
Resultados principales | Conclusión relevante para esta tesis | DOI verificado

**Contenido:**
- **Antecedentes internacionales** (≥5, últimos 5 años preferentemente).
- **Antecedentes nacionales/regionales** (≥5).
- **Bases teóricas:** por variable/dimensión, autores originales + artículos de aplicación con DOI.
- **Bases conceptuales:** glosario con definición de autor + cita verificada.
- **Marco legal/normativo** (si aplica: leyes, decretos, convenios internacionales).
- **Tablas comparativas** entre teorías o enfoques.
- **Figuras conceptuales** (mapas de variables, esquemas de relación) con matplotlib.
- **Referencias** completas.

**Regla anti-invención:** Si Claude no puede verificar una fuente → no la usa.
Informa en el chat y busca alternativa.

---

## FASE 3 — Metodología
**Entregable:** `03_Metodologia.docx`

**Búsquedas obligatorias:**
- Artículo que respalde el diseño de investigación elegido.
- Instrumento validado similar en la literatura.
- Datos de la población en fuentes oficiales verificadas.

**Contenido:**
- Tipo, nivel, enfoque y diseño de investigación (con cita que lo justifique).
- **Población** con fuente oficial verificada (padrón, censo, registro institucional).
- **Muestra** con fórmula estadística completa:

  Para población finita:
  n = (N · Z² · p · q) / (e² · (N-1) + Z² · p · q)

  - N = tamaño de la población (fuente oficial)
  - Z = valor crítico según confianza (1.96 para 95%)
  - p = proporción estimada (0.5 si desconocida)
  - q = 1 - p
  - e = error máximo aceptable (0.05 típicamente)

  Cálculo numérico completo paso a paso con valores justificados.

- Técnicas e instrumentos de recolección.
- **Validez:** juicio de expertos (tabla: pertinencia, relevancia, claridad por ítem).
- **Confiabilidad:** alfa de Cronbach calculado con scipy si hay datos; si no,
  referenciar estudio piloto con cita real.
- Procedimiento de recolección de datos.
- Plan de análisis estadístico (SPSS, R, Jamovi, Atlas.ti — según tipo).
- Consideraciones éticas (consentimiento, anonimato, beneficencia, no maleficencia).
- **Anexos:** instrumento completo, ficha de validación, consentimiento informado.

---

## FASE 4 — Instrumentos y Herramientas
**Entregable:** `04_Instrumentos.docx`

**Búsquedas:** instrumentos validados similares para justificar el diseño elegido.

**Contenido:**
- Cuestionario completo listo para imprimir (instrucciones + ítems + escala).
- Escala Likert con redacción positiva y negativa equilibrada.
- Ficha de validación por juicio de expertos (una página por experto, tabla de criterios).
- Matriz ítem-indicador-dimensión-variable.

---

## FASE 5 — Resultados y Discusión
**Entregable:** `05_Resultados_y_Discusion.docx`

**Búsquedas:** estudios con resultados similares o contrarios para enriquecer la discusión.

**Contenido:**
- **Tablas estadísticas** formato APA (sin bordes verticales; título arriba; fuente abajo):
  - Frecuencias y porcentajes por variable/dimensión.
  - Estadísticos descriptivos: media, mediana, moda, desviación estándar.
- **Pruebas estadísticas reales** con scipy.stats:
  - chi2_contingency → chi cuadrado (variables nominales)
  - ttest_ind / ttest_rel → t de Student
  - f_oneway → ANOVA
  - pearsonr / spearmanr → correlaciones
  - Resultado obligatorio: estadístico, grados de libertad, p-valor, conclusión.
- **Gráficas** con matplotlib ≥300 dpi. Cada figura: número, título, fuente.
- **Interpretación** en prosa académica formal (tercera persona, voz impersonal).
- **Discusión:** cada resultado contrastado con ≥1 antecedente verificado del Marco
  Teórico. Validación o rechazo de hipótesis con evidencia estadística.

---

## FASE 6 — Conclusiones y Recomendaciones
**Entregable:** `06_Conclusiones_y_Recomendaciones.docx`

- Una conclusión por cada objetivo específico (correspondencia 1:1 obligatoria).
- Conclusión general vinculada al objetivo general.
- Recomendaciones diferenciadas por actor: institución, autoridades, comunidad,
  futuros investigadores.
- Cada recomendación: acción concreta + justificación basada en los resultados.

---

## FASE 7 — Referencias Bibliográficas
**Entregable:** `07_Referencias.docx`

**Búsquedas:** verificar DOI de cada referencia pendiente de confirmar.

- Lista completa en norma exigida, orden alfabético, sangría francesa.
- Verificación cruzada: toda cita en el texto tiene su referencia y viceversa.
- DOI/URL verificado para cada fuente digital.
- Clasificación por tipo: artículo científico, libro, tesis, informe, sitio web.

---

## FASE 8 — Sustentación
**Entregables:**
- `08a_Guion_Sustentacion.docx` — guion oral 15–20 min con tiempos por sección:
  - Introducción y presentación personal: 2 min
  - Planteamiento del problema y objetivos: 3 min
  - Marco teórico (puntos clave): 3 min
  - Metodología: 3 min
  - Resultados y discusión: 5 min
  - Conclusiones y recomendaciones: 3 min
  - Cierre y agradecimiento: 1 min

- `08b_Preguntas_del_Jurado.docx` — 25 preguntas probables con respuestas modelo:
  - 5 preguntas sobre planteamiento/justificación
  - 5 sobre marco teórico
  - 5 sobre metodología
  - 5 sobre resultados
  - 5 sobre conclusiones/implicaciones

- `08c_Presentacion.pptx` — usar skill `pptx`. Incluir:
  - Colores institucionales de la universidad
  - Logo institucional
  - Máximo 20 diapositivas
  - Cada slide: título claro + máximo 5 puntos o 1 gráfica

**Búsquedas para preguntas del jurado:**
- Preguntas frecuentes de defensa en el área de investigación.
- Críticas metodológicas comunes al diseño utilizado.
- Limitaciones típicas del instrumento elegido.

---

## FASE 9 — Documento Final Consolidado
**Entregable:** `TESIS_FINAL_[Apellido]_[Año].docx`

Integra todos los capítulos en un solo documento con:
- Portada, contraportada, hoja de aprobación, dedicatoria, agradecimientos.
- Resumen en español (250–300 palabras: objetivo, metodología, resultados, conclusión).
- Abstract en inglés (traducción del resumen).
- Palabras clave / Keywords (5–7).
- Índice general, índice de tablas, índice de figuras.
- Capítulos I–VI completos (sin secciones cortadas).
- Referencias bibliográficas completas.
- Anexos (instrumentos, validaciones, datos).
- Paginación diferenciada:
  - Romana (i, ii, iii…) para: portada, aprobación, dedicatoria, agradecimientos,
    resumen, abstract, índices.
  - Arábiga (1, 2, 3…) desde introducción o capítulo I.
- Encabezado: título abreviado de la tesis (máx. 50 caracteres).
- Pie de página: número de página centrado.
