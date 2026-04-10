# Sistema de Verificación de Texto

Leer este archivo cuando el usuario pegue un texto (título, objetivo, párrafo, sección).

## Paso 1 — Análisis de coherencia interna

Evaluar:
- ¿El texto es coherente con el tema declarado en el perfil?
- ¿El objetivo tiene: verbo en infinitivo + variable + unidad de análisis + contexto?
  - ✅ "Determinar la relación entre el estrés laboral y el desempeño docente en
       instituciones educativas públicas de Lima, 2024"
  - ❌ "Ver si el estrés afecta a los profesores"
- ¿La hipótesis es falseable y se conecta con los objetivos?
- ¿La redacción es académica? (tercera persona, sin coloquialismos, sin primera persona)
- ¿Las estadísticas citadas tienen fuente y año?
- ¿El nivel de vocabulario corresponde al nivel académico declarado?

## Paso 2 — Verificación con fuentes reales

```
web_search: "[afirmación principal del texto] evidencia académica"
web_search: "[dato estadístico mencionado] fuente oficial año"
web_search: "[concepto teórico] definición autor original"
```

## Paso 3 — Reporte al usuario (siempre en el chat, nunca en el .docx)

```
📊 ANÁLISIS DE TU TEXTO

✅ Lo que está bien:
- [aspecto 1 con breve explicación]
- [aspecto 2]

⚠️ Lo que puede mejorar:
- [problema] → Sugerencia: [mejora concreta con ejemplo]
- [problema] → Sugerencia: [mejora concreta]

❌ Lo que necesita corrección:
- [error crítico] → Por qué: [razón académica]
  Versión corregida: "[texto mejorado]"

🔍 Verificación de fuentes:
- "[afirmación X]" → ✅ VERIFICADO: [fuente real, año, DOI]
- "[afirmación Y]" → ⚠️ NO ENCONTRADO → Alternativa: [fuente sugerida]

🎯 Mi recomendación:
A) Conservar con ajustes menores → [detalle de qué ajustar]
B) Reescribir parcialmente → [qué secciones y por qué]
C) Reescribir totalmente → [motivo principal]

¿Qué prefieres?
```

## Paso 4 — Acción según elección del usuario

**Opción A — Ajustes menores:**
- Aplicar correcciones en el chat.
- Mostrar versión final corregida.
- Preguntar: "¿Apruebas esta versión para incluirla en el .docx?"

**Opción B — Reescritura parcial:**
- Identificar secciones a mantener vs. reescribir.
- Presentar versión híbrida en el chat con fuentes añadidas.
- Esperar aprobación antes de generar el `.docx`.

**Opción C — Reescritura total:**
- Generar versión completamente nueva con fuentes reales.
- Presentar en el chat para aprobación.
- Si el usuario aprueba → incluir en `.docx`.

## Casos especiales

### Título tentativo
Si el usuario da un título, evaluar:
- ¿Es específico? (identifica variables, población, contexto, tiempo)
- ¿No es demasiado largo? (máx. 20 palabras recomendado)
- ¿Corresponde al tipo de investigación?

Ofrecer siempre 3 versiones:
1. Título original ajustado
2. Título más específico y académico
3. Título alternativo si el enfoque puede mejorar

### Objetivos
Verificar estructura: VERBO (infinitivo) + QUÉ (variable/fenómeno) + EN QUIÉN (unidad) + DÓNDE/CUÁNDO (contexto)

Verbos para objetivo general: Determinar, Establecer, Analizar, Evaluar, Identificar
Verbos para objetivos específicos: Describir, Comparar, Relacionar, Medir, Conocer

### Hipótesis
Verificar:
- Debe ser una afirmación (no pregunta)
- Debe mencionar la relación entre variables
- Debe ser falseable (comprobable con datos)
- Debe corresponder al objetivo general
