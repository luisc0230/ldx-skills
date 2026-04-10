# Protocolo de Búsqueda de Artículos Científicos

## Principio
Cada afirmación teórica, estadística o metodológica en el `.docx` debe estar respaldada
por al menos una fuente científica verificada en tiempo real. Claude nunca inventa citas.

## Bases de datos (en orden de prioridad)
1. **Google Scholar** — más amplio, multidisciplinario
2. **Scielo** — scielo.org — iberoamericano, acceso libre
3. **Redalyc** — redalyc.org — latinoamericano, acceso libre
4. **PubMed** — pubmed.ncbi.nlm.nih.gov — ciencias de la salud
5. **Dialnet** — dialnet.unirioja.es — español/portugués
6. **DOAJ** — doaj.org — acceso abierto multidisciplinario
7. **IEEE Xplore** — ieeexplore.ieee.org — ingeniería/tecnología
8. **Springer / Elsevier** — resúmenes disponibles

## Queries por tipo de contenido

### Antecedentes (Marco Teórico)
```
web_search: "[tema principal] investigación [año reciente] scielo OR redalyc"
web_search: "[variable 1] [variable 2] estudio cuantitativo site:scholar.google.com"
web_search: "[tema] systematic review meta-analysis [últimos 5 años]"
```
Meta: ≥10 antecedentes (≥5 internacionales + ≥5 nacionales), últimos 5 años preferentemente.

### Bases teóricas
```
web_search: "teoría [nombre] [autor fundador] definición académica año"
web_search: "[concepto clave] definición científica autor cita"
```

### Estadísticas para planteamiento del problema
```
web_search: "[problema] estadísticas [país] [año actual] INEI OR CEPAL OR OMS OR UNESCO"
web_search: "[indicador] informe oficial [organismo] [año]"
web_search: "[tema] datos oficiales ministerio [país] [año]"
```

### Validación de instrumentos
```
web_search: "cuestionario [tema] validado alfa Cronbach propiedades psicométricas"
web_search: "escala [nombre] validez confiabilidad [año]"
```

## Ficha de artículo científico (registro interno)

Por cada fuente encontrada, Claude registra internamente:

```
AUTOR(ES): Apellido, N.
AÑO: XXXX
TÍTULO: Título completo
REVISTA: Nombre de la revista indexada
VOLUMEN/NÚMERO: V(N)
PÁGINAS: pp–pp
DOI/URL: [enlace verificado]
APORTE: [qué aporta a esta tesis en 2 líneas]
CITA APA 7: Apellido, A. (año). Título. Revista, V(N), pp–pp. https://doi.org/xxx
CITA VANCOUVER: N. Apellido et al., "Título", Revista, vol. V, n.º N, pp. pp-pp, año.
```

## Proceso de verificación de fuentes

Antes de insertar cualquier cita en el `.docx`:

1. Buscar DOI o URL con `web_search`.
2. Si el artículo existe y es accesible → incluir.
3. Si solo hay referencia de segunda mano → buscar el original.
4. Si no se puede verificar → **NO incluir**, buscar alternativa.
5. **NUNCA fabricar DOIs, años, nombres de revistas ni autores.**

## Informe de fuentes al usuario (en el chat)

Al completar las búsquedas de una fase, Claude informa:

```
🔍 FUENTES ENCONTRADAS — FASE [N]

✅ Artículos verificados ([N]):
1. Apellido (año) — Título resumido — DOI: [link]
2. Apellido (año) — Título resumido — DOI: [link]
...

⚠️ No encontrado (buscado, descartado):
- [tema buscado] → reemplazado por: [alternativa]

📊 Estadísticas oficiales encontradas:
- [dato] → Fuente: [organismo, año, URL]
```

## Mínimo de búsquedas por fase

| Fase | Búsquedas mínimas | Artículos mínimos |
|---|---|---|
| 1 — Plan de Tesis | 3 (estadísticas + marco legal + contexto) | 3–5 |
| 2 — Marco Teórico | 6 (antecedentes int. + nac. + bases teóricas) | ≥10 |
| 3 — Metodología | 2 (diseño + instrumento validado) | 2–3 |
| 4 — Instrumentos | 2 (escalas similares) | 1–2 |
| 5 — Resultados | 3 (para discusión) | 3–5 |
| 6 — Conclusiones | 1 (verificar recomendaciones) | 1–2 |
| 8 — Sustentación | 2 (preguntas frecuentes de defensa) | — |
