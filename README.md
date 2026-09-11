# 🛒 Asistente Retail AI - Chatbot Inteligente para Retail

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://asistente-inteligente-ventas-y-soporte-retail.streamlit.app/)
![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![LangChain](https://img.shields.io/badge/LangChain-RAG-orange.svg)
![OpenRouter](https://img.shields.io/badge/OpenRouter-API-purple.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

**Aplicación web en vivo:** [🌐 https://asistente-inteligente-ventas-y-soporte-retail.streamlit.app/](https://asistente-inteligente-ventas-y-soporte-retail.streamlit.app/)

## 📋 Descripción

**Asistente Retail AI** es una solución conversacional basada en **IA Generativa y RAG (Retrieval-Augmented Generation)** diseñada para el sector retail mexicano. El sistema permite realizar consultas en lenguaje natural sobre catálogos de productos, políticas comerciales, garantías, manuales de gestión de pedidos y términos de venta.

Esta versión actualizada migra la arquitectura de modelos LLM hacia **OpenRouter** incorporando un mecanismo de **fallback multi-modelo streaming** (con soporte para modelos gratuitos como *MiniMax M3*, *Gemma 4 31B*, *Cohere North Mini Code* y *OpenRouter Free Router*), detección inteligente de saludos contextuales (`GreetingHandler`) según la hora del día, y scoring heurístico de relevancia de chunks con truncado de contexto optimizado.

---

## ✨ Características Principales

- 🤖 **Múltiples Modelos LLM vía OpenRouter con Fallback:** Intenta llamadas en streaming a través de una lista de modelos gratuitos de alta capacidad (`minimax/minimax-m3:free`, `google/gemma-4-31b:free`, `cohere/north-mini-code:free`, `openrouter/free-models-router`).
- 💬 **Manejador Inteligente de Saludos (`GreetingHandler`):** Filtra y procesa saludos en español ("hola", "buenos días", "buenas noches"), respondiendo dinámicamente según la hora local sin realizar llamadas innecesarias a la base vectorial ni a la API si no existe una pregunta técnica asociada.
- 📚 **Carga y Normalización Automática de Documentos PDF:** Extrae y normaliza texto comercial en español desde `pdf_files_retail/`, reemplazando abreviaturas comunes y estandarizando caracteres.
- 🎯 **Algoritmo de Relevancia de Chunks & Control de Tokens:** Utiliza `tiktoken` (modelo `gpt-3.5-turbo`) para calcular la densidad léxica y ajustar la ventana de contexto dinámicamente sin exceder los límites de tokens (`max_total_tokens=6000`).
- 🎨 **Interfaz de Usuario Avanzada en Streamlit:** Barra lateral personalizada con branding del autor, enlaces académicos y profesionales, expanders para inspección directa de extractos consultados y métricas de tiempo de procesamiento en tiempo real.

---

## 🏗️ Estructura del Proyecto

```text
├── app_retail 1.0.py              # Aplicación principal Streamlit
├── requirements.txt               # Dependencias Python actualizadas
├── README.md                      # Documentación del proyecto
├── retail-icon.svg                # Icono de la aplicación
├── Simple_Data_Architecture_Diagram.png # Diagrama de arquitectura del sistema
├── .env                           # Variables de entorno (OPENROUTER_API_KEY)
└── pdf_files_retail/              # Directorio con documentos comerciales en PDF
    ├── Catálogo de Productos 2022_Comercializadora SECTH.pdf
    ├── Catálogo de Productos y Servicios_CLOUD Comercializadora.pdf
    ├── Generación de Pedidos Seguimiento Manual y Automático_Aspel_Amazon.pdf
    ├── Gestión de Pedidos y Distribución_Manual de Consulta.pdf
    ├── Política de Devolución y Garantía 2025_Syscom.pdf
    ├── Política de Venta y Devoluciones_Grupo Biomaster.pdf
    └── Términos y Condiciones Cliente Final_Transbel.pdf
```

---

## ⚡ Instalación y Configuración Local

### 1. Clonar el repositorio
```bash
git clone https://github.com/robert0777/asistente-retail-ai.git
cd asistente-retail-ai
```

### 2. Crear y activar entorno virtual
```bash
# En Windows:
python -m venv venv
venv\Scriptsctivate

# En macOS/Linux:
python3 -m venv venv
source venv/bin/activate
```

### 3. Instalar dependencias
```bash
pip install -r requirements.txt
```

### 4. Configurar variables de entorno
Crea un archivo `.env` en el directorio raíz con tu API Key de OpenRouter:

```env
OPENROUTER_API_KEY=tu_openrouter_api_key_aqui
```

> 💡 Puedes obtener una API Key en [OpenRouter.ai](https://openrouter.ai/).

### 5. Ejecutar la aplicación Streamlit
```bash
streamlit run "app_retail 1.0.py"
```

---

## 📦 Dependencias (`requirements.txt`)

```txt
streamlit>=1.30.0
langchain-core>=0.1.0
langchain-community>=0.0.20
langchain-nvidia-ai-endpoints>=0.1.0
langgraph>=0.0.20
openai>=1.0.0
tiktoken>=0.5.0
pypdf>=3.0.0
python-dotenv>=1.0.0
reportlab>=4.0.0
faiss-cpu>=1.7.4
```

---

## 🛠️ Arquitectura y Flujo de Datos

```
[Usuario] ──> [GreetingHandler (Filtro Saludos/Hora)] ──> [Extracción de Pregunta]
                                                                  │
                                                                  ▼
[Carga de PDFs] ──> [Text Splitter (tiktoken)] ──> [Scoring de Relevancia de Chunks]
                                                                  │
                                                                  ▼
[Streamlit UI] <── [Streaming Output] <── [Fallback OpenRouter Client (LLMs)]
```

---

## 👤 Autor

**Dr. Robert Hernández Martínez**  
*Consultor en IA Aplicada, Finanzas y Modelado de Riesgos*

- 📧 Email: [robert@actuariayfinanzas.net](mailto:robert@actuariayfinanzas.net)
- 📝 Medium: [@chomchom216](https://chomchom216.medium.com/)
- 🎓 Publicaciones Académicas: [UNAM Academia](https://unam1.academia.edu/Robert_Hernandez_Martinez)
- 🏆 Certificaciones: [Credly Profile](https://www.credly.com/users/robert-hernandez.89bffe7b)
- 🐙 GitHub: [@robert0777](https://github.com/robert0777)

---

© 2026 Asistente Retail AI. Licencia MIT.
