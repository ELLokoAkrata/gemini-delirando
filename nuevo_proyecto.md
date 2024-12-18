# Tengo GOOGLE_API_KEY
# 
Como variable de entorno del sistema operativo

# Quiero que el script test.py use GOOGLE_API_KEY
# Para obtener la latitud y longitud de una ciudad

# Como hago?

Despues tengo esta documentación 
from google import genai

client = genai.Client(
    api_key="YOUR_API_KEY"
)
response = client.models.generate_content(
    model='gemini-2.0-flash-exp', contents='How does AI work?'
)
print(response.text)

Pero me gustaria usar estos parámetros en el script test.py
# Configuración del modelo de Google Generative AI
model_name = 'gemini-2.0-flash-exp'
harassment_setting = 'block_none'
temperature = 0.66
top_p = 1
top_k = 1
max_output_tokens = 1024

model = genai.GenerativeModel(
    model_name=model_name,
    safety_settings={'HARASSMENT': harassment_setting},
    generation_config={
        "temperature": temperature,
        "top_p": top_p,
        "top_k": top_k,
        "max_output_tokens": max_output_tokens
    }
)

# Pero necestimos darle un system.txt a nuestro estilo y un input de prueba, luego ejecutaras el script para probarlo y ver si funciona correctamente, luego veremos que más hacer
