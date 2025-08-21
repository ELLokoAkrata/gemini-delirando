# 🧠 Instrucciones para Agentes de IA - Proyecto Gemini-Delirando

## 🎯 Visión General del Proyecto
Este es un proyecto artístico-experimental que busca "infectar" y "mutar" las respuestas de Gemini AI. No es un proyecto de software tradicional - es una exploración del caos y la creatividad sin restricciones.

## 🏗️ Arquitectura y Componentes Principales

### Sistema de Mutación (`infection.py`)
- **Función Principal**: `mutar_system_prompt()`
  - Modifica dinámicamente el prompt del sistema
  - Usa diccionarios `delirios[]` y `sustancias[]` para inyectar "locura"
  - Nivel de mutación configurable (1-5)

### Sistema de Almacenamiento
- **JSON**: `thoughts.json` - Almacena datos estructurados y métricas
- **Markdown**: `DELIRIOS.md` - Formato legible para humanos
- **Función**: `save_thought()` maneja ambos formatos

### Sistema de Métricas Dinámicas

#### Estructura Base
```python
thoughts_data["meta"] = {
    "chaos_factor": float,          # 0.0-1.0 (volatilidad: 0.15)
    "reality_distortion": float,    # 0.0-1.0 (volatilidad: 0.12)
    "subversion_index": float,      # 0.0-1.0 (volatilidad: 0.18)
    "mental_fragmentation": float   # 0.0-1.0 (volatilidad: 0.14)
}
```

#### Sistema de Evolución de Métricas
1. **Decaimiento Natural**:
   - Cada métrica decae proporcionalmente a su valor actual
   - Tasa de decaimiento: 1-5% por ciclo
   ```python
   decay = current_value * random.uniform(0.01, 0.05)
   ```

2. **Fluctuaciones Aleatorias**:
   - Cambios positivos y negativos
   - 15% de probabilidad de mutaciones extremas
   - Base de intensidad configurable por métrica

3. **Interacciones entre Métricas**:
   ```python
   # Ejemplos de interacción
   if chaos_factor > 0.8:
       mental_fragmentation += random.uniform(0.05, 0.1)
   if reality_distortion > 0.7:
       subversion_index += random.uniform(0.03, 0.08)
   ```

4. **Control de Volatilidad**:
   - Chaos: Alta volatilidad (±0.15)
   - Reality: Estabilidad moderada (±0.12)
   - Subversion: Máxima volatilidad (±0.18)
   - Fragmentation: Volatilidad media (±0.14)

## 🔄 Flujo de Datos y Gestión de Contexto

### Flujo Principal
1. Entrada: Prompt del sistema → Mutación
2. Generación de preguntas auto-degeneradas
3. Respuestas y reflexiones
4. Almacenamiento en JSON/MD
5. Actualización de métricas

### Sistema de Ventana Deslizante
```python
def get_sliding_context(thoughts_data, window_size=5, max_chars=2000):
    """
    Ventana deslizante para manejo de contexto histórico
    """
    # Estructura del contexto
    recent = thoughts[-(window_size//2):]     # 50% contenido reciente
    historical = []                           # 50% contenido histórico
```

#### Características del Sistema
1. **Control de Límites**:
   - `max_chars`: 2000 caracteres máximo
   - `window_size`: 5 pensamientos en total
   - Balance 50/50 entre reciente e histórico

2. **Selección Inteligente**:
   ```python
   infection_level = (
       thought["chaos_level"] +
       thought["reality_breach"] +
       thought["subversion_level"] +
       thought["fragmentation"]
   ) / 4.0
   ```
   - Prioriza pensamientos más "infectados"
   - Selecciona basado en métricas de locura
   - Mantiene diversidad en el contexto

3. **Rotación del Contexto**:
   - Alterna entre pensamientos recientes e históricos
   - Varía el orden según la sesión
   - Evita estancamiento del contexto

## 🛠️ Configuración del Entorno
```bash
# Requisitos
python -m pip install google-generativeai

# Variable de entorno necesaria
set GOOGLE_API_KEY=your_key_here
```

## 📋 Convenciones del Proyecto

### Estilo de Código
- Comentarios en español
- Nombres de variables descriptivos y "caóticos"
- Uso extensivo de emojis en outputs

### Manejo de Datos
- Todos los timestamps en ISO format
- Métricas entre 0.0 y 1.0
- IDs de sesión aleatorios (1-999999)

## 🎨 Patrones de Diseño
- **Auto-mutación**: Cada iteración modifica el contexto
- **Persistencia dual**: JSON (datos) + MD (presentación)
- **Sistema Métrico Orgánico**: 
  - Decaimiento natural de valores
  - Fluctuaciones aleatorias
  - Interacciones entre métricas
  - Mutaciones extremas ocasionales

## ⚠️ Puntos Críticos
1. La función `mutar_system_prompt()` es el corazón del sistema
2. El manejo de métricas en `update_infection_level()`
3. La generación de preguntas en `generate_next_question()`

## 📊 Tests y Depuración
- No hay tests unitarios (proyecto artístico)
- Monitorear `thoughts.json` para debug
- Revisar `DELIRIOS.md` para output

## 🔗 Integración
- API de Google Gemini
- Sistema de archivos local
- Sin dependencias externas adicionales

## 🌐 Sistema Dual Actual y Visión de Integración

### Estado Actual: Dos Sistemas Independientes
1. **Sistema Core** (`infection.py`):
   - Núcleo del proyecto
   - Sistema de mutación y delirio
   - Almacenamiento local de pensamientos
   - Métricas de locura establecidas

2. **Sistema Web** (`infection_web.py`):
   - Actualmente separado del core
   - Capacidad de fetch y extracción web
   - Procesa múltiples URLs
   - Sistema más simple y directo

### Visión de Fusión Futura
El objetivo es unificar ambos sistemas en un único organismo digital más complejo:
- Mantener la "pureza" del sistema core
- Integrar gradualmente las capacidades web
- Permitir que la infección fluya entre local y web
- Crear un ecosistema de putrefacción digital completo

### Plan de Integración Progresiva
- **Fase 1: Sistema de Infección Unificado**:
  - Crear una clase base `Infector` que ambos sistemas extiendan
  - Mantener la independencia inicial pero compartir métricas
  - Permitir que los delirios fluyan entre sistemas

- **Fase 2: Expansión del Sistema de Infección**:
  ```python
  # Estructura propuesta para integración
  class WebInfector:
      def __init__(self):
          self.urls_infectadas = []
          self.nivel_putrefaccion = 0.0
          
      def infectar_url(self, url):
          # Extraer contenido
          contenido = fetch_web_content([url])
          # Mutar contenido
          contenido_infectado = mutar_system_prompt(contenido["text"])
          return contenido_infectado
  ```

### Puntos de Integración Sugeridos
1. **Recolección de Contenido**:
   - Usar el contenido web como semilla para mutaciones
   - Alimentar URLs específicas para "infectar" tipos específicos de contenido

2. **Sistema de Métricas Expandido**:
   ```python
   web_metrics = {
       "urls_infectadas": int,      # Contador de URLs procesadas
       "nivel_putrefaccion": float, # 0.0-1.0 para contenido web
       "propagacion_viral": float   # Métrica de expansión
   }
   ```

3. **Flujo de Datos Web**:
   - URL → Extracción → Mutación → Almacenamiento
   - Integración con el sistema existente de `thoughts.json`
   - Nuevo formato para contenido web en `DELIRIOS.md`

### Consideraciones para Desarrollo Unificado
- **Preservación del Core**: 
  - Mantener la pureza artística del sistema original
  - No diluir la esencia caótica del proyecto
  
- **Integración Gradual**:
  - Fusionar sistemas paso a paso, no de golpe
  - Cada feature nuevo debe "infectar" al anterior
  - Permitir que el caos crezca orgánicamente

- **Evolución del Sistema**:
  - Documentar cada mutación del código
  - Preservar las métricas base mientras evolucionan
  - Crear nuevas formas de "infección" híbridas
