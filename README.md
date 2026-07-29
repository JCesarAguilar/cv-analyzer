# 🤖 CV Analyzer

Aplicación de IA que analiza currículums (CV) en PDF contra una descripción de puesto, y devuelve un informe estructurado y validado: experiencia, habilidades clave, fortalezas, áreas de mejora y un porcentaje de ajuste al puesto.

🔗 **Demo en vivo:** [agrega aquí tu link de Streamlit Cloud]

![CV Analyzer Demo](agrega-aqui-tu-screenshot.png)

---

## 📋 Descripción

CV Analyzer automatiza una tarea que normalmente hace un reclutador de forma manual: leer un CV, contrastarlo contra los requisitos de un puesto, y emitir un juicio estructurado sobre qué tan buen candidato es la persona.

El sistema usa un modelo de lenguaje (Google Gemini) a través de LangChain, con **salidas estructuradas y validadas** mediante Pydantic — la respuesta del modelo nunca es texto libre impredecible, siempre cumple un contrato de datos fijo.

## ✨ Funcionalidades

- 📄 Extracción de texto desde archivos PDF
- 🧠 Análisis del CV con IA (Google Gemini) contra una descripción de puesto específica
- ✅ Salida estructurada y validada (Pydantic): nombre, años de experiencia, habilidades clave, educación, experiencia relevante, fortalezas, áreas de mejora y % de ajuste al puesto
- 🛡️ Manejo de errores robusto: si algo falla, la app siempre devuelve una respuesta con la misma forma esperada, nunca se rompe
- 🎨 Interfaz interactiva construida con Streamlit

## 🏗️ Arquitectura

El proyecto sigue el principio de separación de responsabilidades, dividido en módulos independientes:

```
cv-analyzer/
├── app.py                    # Punto de entrada de la aplicación
├── models/
│   └── cv_model.py           # Contrato de datos (Pydantic) del análisis
├── prompts/
│   └── cv_prompts.py         # Prompts y templates para el LLM
├── services/
│   ├── cv_evaluator.py       # Orquesta el análisis: prompt + LLM + validación
│   └── pdf_processor.py      # Extracción de texto desde PDF
├── ui/
│   └── streamlit_ui.py       # Interfaz de usuario
└── requirements.txt
```

Esta estructura permite que, por ejemplo, cambiar la interfaz (de Streamlit a una API REST) no requiera tocar la lógica de negocio ni el contrato de datos.

## 🛠️ Tecnologías

- **Python 3.9+**
- **LangChain** — orquestación del flujo con el LLM
- **Google Gemini API** (`langchain-google-genai`) — modelo de lenguaje
- **Pydantic** — validación y estructura de datos
- **Streamlit** — interfaz de usuario
- **PyPDF2** — extracción de texto desde PDF

## 🚀 Instalación local

**1. Clona el repositorio**

```bash
git clone https://github.com/JCesarAguilar/cv-analyzer.git
cd cv-analyzer
```

**2. Crea y activa un entorno virtual**

```bash
python3 -m venv venv
source venv/bin/activate   # En Windows: venv\Scripts\activate
```

**3. Instala las dependencias**

```bash
pip install -r requirements.txt
```

**4. Configura tu API key**

Crea un archivo `.env` en la raíz del proyecto:

```
GOOGLE_API_KEY=tu-api-key-aqui
```

**5. Ejecuta la aplicación**

```bash
streamlit run app.py
```

La app quedará disponible en `http://localhost:8501`

## 📖 Uso

1. Sube un CV en formato PDF
2. Escribe o pega la descripción del puesto al que aplica el candidato
3. La IA analiza el CV y genera un informe estructurado con:
   - Datos generales y años de experiencia
   - Habilidades clave detectadas
   - Fortalezas y áreas de mejora
   - Porcentaje de ajuste al puesto (0–100%)

## 🗺️ Posibles mejoras futuras

- [ ] Soporte para comparar múltiples CVs a la vez
- [ ] Exportar el informe a PDF
- [ ] Historial de análisis previos
- [ ] Soporte para más formatos de entrada (DOCX)

## 📄 Licencia

Este proyecto es de uso educativo/portafolio.

---

Desarrollado por [JCesarAguilar](https://github.com/JCesarAguilar)
