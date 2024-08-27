# Herramienta de Extracción de Texto de PDF

Este script de Python permite extraer texto de cada página de un archivo PDF, guardarlo en un documento de Word y luego convertirlo en un archivo PDF. Incluye características como la corrección de la inclinación (deskew) de las páginas escaneadas, la eliminación de encabezados y pies de página, y la extracción de datos detallados de texto utilizando Tesseract OCR. El script aprovecha el multiprocesamiento para procesar las páginas en paralelo, lo que acelera significativamente el proceso, especialmente para PDFs grandes.

## Características

- **Convertir PDF a Imágenes**: El script convierte cada página de un PDF en una imagen usando `pdf2image`.
- **Corrección de Inclinación (Deskewing)**: Corrige la inclinación de las imágenes escaneadas para mejorar la precisión del OCR.
- **Extracción de Texto**: Utiliza Tesseract OCR para extraer texto de las imágenes.
- **Eliminación de Encabezados y Pies de Página**: Elimina los encabezados y pies de página del texto extraído para centrarse en el contenido principal.
- **Procesamiento en Paralelo**: Procesa las páginas del PDF en paralelo utilizando la biblioteca `multiprocessing`, acelerando así el proceso de extracción de texto.
- **Conversión de Texto a Word y PDF**: El texto extraído se guarda en un documento de Word y luego se convierte automáticamente en un archivo PDF.


## Requisitos

- Python 3.x
- Librerías de Python requeridas:
  - `pdf2image`
  - `opencv-python` (cv2)
  - `numpy`
  - `pytesseract`
  - `pandas`
  - `multiprocessing` (parte de la biblioteca estándar de Python)
  - `python-docx`
  - `comtypes`

Puedes instalar las librerías requeridas usando pip:

'''
pip install pdf2image opencv-python numpy pytesseract pandas python-docx comtypes
'''

Además, debes tener instalado Poppler y Tesseract OCR en tu máquina. 
Puedes descargar Poppler desde aquí (Versión Windows): https://github.com/oschwartz10612/poppler-windows/releases/
Puedes descargar Tesseract OCR desde aquí: https://github.com/tesseract-ocr/tesseract
Se recomienda el siguiente video en el caso de Windows (x64): https://youtu.be/2kWvk4C1pMo?si=PMEiObpABV2JRHBy

## Cómo Usar

**Preparar el Entorno**:

Instala las librerías de Python necesarias mencionadas en los requisitos.
Asegúrate de que Poppler esté instalado y configurado en tu sistema para que pdf2image funcione correctamente.
Asegúrate de que Tesseract OCR esté instalado y configurado correctamente en tu máquina.

**Descripción General del Script**:

El script sigue estos pasos:

**1. Convierte el archivo PDF en imágenes (una imagen por página)**.
**2. Corrige la inclinación de cada imagen**.
**3. Utiliza Tesseract OCR para extraer texto de cada imagen**.
**4. Elimina los encabezados y pies de página del texto extraído**.
**5. Guarda el texto extraído en un documento de Word.**
**6. Convierte el documento de Word a PDF.**

**Ejecutar el Script**:

Reemplaza 'PUT THE FILENAME OF THE PDF HERE' con la ruta y el nombre de tu archivo PDF y ejecuta el script:

'''
python script_name.py
'''

**Ejemplo de Salida**:

El script generará un archivo Word (*_output.docx) y un archivo PDF (*_output.pdf) con el texto extraído del PDF original.

**Registro de Errores**:

Si hay algún problema durante el procesamiento de las páginas, los errores se registrarán en un archivo llamado pdf_processing.log. Este archivo de log contendrá detalles sobre cualquier excepción o error encontrado durante la ejecución.

## Estructura del Código

- convert_pdf_to_images(pdf_file): Convierte un archivo PDF en una lista de imágenes, una por página.
- deskew(image): Corrige la inclinación de la imagen dada.
- extract_text_from_image(image): Extrae texto de una imagen dada usando Tesseract OCR.
- get_text_data_from_image(image): Extrae datos de texto detallados, incluyendo confianza, y elimina encabezados y pies de página.
- process_page(page): Procesa una imagen de página: corrige la inclinación y extrae los datos de texto.
- extract_text_from_pdf(pdf_file): Extrae texto de cada página del archivo PDF dado, procesando las páginas en paralelo.
- save_to_word(text_from_pdf, output_filename): Guarda el texto extraído en un documento de Word.
- convert_word_to_pdf(word_filename, pdf_filename): Convierte un documento de Word a PDF utilizando comtypes.

## Notas Adicionales

- Rendimiento: El script está diseñado para manejar eficientemente archivos PDF grandes aprovechando múltiples núcleos de la CPU para el procesamiento en paralelo. Sin embargo, el rendimiento puede variar dependiendo del tamaño y la complejidad del archivo PDF.
- Configuración de Tesseract: Puedes modificar la configuración de Tesseract en la función extract_text_from_image si necesitas usar un idioma diferente o personalizar el comportamiento del OCR.
- Interacción con Microsoft Word: Este script requiere que Microsoft Word esté instalado en tu sistema para poder convertir documentos de Word a PDF.

## Contribuciones
Si deseas contribuir a este proyecto, siéntete libre de bifurcar el repositorio y enviar una solicitud de extracción con tus cambios. Las contribuciones para mejorar el rendimiento, agregar nuevas características o corregir errores son siempre bienvenidas.

## Licencia
Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo LICENSE para más detalles.