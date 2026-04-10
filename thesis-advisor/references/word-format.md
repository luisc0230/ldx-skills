# Especificaciones Técnicas del Documento Word (.docx)

Leer junto con `/mnt/skills/public/docx/SKILL.md`.
Aplicar DISEÑO_INSTITUCIONAL si fue detectado; si no, usar los valores estándar de este archivo.

## Configuración general (estándar iberoamericano)

| Elemento | Valor estándar | Nota |
|---|---|---|
| Fuente cuerpo | Times New Roman 12pt | Arial si exige la universidad |
| Interlineado | 1.5 | Simple para tablas, citas bloque, referencias |
| Margen superior | 2.5 cm | |
| Margen inferior | 2.5 cm | |
| Margen izquierdo | 3.0 cm | |
| Margen derecho | 2.5 cm | |
| Sangría primera línea | 1.25 cm | |
| Alineación | Justificada | |
| Tamaño página | A4 | |

## Estilos de títulos

| Nivel | Formato |
|---|---|
| Capítulo (Heading 1) | Centrado · Mayúsculas · Negrita · 14pt |
| Subtítulo 1 (Heading 2) | Izquierda · Negrita · 12pt |
| Subtítulo 2 (Heading 3) | Izquierda · Negrita + Cursiva · 12pt |
| Subtítulo 3 (Heading 4) | Izquierda · Cursiva · 12pt |

## Tablas (formato APA)

- Sin bordes verticales.
- Línea horizontal superior e inferior del encabezado, línea final.
- **Número y título arriba** (negrita el número, normal el título):
  `Tabla 1`
  `Distribución de frecuencias por variable X`
- **Nota/fuente abajo:** `Nota. Elaboración propia. / Fuente: [autor, año].`
- Fuente dentro de la tabla: 10–11pt.

## Figuras (formato APA)

- **Número, título y fuente debajo** de la imagen.
- Formato: `Figura 1. Título descriptivo. Fuente: Elaboración propia.`
- PNG ≥300 dpi generados con matplotlib.
- Fuente del texto: 10pt debajo.

## Ecuaciones

- Ecuaciones Word nativas (OMML) cuando sea posible.
- Si no, imagen LaTeX renderizada con `matplotlib.mathtext`.
- Numeradas al margen derecho: (1), (2)…
- Centradas en la página.

## Citas textuales

- Menos de 40 palabras: entre comillas, integrada en el párrafo.
- 40 o más palabras: bloque separado, sangría 1.25 cm en todo el párrafo,
  sin comillas, interlineado simple, tamaño 11pt.

## Paginación

- **Preliminares:** romana minúscula (i, ii, iii…) — portada sin número visible.
- **Cuerpo:** arábiga (1, 2, 3…) desde introducción o capítulo I.
- Posición: centro inferior (o según diseño institucional).

## Portada institucional — elementos obligatorios

1. Logo de la universidad (buscar en internet si no fue provisto, usar URL directa).
2. Nombre completo de la universidad (mayúsculas).
3. Facultad / Escuela / Departamento.
4. Carrera o programa.
5. Título completo de la tesis (negrita, centrado, entre 15 y 20 palabras).
6. Para optar el grado/título de: [grado académico].
7. Autor(es): Apellido, Nombre.
8. Asesor(a): Apellido, Nombre. (con grado académico si se conoce).
9. Ciudad, País, Año.

## Índice automático

Insertar campo TOC con instrucción al usuario:
```
# ÍNDICE
[Actualizar con clic derecho → "Actualizar campo" o presionar F9]
```
Configurar para incluir Heading 1, 2 y 3.

## Código Python base para python-docx

```python
from docx import Document
from docx.shared import Pt, Cm, RGBColor
from docx.enum.text import WD_ALIGN_PARAGRAPH
from docx.oxml.ns import qn
from docx.oxml import OxmlElement

def configurar_documento(diseño):
    doc = Document()
    section = doc.sections[0]

    # Márgenes
    section.page_height = Cm(29.7)
    section.page_width  = Cm(21.0)
    section.top_margin    = Cm(float(diseño["margenes"]["sup"]))
    section.bottom_margin = Cm(float(diseño["margenes"]["inf"]))
    section.left_margin   = Cm(float(diseño["margenes"]["izq"]))
    section.right_margin  = Cm(float(diseño["margenes"]["der"]))

    # Fuente y tamaño base
    style = doc.styles["Normal"]
    style.font.name = diseño["fuente"]
    style.font.size = Pt(diseño["tamaño"])

    # Interlineado 1.5
    pPr = style.element.get_or_add_pPr()
    spacing = OxmlElement("w:spacing")
    spacing.set(qn("w:line"), "360")   # 1.5 = 360 twips
    spacing.set(qn("w:lineRule"), "auto")
    pPr.append(spacing)

    return doc

def agregar_tabla_apa(doc, datos, titulo, numero, fuente="Elaboración propia"):
    """Tabla APA sin bordes verticales."""
    # Título arriba
    p_titulo = doc.add_paragraph()
    p_titulo.add_run(f"Tabla {numero}\n").bold = True
    p_titulo.add_run(titulo)

    # Tabla
    tabla = doc.add_table(rows=len(datos), cols=len(datos[0]))
    tabla.style = "Table Grid"

    # Quitar bordes verticales (solo horizontales en cabecera y final)
    for row in tabla.rows:
        for cell in row.cells:
            tc = cell._tc
            tcPr = tc.get_or_add_tcPr()
            tcBorders = OxmlElement("w:tcBorders")
            for border in ["left", "right"]:
                b = OxmlElement(f"w:{border}")
                b.set(qn("w:val"), "nil")
                tcBorders.append(b)
            tcPr.append(tcBorders)

    # Nota al pie
    p_nota = doc.add_paragraph()
    p_nota.add_run("Nota. ").italic = True
    p_nota.add_run(f"Fuente: {fuente}.")
    return tabla
```

## Insertar gráfica PNG

```python
import matplotlib.pyplot as plt
import os

def generar_grafica_barras(datos, etiquetas, titulo, ruta_salida):
    fig, ax = plt.subplots(figsize=(8, 5), dpi=300)
    bars = ax.bar(etiquetas, datos, color="#2563EB", edgecolor="white")
    ax.set_title(titulo, fontsize=13, fontweight="bold", pad=12)
    ax.set_ylabel("Frecuencia", fontsize=11)
    ax.set_xlabel("Categorías", fontsize=11)
    ax.bar_label(bars, fmt="%.1f", padding=3)
    plt.tight_layout()
    plt.savefig(ruta_salida, dpi=300, bbox_inches="tight")
    plt.close()
    return ruta_salida

# Insertar en el doc
from docx.shared import Inches
figura_path = "/home/claude/figuras/figura_01.png"
doc.add_picture(figura_path, width=Inches(5.5))
p = doc.add_paragraph(f"Figura 1. {titulo}. Fuente: Elaboración propia.")
p.alignment = WD_ALIGN_PARAGRAPH.CENTER
p.runs[0].font.size = Pt(10)
```
