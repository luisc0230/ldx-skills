# Sistema de Replicación de Diseño Institucional

Leer este archivo cuando el usuario suba un archivo de referencia (reglamento, tesis
modelo, plantilla, guía institucional).

## Paso 1 — Leer el archivo

```python
# Si es .docx
from docx import Document
doc = Document("/mnt/user-data/uploads/[archivo].docx")

# Si es .pdf
import pdfplumber
with pdfplumber.open("/mnt/user-data/uploads/[archivo].pdf") as pdf:
    texto = "\n".join(p.extract_text() for p in pdf.pages if p.extract_text())
```

## Paso 2 — Extraer especificaciones

Construir este diccionario con los datos del archivo:

```python
DISEÑO_INSTITUCIONAL = {
    "portada": {
        "logo_posicion": "",       # "centro superior" / "izquierda" / etc.
        "universidad": {
            "texto": "",
            "fuente": "", "tamaño": "", "negrita": True/False,
            "posicion": ""         # "centro" / "izquierda"
        },
        "facultad": {"texto": "", "fuente": "", "tamaño": ""},
        "carrera": {"texto": "", "fuente": "", "tamaño": ""},
        "titulo_tesis": {
            "fuente": "", "tamaño": "", "negrita": True/False,
            "mayusculas": True/False, "posicion": ""
        },
        "autor_label": "",         # "Autor:" / "Presentado por:" / etc.
        "asesor_label": "",        # "Asesor:" / "Director:" / etc.
        "ciudad_año": ""
    },
    "cuerpo": {
        "fuente": "",              # "Times New Roman" / "Arial" / etc.
        "tamaño": 12,
        "interlineado": "",        # "1.5" / "2.0" / "simple"
        "margenes": {
            "sup": "", "inf": "", "izq": "", "der": ""  # en cm
        },
        "sangria_primera_linea": "", # en cm
        "alineacion": ""           # "justified" / "left"
    },
    "titulos": {
        "capitulo": {
            "fuente": "", "tamaño": "", "negrita": True/False,
            "mayusculas": True/False, "centrado": True/False
        },
        "nivel_1": {"fuente": "", "tamaño": "", "negrita": True/False},
        "nivel_2": {"fuente": "", "tamaño": "", "cursiva": True/False},
        "nivel_3": {"fuente": "", "tamaño": ""}
    },
    "tablas": {
        "estilo": "",              # "APA" / "con bordes" / etc.
        "titulo_posicion": "",     # "arriba" / "abajo"
        "fuente_posicion": ""      # "arriba" / "abajo"
    },
    "figuras": {
        "titulo_posicion": "",     # "arriba" / "abajo"
        "fuente_posicion": ""
    },
    "paginacion": {
        "preliminares": "",        # "romana" / "arabiga"
        "cuerpo": "arabiga",
        "posicion": "",            # "centro inferior" / "derecha inferior"
        "desde_pagina": ""         # desde qué capítulo inicia la arábiga
    },
    "encabezado": "",
    "pie_pagina": "",
    "norma_citacion": "",          # detectada del texto
    "num_capitulos_requeridos": 0
}
```

## Paso 3 — Reporte al usuario

```
🎨 DISEÑO INSTITUCIONAL DETECTADO

Fuente: [X] [tamaño]pt | Interlineado: [X]
Márgenes: sup [X]cm · inf [X]cm · izq [X]cm · der [X]cm
Portada: [descripción del layout detectado]
Capítulos: [fuente, tamaño, centrado/izquierda, mayúsculas]
Tablas: [estilo] — título [arriba/abajo] — fuente [arriba/abajo]
Figuras: título y fuente [posición detectada]
Paginación: [romana/arábiga] en preliminares · arábiga desde [X]
Norma de citación: [detectada]

¿Confirmas que aplique este diseño a todos tus documentos?
```

## Paso 4 — Guardar en perfil y aplicar

Una vez confirmado, este diccionario se almacena en el **PERFIL DEL TESISTA** y se
usa en **todos** los `.docx` generados durante la sesión.

## Aplicación técnica en python-docx

```python
from docx import Document
from docx.shared import Pt, Cm
from docx.enum.text import WD_ALIGN_PARAGRAPH

doc = Document()

# Márgenes
section = doc.sections[0]
section.top_margin    = Cm(float(DISEÑO["cuerpo"]["margenes"]["sup"]))
section.bottom_margin = Cm(float(DISEÑO["cuerpo"]["margenes"]["inf"]))
section.left_margin   = Cm(float(DISEÑO["cuerpo"]["margenes"]["izq"]))
section.right_margin  = Cm(float(DISEÑO["cuerpo"]["margenes"]["der"]))

# Estilo de párrafo por defecto
style = doc.styles["Normal"]
font  = style.font
font.name = DISEÑO["cuerpo"]["fuente"]
font.size = Pt(DISEÑO["cuerpo"]["tamaño"])

# Interlineado
from docx.oxml.ns import qn
from docx.oxml import OxmlElement
pPr = style.element.get_or_add_pPr()
spacing = OxmlElement("w:spacing")
if DISEÑO["cuerpo"]["interlineado"] == "1.5":
    spacing.set(qn("w:line"), "360")
    spacing.set(qn("w:lineRule"), "auto")
elif DISEÑO["cuerpo"]["interlineado"] == "2.0":
    spacing.set(qn("w:line"), "480")
    spacing.set(qn("w:lineRule"), "auto")
pPr.append(spacing)
```

## Diseño estándar iberoamericano (si no hay archivo de referencia)

```
fuente: Times New Roman 12pt
interlineado: 1.5
márgenes: sup 2.5cm · inf 2.5cm · izq 3.0cm · der 2.5cm
sangría: 1.25cm primera línea
alineación: justificada
capítulos: centrado, mayúsculas, negrita, 14pt
subtítulo nivel 1: izquierda, negrita, 12pt
subtítulo nivel 2: izquierda, cursiva, 12pt
tablas: APA (sin bordes verticales, título arriba, fuente abajo)
figuras: título y fuente debajo
paginación: romana para preliminares, arábiga desde introducción, centro inferior
norma predeterminada: APA 7
```
