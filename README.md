# 📖 HYDROSMART

**Versión:** 9.5  
**Última actualización:** Mayo 2026  
**Autores:** Hernandez Silva Lucia, Mancio Almanzar Erik Alejandro, Rúa Salinas Diana Itzel y Sanchez Sanchez Karen Itzel  
**Institución:** Universidad Nacional Rosario Castellanos  
**Licenciatura:** Ciencia de Datos para Negocios  

---

## 📋 TABLA DE CONTENIDOS

1. [Descripción General](#1-descripción-general)
2. [Arquitectura del Sistema](#2-arquitectura-del-sistema)
3. [Requisitos e Instalación](#3-requisitos-e-instalación)
4. [Estructura del Proyecto](#4-estructura-del-proyecto)
5. [Módulos y Funcionamiento](#5-módulos-y-funcionamiento)
6. [Base de Datos y CSVs](#6-base-de-datos-y-csvs)
7. [Interfaz de Usuario](#7-interfaz-de-usuario)
8. [Algoritmos y Fórmulas](#8-algoritmos-y-fórmulas)
9. [Configuración y Personalización](#9-configuración-y-personalización)
10. [Guía de Uso](#10-guía-de-uso)
11. [Solución de Problemas](#11-solución-de-problemas)
12. [Referencias Técnicas](#12-referencias-técnicas)

---

## 1. DESCRIPCIÓN GENERAL

### 1.1 ¿Qué es HYDROSMART?

HYDROSMART es un **sistema de riego inteligente** que combina:
- **Simulación en tiempo real** de condiciones de campo
- **Inteligencia Artificial** para toma de decisiones
- **Procesamiento de Lenguaje Natural (NLP)** para control por voz/chat
- **Análisis predictivo** de estrés hídrico
- **Gestión sectorial** de parcelas agrícolas

### 1.2 Problema que Resuelve

En el Valle del Yaqui, Sonora:
- **Desperdicio de agua**: 40-60% en riego tradicional
- **Estrés hídrico**: Pérdida de rendimiento en cultivos
- **Falta de trazabilidad**: Decisiones basadas en experiencia, no en datos
- **Riego ineficiente**: Todo el campo recibe la misma cantidad de agua

### 1.3 Solución Propuesta

| Característica | Beneficio |
|----------------|-----------|
| **Monitoreo continuo** | Detección temprana de estrés hídrico |
| **Riego sectorial** | Ahorro de 38% en consumo de agua |
| **Alertas automáticas** | Respuesta inmediata a condiciones críticas |
| **NLP integrado** | Control intuitivo sin necesidad de interfaz compleja |
| **Trazabilidad completa** | Registro de todas las decisiones y eventos |

### 1.4 Tecnologías Utilizadas

```
Frontend:        Streamlit (Python)
Visualización:   Plotly, Matplotlib
Base de Datos:   CSV (SQLite compatible)
IA/NLP:          Algoritmos fuzzy matching (difflib)
Simulación:      Modelos de balance hídrico y evapotranspiración
Arquitectura:    MVC (Model-View-Controller) simplificado
```

---

## 2. ARQUITECTURA DEL SISTEMA

### 2.1 Diagrama de Flujo

```
┌─────────────────────────────────────────────────────────────┐
│                    CAPA DE PRESENTACIÓN                      │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐          │
│  │Streamlit│ │ Plotly  │ │ Matplot │ │  HTML/  │          │
│  │   UI    │ │ Gráficos│ │  lib    │ │   CSS   │          │
│  └───────── └─────────┘ ─────────┘ └─────────┘          │
└─────────────────────────────────────────────────────────────┘
                            ↕
┌─────────────────────────────────────────────────────────────┐
│                    CAPA DE LÓGICA                            │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐          │
│  │  NLP Engine │ │  Simulación │ │  Decisiones │          │
│  │  (Chat IA)  │ │  (Balance   │ │  (Reglas &  │          │
│  │             │ │   Hídrico)  │ │   Umbrales) │          │
│  └─────────────┘ └─────────────┘ └─────────────┘          │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐          │
│  │   Alertas   │ │  Cálculo    │ │  Histórico  │          │
│  │  (Webhooks) │ │    IEH      │ │  (Tendencias│          │
│  │             │ │             │ │   y Logs)   │          │
│  └─────────────┘ └─────────────┘ └─────────────┘          │
└─────────────────────────────────────────────────────────────┘
                            ↕
┌─────────────────────────────────────────────────────────────┐
│                    CAPA DE DATOS                             │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐          │
│  │ parcelas.csv│ │  riegos.csv │ │sensores.csv │          │
│  │ (Estado     │ │ (Historial  │ │ (Lecturas   │          │
│  │  actual)    │ │  de riego)  │ │  históricas)│          │
│  └─────────────┘ └─────────────┘ └─────────────┘          │
│  ┌─────────────┐ ┌─────────────┐                          │
│  │chat_log.csv │ │alertas.csv  │                          │
│  │(Consultas   │ │(Eventos     │                          │
│  │   NLP)      │ │ críticos)   │                          │
│  └─────────────┘ └─────────────┘                          │
└─────────────────────────────────────────────────────────────┘
```

### 2.2 Componentes Principales

| Componente | Función | Archivo/Línea |
|------------|---------|---------------|
| **Session State** | Variables globales de sesión | Líneas 13-24 |
| **NLPProcessor** | Procesamiento de lenguaje natural | Clase línea 87 |
| **init_data()** | Inicialización de datos y CSVs | Función línea 167 |
| **actualizar_sistema()** | Loop de simulación principal | Función línea 182 |
| **calcular_ieh()** | Cálculo de Índice de Estrés Hídrico | Función línea 29 |
| **balance_hidrico()** | Modelo de balance hídrico | Función línea 34 |
| **crear_mapa()** | Generación de visualización del dron | Función línea 267 |

---

## 3. REQUISITOS E INSTALACIÓN

### 3.1 Requisitos del Sistema

**Mínimos:**
- Python 3.11 o superior
- 2 GB RAM
- 500 MB espacio en disco
- Conexión a internet (solo para instalación)

**Recomendados:**
- Python 3.11+
- 4 GB RAM
- 1 GB espacio en disco
- Navegador moderno (Chrome, Firefox, Edge)

### 3.2 Instalación Paso a Paso

#### Paso 1: Instalar Python
```bash
# Verificar versión
python --version

# Debe mostrar: Python 3.11.x o superior
```

#### Paso 2: Clonar/Descargar el Proyecto
```bash
# Crear directorio
mkdir hydrosmart
cd hydrosmart

# Estructura inicial
mkdir data
```

#### Paso 3: Crear Archivo requirements.txt
```txt
streamlit==1.30.0
pandas==2.0.0
numpy==1.24.0
plotly==5.18.0
matplotlib==3.7.0
```

#### Paso 4: Instalar Dependencias
```bash
pip install -r requirements.txt
```

#### Paso 5: Ejecutar la Aplicación
```bash
streamlit run app.py
```

#### Paso 6: Acceder al Sistema
El navegador abrirá automáticamente en:
```
http://localhost:8501
```

### 3.3 Verificación de Instalación

Ejecutar prueba rápida:
```python
import streamlit as st
import pandas as pd
import numpy as np
import plotly.graph_objects as go

print("✅ Todas las dependencias instaladas correctamente")
```

---

## 4. ESTRUCTURA DEL PROYECTO

```
hydrosmart/
│
├── app.py                          # Archivo principal (TODO el sistema)
│   ├── Imports                     # Líneas 1-11
│   ├── Configuración               # Líneas 13-24
│   ├── Session State               # Líneas 26-37
│   ├── Funciones Técnicas          # Líneas 39-55
│   │   ├── calcular_ieh()          # Índice de Estrés Hídrico
│   │   └── balance_hidrico()       # Modelo de simulación
│   ├── Tema y CSS                  # Líneas 57-85
│   ├── Clase NLPProcessor          # Líneas 87-165
│   ├── Gestión de Datos            # Líneas 167-265
│   │   ├── init_data()             # Inicialización CSVs
│   │   ├── actualizar_sistema()    # Loop principal
│   │   └── iniciar_riego()         # Activación de riego
│   ├── Visualización               # Líneas 267-300
│   │   └── crear_mapa()            # Mapa con dron animado
│   └── Interfaz de Usuario         # Líneas 302-550
│       ├── Sidebar                 # Panel de control
│       └── Tabs                    # 9 pestañas principales
│
├── data/                           # Directorio de datos (autogenerado)
│   ├── parcelas.csv                # Estado actual de parcelas
│   ├── riegos.csv                  # Historial de riegos
│   └── sensores.csv                # Lecturas históricas
│
├── requirements.txt                # Dependencias Python
└── README.md                       # Este documento
```

---

## 5. MÓDULOS Y FUNCIONAMIENTO

### 5.1 Session State (Líneas 26-37)

**Propósito:** Mantener estado entre recargas de Streamlit

```python
if 'dark_theme' not in st.session_state: 
    st.session_state.dark_theme = True
```

**Variables:**
| Variable | Tipo | Descripción | Valor Inicial |
|----------|------|-------------|---------------|
| `dark_theme` | bool | Modo oscuro/claro | `True` |
| `dron_posicion` | int | Índice de parcela actual del dron | `0` |
| `dron_estado` | str | Estado del dron | `'iniciando'` |
| `parcelas_data` | DataFrame | Datos de parcelas | `None` |
| `historial_humedad` | list | Historial de lecturas | `[]` |
| `riego_automatico` | bool | Activar/desactivar auto-riego | `True` |
| `parcela_regando` | str | Nombre de parcela en riego | `None` |
| `chat_messages` | list | Historial de chat NLP | `[]` |
| `ultima_actualizacion` | float | Timestamp última actualización | `time.time()` |
| `comandos_procesados` | set | Hash de comandos para evitar duplicados | `set()` |
| `decisiones_log` | list | Registro de decisiones IA | `[]` |
| `alertas_log` | list | Registro de alertas críticas | `[]` |

### 5.2 Funciones Técnicas (Líneas 39-55)

#### `calcular_ieh(humedad, cc=40.0, pmp=20.0)`

**Descripción:** Calcula el Índice de Estrés Hídrico (IEH)

**Fórmula:**
```
IEH = ((Humedad - PMP) / (CC - PMP)) × 100
```

**Parámetros:**
- `humedad`: Humedad actual del suelo (%)
- `cc`: Capacidad de Campo (40% - valor típico Vertisol)
- `pmp`: Punto de Marchitez Permanente (20%)

**Retorno:** Valor entre 0-100%
- 0% = Marchitez permanente
- 100% = Capacidad de campo
- >100% = Saturación

**Código:**
```python
def calcular_ieh(humedad, cc=40.0, pmp=20.0):
    return round(max(0, min(100, ((humedad - pmp) / (cc - pmp)) * 100)), 1)
```

#### `balance_hidrico(humedad_ant, precipitacion=0, evapotranspiracion=1.2, riego=0)`

**Descripción:** Simula el balance hídrico del suelo

**Ecuación:**
```
H_nueva = H_anterior + Precipitación + Riego - Evapotranspiración
```

**Parámetros:**
- `humedad_ant`: Humedad anterior (%)
- `precipitacion`: Agua por lluvia (mm o %)
- `evapotranspiracion`: Pérdida por ET (mm/hora, default 1.2)
- `riego`: Agua aplicada por riego (mm o %)

**Retorno:** Nueva humedad (0-100%)

**Código:**
```python
def balance_hidrico(humedad_ant, precipitacion=0, evapotranspiracion=1.2, riego=0):
    nueva = humedad_ant + precipitacion + riego - evapotranspiracion
    return round(max(0, min(100, nueva)), 1)
```

### 5.3 Clase NLPProcessor (Líneas 87-165)

**Propósito:** Procesar lenguaje natural para control por chat

#### Constructor `__init__(self, parcelas_df)`
```python
def __init__(self, parcelas_df):
    self.parcelas = parcelas_df
    self.names = parcelas_df['nombre'].tolist()
```

#### Método `_fuzzy_parcel(self, text)`

**Descripción:** Encuentra la parcela más similar al texto ingresado

**Algoritmo:** Fuzzy matching con `difflib.SequenceMatcher`

**Proceso:**
1. Tokeniza el texto en palabras
2. Genera candidatos (palabras individuales y combinaciones)
3. Compara cada candidato con nombres de parcelas
4. Retorna el nombre con mayor similitud (>60%)

**Ejemplo:**
```python
>>> _fuzzy_parcel("regar bloque")
'Bloque401'

>>> _fuzzy_parcel("parcela 3")
'Esperanza'  # Si es la tercera en la lista
```

#### Método `procesar(self, texto)`

**Descripción:** Interpreta la intención del usuario y genera respuesta

**Flujo:**
```
1. Normalizar texto (minúsculas, strip)
2. Verificar duplicados (hash)
3. Detectar intención por palabras clave
4. Ejecutar acción correspondiente
5. Retornar respuesta formateada
```

**Intenciones Soportadas:**

| Intención | Palabras Clave | Acción | Ejemplo Respuesta |
|-----------|----------------|--------|-------------------|
| **Regar parcela** | regar, riego, agua, irrigar | `REGAR_PARCELA:{nombre}` | "✅ Riego iniciado en Bloque401" |
| **Regar todo** | todo, todas, sistema | `REGAR_TODO:{lista}` | "✅ Riego masivo en: A, B, C" |
| **Consultar humedad** | humedad, nivel, seco, mojado | Retorna % y IEH | "📊 Bloque401: 28.0% | IEH: 20.0%" |
| **Consultar dron** | dron, drone, ubicación | Retorna estado y posición | "🚁 patrullando en ITSON (Pos #1)" |
| **Consultar alertas** | alerta, crítico, urgente | Lista parcelas <40% | "🚨 2 Críticas: Bloque401, Bacum" |
| **Consultar temperatura** | temperatura, calor, grados | Retorna promedio | "🌡️ Promedio: 28.4°C" |
| **Consultar consumo** | consumo, litros, gasto | Suma riegos.csv | "💧 Registrado: 125,000 L" |

**Código de Ejemplo:**
```python
if any(w in t for w in ['regar', 'riego', 'agua']):
    if any(w in t for w in ['todo', 'todas', 'sistema']):
        crit = self.parcelas[self.parcelas['humedad'] < 40]
        return f"REGAR_TODO:{','.join(crit['nombre'].tolist())}"
    parcel = self._fuzzy_parcel(t)
    if parcel: 
        return f"REGAR_PARCELA:{parcel}"
```

### 5.4 Gestión de Datos (Líneas 167-265)

#### `init_data()`

**Propósito:** Inicializar CSVs con estructura y datos de ejemplo

**Proceso:**
1. Verificar si `parcelas_data` existe en session_state
2. Si no, crear DataFrame con 8 parcelas del Valle del Yaqui
3. Calcular IEH inicial para cada parcela
4. Crear directorio `data/` si no existe
5. Guardar CSVs iniciales

**Estructura parcelas.csv:**
```csv
id,nombre,cultivo,humedad,x,y,area_ha,estado,temp_c,watermark_cb,ieh
1,ITSON,Cedrela,85.0,10,15,0.35,óptimo,28.4,12,100.0
2,Bórquez,Aguacate,62.0,30,35,0.28,atención,29.1,28,70.0
...
```

**Columnas:**
- `id`: Identificador único (1-8)
- `nombre`: Nombre de la parcela
- `cultivo`: Tipo de cultivo
- `humedad`: Humedad actual (%)
- `x`, `y`: Coordenadas para visualización (0-100)
- `area_ha`: Área en hectáreas
- `estado`: óptimo/atención/crítico
- `temp_c`: Temperatura (°C)
- `watermark_cb`: Sensor Watermark (centibares)
- `ieh`: Índice de Estrés Hídrico (%)

#### `actualizar_sistema()`

**Propósito:** Loop principal de simulación (se ejecuta cada 0.8-3 segundos)

**Proceso Detallado:**

```python
def actualizar_sistema():
    # 1. Copiar datos actuales
    df = st.session_state.parcelas_data.copy()
    
    # 2. Para cada parcela:
    for i in df.index:
        humedad_ant = df.loc[i, 'humedad']
        
        # 3. Si está siendo regada:
        if st.session_state.parcela_regando == df.loc[i, 'nombre']:
            df.loc[i, 'humedad'] = balance_hidrico(humedad_ant, riego=2.5)
        # 4. Si no, decaimiento natural:
        else:
            df.loc[i, 'humedad'] = balance_hidrico(humedad_ant, evapotranspiracion=0.8)
        
        # 5. Recalcular IEH
        df.loc[i, 'ieh'] = calcular_ieh(df.loc[i, 'humedad'])
        
        # 6. Actualizar estado
        if df.loc[i, 'humedad'] >= 70:
            df.loc[i, 'estado'] = 'óptimo'
        elif df.loc[i, 'humedad'] >= 40:
            df.loc[i, 'estado'] = 'atención'
        else:
            df.loc[i, 'estado'] = 'crítico'
    
    # 7. Riego automático si está activado
    if st.session_state.riego_automatico and st.session_state.parcela_regando is None:
        crit = df[df['humedad'] < 35]
        if len(crit) > 0:
            iniciar_riego(crit.iloc[0]['nombre'], 'automático')
            # Registrar decisión
            st.session_state.decisiones_log.append({
                'hora': datetime.now().strftime('%H:%M:%S'),
                'accion': 'Riego Automático IA',
                'parcela': crit.iloc[0]['nombre'],
                'motivo': f"Humedad {crit.iloc[0]['humedad']:.1f}% < 35%"
            })
    
    # 8. Mover dron si está patrullando
    if st.session_state.dron_estado == 'patrullando' and st.session_state.parcela_regando is None:
        st.session_state.dron_posicion = (st.session_state.dron_posicion + 1) % len(df)
    
    # 9. Guardar en session_state y CSV
    st.session_state.parcelas_data = df
    df.to_csv('data/parcelas.csv', index=False)
    
    # 10. Agregar al historial
    if len(st.session_state.historial_humedad) < 50:
        st.session_state.historial_humedad.append({
            'timestamp': datetime.now().strftime('%H:%M:%S'),
            'datos': df[['nombre', 'humedad', 'ieh']].to_dict('records')
        })
    
    # 11. Generar alertas si hay críticas
    criticas = df[df['humedad'] < 40]
    if len(criticas) > 0:
        st.session_state.alertas_log.append({
            'hora': datetime.now().strftime('%H:%M:%S'),
            'tipo': 'Estrés Hídrico Detectado',
            'detalle': f"{len(criticas)} parcelas críticas",
            'accion': 'Activación de riego sectorial'
        })
```

**Frecuencia de Ejecución:**
- Velocidad 1x: Cada 3 segundos
- Velocidad 2x: Cada 1.5 segundos
- Velocidad 3x: Cada 0.8 segundos

#### `iniciar_riego(nombre, tipo='manual')`

**Propósito:** Activar sistema de riego en una parcela

**Proceso:**
```python
def iniciar_riego(nombre, tipo='manual'):
    # 1. Obtener datos de la parcela
    df = st.session_state.parcelas_data
    p = df[df['nombre'] == nombre].iloc[0]
    
    # 2. Calcular volumen de agua (5000 L/ha)
    litros = int(p['area_ha'] * 5000)
    
    # 3. Crear registro de riego
    riego = pd.DataFrame({
        'timestamp': [datetime.now().strftime('%Y-%m-%d %H:%M:%S')],
        'parcela': [nombre],
        'tipo': [tipo],  # manual/automático/sectorial
        'duracion_min': [5],
        'litros': [litros]
    })
    
    # 4. Guardar en CSV
    riegos = pd.read_csv('data/riegos.csv')
    pd.concat([riegos, riego], ignore_index=True).to_csv('data/riegos.csv', index=False)
    
    # 5. Actualizar estado del sistema
    st.session_state.parcela_regando = nombre
    st.session_state.dron_estado = 'regando'
    st.session_state.dron_posicion = p.name
    
    # 6. Registrar en log de decisiones
    st.session_state.decisiones_log.append({
        'hora': datetime.now().strftime('%H:%M:%S'),
        'accion': f'Riego {tipo.capitalize()}',
        'parcela': nombre,
        'motivo': 'Solicitud usuario' if tipo == 'manual' else 'Umbral crítico'
    })
    
    return litros
```

### 5.5 Visualización (Líneas 267-300)

#### `crear_mapa(t)`

**Propósito:** Generar mapa interactivo con dron animado

**Tecnología:** Plotly Graph Objects

**Componentes:**

1. **Fondo de Campo Agrícola:**
```python
fig.add_shape(type="rect", x0=0, y0=0, x1=100, y1=100,
              fillcolor="#1a472a" if is_dark else "#d4edda", 
              opacity=0.2, layer="below")
```

2. **Surcos Simulados:**
```python
for i in range(0, 100, 8):
    fig.add_shape(type="line", x0=0, y0=i, x1=100, y1=i,
                 line=dict(color="#2d5a3d", width=1, dash="dot"))
```

3. **Parcelas (Marcadores):**
```python
colors = {'óptimo': '#22c55e', 'atención': '#f59e0b', 'crítico': '#ef4444'}
for _, r in df.iterrows():
    fig.add_trace(go.Scatter(
        x=[r['x']], y=[r['y']],
        mode='markers+text',
        marker=dict(
            size=40 if r['nombre']==st.session_state.parcela_regando else 28,
            color=colors[r['estado']],
            line=dict(color='white', width=2)
        ),
        text=[f"🌾<br>{r['nombre']}<br>{r['humedad']:.0f}%"]
    ))
```

4. **Dron Animado:**
```python
dp = df.iloc[st.session_state.dron_posicion]
fig.add_trace(go.Scatter(
    x=[dp['x']], y=[dp['y']],
    marker=dict(size=55, color='#3b82f6'),
    text=['🚁'],
    textfont=dict(size=22)
))
```

5. **Ruta del Dron:**
```python
if st.session_state.dron_estado == 'patrullando':
    fig.add_trace(go.Scatter(
        x=df['x'], y=df['y'],
        mode='lines',
        line=dict(color='#3b82f6', width=2, dash='dash'),
        opacity=0.5
    ))
```

**Configuración del Layout:**
```python
fig.update_layout(
    height=520,
    xaxis=dict(range=[0,100], visible=False),
    yaxis=dict(range=[100,0], visible=False),  # Invertido (coordenadas de imagen)
    plot_bgcolor=t['bg'],
    paper_bgcolor=t['bg'],
    margin=dict(l=0,r=0,t=30,b=0),
    showlegend=False,
    title=dict(
        text=f"🚁 {st.session_state.dron_estado.upper()} | {dp['nombre']} | {dp['humedad']:.1f}%",
        font=dict(size=14, color=t['text']),
        x=0.5  # Centrado
    )
)
```

---

## 6. BASE DE DATOS Y CSVS

### 6.1 Estructura de Archivos

#### `data/parcelas.csv`
**Propósito:** Estado actual del sistema

| Columna | Tipo | Descripción | Ejemplo |
|---------|------|-------------|---------|
| `id` | int | ID único | 1 |
| `nombre` | str | Nombre de parcela | "ITSON" |
| `cultivo` | str | Tipo de cultivo | "Cedrela" |
| `humedad` | float | Humedad actual (%) | 85.0 |
| `x` | int | Coordenada X (0-100) | 10 |
| `y` | int | Coordenada Y (0-100) | 15 |
| `area_ha` | float | Área en hectáreas | 0.35 |
| `estado` | str | Estado (óptimo/atención/crítico) | "óptimo" |
| `temp_c` | float | Temperatura (°C) | 28.4 |
| `watermark_cb` | int | Sensor Watermark (cB) | 12 |
| `ieh` | float | Índice de Estrés Hídrico | 100.0 |

**Frecuencia de Actualización:** Cada ciclo de simulación (0.8-3 segundos)

#### `data/riegos.csv`
**Propósito:** Historial de riegos aplicados

| Columna | Tipo | Descripción | Ejemplo |
|---------|------|-------------|---------|
| `timestamp` | str | Fecha y hora | "2026-05-25 14:30:00" |
| `parcela` | str | Nombre de parcela | "Bloque401" |
| `tipo` | str | Tipo de riego | "automático" |
| `duracion_min` | int | Duración en minutos | 5 |
| `litros` | int | Volumen aplicado | 1100 |

**Frecuencia de Actualización:** Cada vez que se activa un riego

#### `data/sensores.csv`
**Propósito:** Lecturas históricas de sensores (preparado para expansión)

| Columna | Tipo | Descripción |
|---------|------|-------------|
| `timestamp` | str | Fecha y hora |
| `parcela_id` | int | ID de parcela |
| `humedad` | float | Humedad (%) |
| `temperatura` | float | Temperatura (°C) |
| `watermark` | int | Watermark (cB) |

**Nota:** Actualmente no se utiliza activamente, pero está preparado para integración con sensores IoT reales.

### 6.2 Operaciones CRUD

**Create:**
```python
# Crear nuevo registro de riego
riego = pd.DataFrame({...})
riegos_df = pd.read_csv('data/riegos.csv')
pd.concat([riegos_df, riego], ignore_index=True).to_csv('data/riegos.csv', index=False)
```

**Read:**
```python
# Leer datos actuales
parcelas_df = pd.read_csv('data/parcelas.csv')
```

**Update:**
```python
# Actualizar humedad
df.loc[idx, 'humedad'] = nueva_humedad
df.to_csv('data/parcelas.csv', index=False)
```

**Delete:** (No se implementa - se mantiene historial completo)

---

## 7. INTERFAZ DE USUARIO

### 7.1 Layout General

```
┌─────────────────────────────────────────────────────────────┐
│  HEADER: Título del Sistema                                 │
├──────────────┬──────────────────────────────────────────────┤
│              │                                              │
│   SIDEBAR    │              CONTENIDO PRINCIPAL             │
│   (Control)  │              (9 Pestañas/Tabs)               │
│              │                                              │
│              │  ┌──────────────────────────────────────┐  │
│              │  │                                      │  │
│              │  │           TAB ACTIVA                 │  │
│              │  │                                      │  │
│              │  └──────────────────────────────────────┘  │
└──────────────┴──────────────────────────────────────────────┘
```

### 7.2 Sidebar (Panel Lateral)

**Componentes:**

1. **Header:**
   - Título: "Centro de Control"
   - Divider: Arcoíris

2. **Toggle Modo Oscuro:**
   ```python
   st.session_state.dark_theme = st.toggle("🌙 Modo Oscuro", value=True)
   ```

3. **Toggle Auto Riego:**
   ```python
   st.session_state.riego_automatico = st.toggle("🤖 Auto Riego", value=True)
   ```

4. **Selector de Velocidad:**
   ```python
   velocidad = st.select_slider("⚡ Velocidad", options=['1x', '2x', '3x'], value='1x')
   ```

5. **Estado del Dron:**
   ```python
   st.markdown(f'<div class="dron-status">
       <b>🚁 Estado:</b> {st.session_state.dron_estado.upper()}
       <br><b>📍 Posición:</b> #{st.session_state.dron_posicion + 1}
   </div>')
   ```

6. **KPIs (Métricas Clave):**
   - Humedad Promedio (%)
   - Parcelas Críticas (count)
   - Litros Usados Hoy (L)

7. **Timestamp:**
   - Hora actual de actualización

### 7.3 Pestañas Principales

#### **Tab 1: 🗺️ Mapa**

**Componentes:**
- Gráfico Plotly del mapa con dron
- 8 botones de riego rápido (uno por parcela)
- Formato: `🟢 ITSON \| 85.0%`

**Interacción:**
- Click en botón → Inicia riego en esa parcela
- Dron se mueve automáticamente a la parcela
- Animación de riego (hover del dron)

#### **Tab 2: 📊 Análisis**

**Componentes:**
1. **Gráfica de Barras (Humedad Actual):**
   - X: Nombre de parcelas
   - Y: Humedad (%)
   - Color: Verde/Amarillo/Rojo según estado

2. **Gráfica de Líneas (Tendencia):**
   - Últimas 12 lecturas de 3 parcelas representativas
   - Muestra evolución temporal

3. **Tabla de Datos:**
   - Columnas: nombre, cultivo, humedad, ieh, estado, temp_c

#### **Tab 3: 💬 Control IA**

**Componentes:**
- Historial de chat (últimos 12 mensajes)
- Input de chat (`st.chat_input`)
- Ejemplos de comandos

**Flujo:**
```
Usuario escribe → NLP procesa → Sistema ejecuta → Respuesta en chat
```

#### **Tab 4: 📋 Datos**

**Componentes:**
- Botón de descarga CSV Parcelas
- Tabla completa de parcelas
- Botón de descarga CSV Riegos
- Tabla de historial de riegos

#### **Tab 5: 🎯 Sectores**

**Propósito:** Gestión por zonas independientes

**Estructura:**
```python
sectores = {
    'Zona A (Cereales)': df[df['cultivo'].isin(['Trigo', 'Maíz', 'Cedrela'])],
    'Zona B (Frutales)': df[df['cultivo'] == 'Aguacate'],
    'Zona C (Forrajes/Exp)': df[df['cultivo'].isin(['Alfalfa', 'Cártamo', 'Experimental'])]
}
```

**Visualización:**
- 3 columnas (una por zona)
- Tarjetas por parcela con:
  - Nombre y cultivo
  - Humedad e IEH
  - Estado (color)
- Botón "💧 Regar {Zona}"

#### **Tab 6: 💰 Economía**

**Propósito:** Proyección económica y precios de garantía

**Tabla de Escenarios:**
| Escenario | Producción (ton/ha) | Precio ($/ton) | Ingreso ($/ha) | Ahorro Agua | Estrés Hídrico |
|-----------|---------------------|----------------|----------------|-------------|----------------|
| Sequía Extrema | 2.1 | 8,200 | 17,220 | 0% | Alto |
| Condiciones Normales | 4.5 | 7,500 | 33,750 | 15% | Moderado |
| Óptimo (HydroSmart) | 6.8 | 6,900 | 46,920 | 38% | Controlado |

**Fórmulas:**
```
Ingreso = Producción × Precio
% Ahorro = [(Vol_Tradicional - Vol_Optimizado) / Vol_Tradicional] × 100
```

#### **Tab 7: 🏗️ Arquitectura**

**Propósito:** Evidencia visual del modelo

**Secciones:**

1. **Diagrama de Flujo (Mermaid):**
   ```mermaid
   graph TD
       A[Sensores] --> B[Base de Datos]
       B --> C{Motor IA}
       C --> D[Alertas]
       C --> E[Riego]
   ```

2. **Imágenes de Detección:**
   - **Mapa de Calor (Heatmap):**
     - 10×10 celdas
     - Colores: Rojo (0%) a Verde (100%)
     - Simula sensores distribuidos
   
   - **Curva de Decaimiento:**
     - Función exponencial: `H(t) = H₀ × e^(-kt)`
     - Línea punteada: Umbral crítico (40%)
     - Eje X: Horas (0-25)
     - Eje Y: Humedad %

3. **Explicación de Predicciones:**
   - Tiempo hasta estrés hídrico
   - Volumen de agua requerido
   - Ventana óptima de riego

4. **Generación de Alertas:**
   - Paso 1: Lectura de humedad
   - Paso 2: Cálculo de IEH
   - Paso 3: Comparación con umbrales
   - Paso 4: Disparo de alerta si < 40%
   - Paso 5: Riego automático si no hay respuesta

#### **Tab 8: 📜 Código**

**Propósito:** Evidencia de implementación técnica

**Bloques Desplegables:**

1. **Balance Hídrico:**
   ```python
   def balance_hidrico(humedad_ant, precipitacion=0, evapotranspiracion=1.2, riego=0):
       nueva = humedad_ant + precipitacion + riego - evapotranspiracion
       return round(max(0, min(100, nueva)), 1)
   ```

2. **Cálculo IEH:**
   ```python
   def calcular_ieh(humedad, cc=40.0, pmp=20.0):
       return round(max(0, min(100, ((humedad - pmp) / (cc - pmp)) * 100)), 1)
   ```

3. **Simulación y Decisión IA:**
   ```python
   if st.session_state.riego_automatico and st.session_state.parcela_regando is None:
       crit = df[df['humedad'] < 35]
       if len(crit) > 0:
           iniciar_riego(crit.iloc[0]['nombre'], 'automático')
   ```

4. **Predicción de Decaimiento:**
   ```python
   def predecir_humedad_futura(humedad_actual, tasa_decaimiento=0.8, horas=6):
       return max(0, humedad_actual - (tasa_decaimiento * horas))
   ```

#### **Tab 9: 📈 Resultados**

**Propósito:** Comparativa y trazabilidad

**Componentes:**

1. **Gráfica Comparativa:**
   - Barras agrupadas: "Sin Sistema" vs "Con HydroSmart"
   - Métricas: Agua consumida, Estrés hídrico, Rendimiento

2. **Registro de Decisiones:**
   - Tabla con últimas 10 decisiones
   - Columnas: hora, accion, parcela, motivo

3. **Historial de Alertas:**
   - Tabla con últimas 10 alertas
   - Columnas: hora, tipo, detalle, accion

4. **Evidencia de Detección:**
   - Explicación de parcelas críticas
   - Referencia a tabs Mapa y Sectores

---

## 8. ALGORITMOS Y FÓRMULAS

### 8.1 Balance Hídrico

**Ecuación General:**
```
ΔS = P + R - ET - D - RO

Donde:
ΔS = Cambio en almacenamiento de agua en el suelo
P = Precipitación
R = Riego aplicado
ET = Evapotranspiración
D = Drenaje profundo
RO = Escorrentía superficial
```

**Simplificación del Sistema:**
```
H_nueva = H_anterior + Riego - ET

Tasa de ET: 0.8-1.2%/hora (depende de temperatura y cultivo)
```

### 8.2 Índice de Estrés Hídrico (IEH)

**Fórmula:**
```
IEH = ((θ - θ_pmp) / (θ_cc - θ_pmp)) × 100

Donde:
θ = Humedad volumétrica actual
θ_pmp = Humedad en punto de marchitez permanente (20%)
θ_cc = Humedad en capacidad de campo (40%)
```

**Interpretación:**
- IEH < 45%: Estrés hídrico severo
- IEH 45-70%: Condiciones adecuadas
- IEH > 100%: Saturación (riesgo de asfixia radicular)

### 8.3 Evapotranspiración (ET₀)

**Método FAO Penman-Monteith (Simplificado):**
```
ET₀ = 0.0023 × (T_media + 17.8) × (T_max - T_min)^0.5 × Ra

Donde:
T_media = Temperatura media (°C)
T_max = Temperatura máxima (°C)
T_min = Temperatura mínima (°C)
Ra = Radiación extraterrestre (MJ/m²/día)
```

**En el Sistema:**
```python
# Tasa fija para simulación
evapotranspiracion = 1.2  # %/hora
```

### 8.4 Lámina de Riego

**Cálculo:**
```
LR = (ET₀ × Kc × Area) / Eficiencia

Donde:
LR = Lámina de riego (mm)
ET₀ = Evapotranspiración de referencia
Kc = Coeficiente de cultivo
Area = Superficie (ha)
Eficiencia = 0.6-0.9 (según método de riego)
```

**Volumen Aplicado:**
```python
litros = area_ha * 5000  # 5000 L/ha estándar
```

### 8.5 Fuzzy Matching (NLP)

**Algoritmo:** SequenceMatcher de difflib

**Fórmula de Similitud:**
```
similarity = 2.0 * M / T

Donde:
M = Número de elementos coincidentes
T = Total de elementos en ambas secuencias
```

**Umbral:** 60% (0.6) para considerar coincidencia

---

## 9. CONFIGURACIÓN Y PERSONALIZACIÓN

### 9.1 Parámetros Ajustables

**En el Código:**

| Parámetro | Línea | Valor Default | Descripción |
|-----------|-------|---------------|-------------|
| `cc` (Capacidad Campo) | 31 | 40.0 | % humedad máxima aprovechable |
| `pmp` (Punto Marchitez) | 31 | 20.0 | % humedad mínima |
| `tasa_decaimiento` | 195 | 0.8 | %/hora de pérdida de humedad |
| `umbral_riego_auto` | 212 | 35 | % humedad para activar riego |
| `umbral_alerta` | 239 | 40 | % humedad para alerta crítica |
| `volumen_riego` | 255 | 5000 | L/ha por riego |

### 9.2 Agregar Nuevas Parcelas

**Paso 1:** Modificar `init_data()`:
```python
st.session_state.parcelas_data = pd.DataFrame({
    'id': range(1, 10),  # Agregar una más
    'nombre': ['ITSON', 'Bórquez', ..., 'Nueva Parcela'],
    'cultivo': ['Cedrela', 'Aguacate', ..., 'Nuevo Cultivo'],
    'humedad': [85.0, 62.0, ..., 70.0],
    'x': [10, 30, ..., 50],
    'y': [15, 35, ..., 40],
    'area_ha': [0.35, 0.28, ..., 0.50],
    ...
})
```

**Paso 2:** Actualizar base de cultivos en sidebar:
```python
cultivos_db = {
    ...
    'Nuevo Cultivo': {
        'requerimiento': 'XXX mm/año',
        'optimo': 'XX%',
        'minimo': 'XX%',
        ...
    }
}
```

### 9.3 Cambiar Umbrales

**Ejemplo: Modificar umbral de riego automático de 35% a 30%:**

```python
# Línea 212
if st.session_state.riego_automatico and st.session_state.parcela_regando is None:
    crit = df[df['humedad'] < 30]  # Cambiar 35 por 30
```

### 9.4 Personalizar Tema de Colores

**En `get_theme()` (líneas 57-64):**
```python
def get_theme():
    return {
        'bg': '#0f172a' if st.session_state.dark_theme else '#f8fafc',
        'card': '#1e293b' if st.session_state.dark_theme else '#ffffff',
        'text': '#f1f5f9' if st.session_state.dark_theme else '#0f172a',
        'text_sec': '#94a3b8' if st.session_state.dark_theme else '#475569',
        'accent': '#3b82f6',      # Azul principal
        'success': '#22c55e',     # Verde
        'warning': '#f59e0b',     # Amarillo
        'danger': '#ef4444'       # Rojo
    }
```

---

## 10. GUÍA DE USO

### 10.1 Inicio del Sistema

```bash
# Terminal
cd hydrosmart
streamlit run app.py

# Navegador
http://localhost:8501
```

### 10.2 Flujo de Trabajo Típico

**Escenario 1: Monitoreo Pasivo**

1. Abrir sistema
2. Observar **Tab Mapa** para vista general
3. Revisar **Tab Análisis** para tendencias
4. Verificar **Sidebar** para KPIs rápidos
5. El sistema riega automáticamente si está activado

**Escenario 2: Intervención Manual**

1. Identificar parcela crítica (rojo en mapa)
2. Click en botón de riego de esa parcela
3. O usar chat: `"regar bloque"` o `"regar parcela 4"`
4. Observar animación del dron
5. Verificar aumento de humedad en tiempo real

**Escenario 3: Consulta por Voz/Chat**

```
Usuario: "¿qué parcelas necesitan riego?"
Sistema: "🚨 2 Críticas: Bloque401: 28.0%, Bacum: 34.0%"

Usuario: "humedad promedio"
Sistema: "📊 Promedio: 56.3%"

Usuario: "dónde está el dron"
Sistema: "🚁 patrullando en ITSON (Pos #1)"

Usuario: "regar todo"
Sistema: "✅ Riego masivo activado en: Bloque401, Bacum"
```

**Escenario 4: Riego Sectorial**

1. Ir a **Tab Sectores**
2. Revisar estado de cada zona
3. Click en "💧 Regar Zona A (Cereales)"
4. Sistema riega todas las parcelas de esa zona

**Escenario 5: Análisis Económico**

1. Ir a **Tab Economía**
2. Comparar escenarios
3. Exportar datos para presentación
4. Justificar inversión en el sistema

**Escenario 6: Documentación Técnica**

1. Ir a **Tab Arquitectura**
2. Capturar diagramas de flujo
3. Ir a **Tab Código**
4. Capturar bloques de código
5. Ir a **Tab Resultados**
6. Capturar gráficas comparativas

### 10.3 Comandos NLP Disponibles

| Categoría | Comando | Respuesta del Sistema |
|------------|---------|----------------------|
| **Riego** | "regar [parcela]" | Inicia riego en parcela específica |
| | "regar todo" | Riega todas las parcelas críticas |
| | "activar riego en [nombre]" | Sinónimo de regar |
| **Consulta** | "humedad [parcela]" | Muestra % e IEH |
| | "humedad promedio" | Muestra promedio del sistema |
| | "quién necesita agua" | Lista parcelas críticas |
| | "alertas" | Muestra alertas activas |
| **Estado** | "dónde está el dron" | Ubicación y estado del dron |
| | "estado del sistema" | Resumen general |
| | "temperatura" | Temperatura promedio |
| **Consumo** | "cuánta agua se usó" | Total litros registrados |
| | "consumo hoy" | Consumo del día actual |

### 10.4 Interpretación de Alertas

**Alerta Crítica (Rojo):**
```
🚨 Estrés Hídrico Detectado
Parcela: Bloque401
Humedad: 28.0%
IEH: 20.0%
Acción: Riego automático activado
```

**Significado:**
- Humedad < 40% (umbral crítico)
- IEH < 45% (estrés severo)
- Riesgo de pérdida de rendimiento
- Acción inmediata requerida

**Alerta de Atención (Amarillo):**
```
⚠️ Monitoreo Requerido
Parcela: Esperanza
Humedad: 45.0%
IEH: 62.5%
Acción: Programar riego en próximas 6 horas
```

### 10.5 Exportación de Datos

**CSV Parcelas:**
1. Ir a **Tab Datos**
2. Click "📥 CSV Parcelas"
3. Archivo: `parcelas.csv`
4. Usar en Excel, Python, Power BI

**CSV Riegos:**
1. Ir a **Tab Datos**
2. Click "📥 CSV Riegos"
3. Archivo: `riegos.csv`
4. Análisis de consumo histórico

**Capturas de Pantalla:**
- Usar `Print Screen` o herramienta de recortes
- Formato recomendado: PNG (alta calidad)
- Resolución: 1920×1080 mínimo

---

## 11. SOLUCIÓN DE PROBLEMAS

### 11.1 Errores Comunes

**Error: `KeyError: 'dark_theme'`**

**Causa:** Session state no inicializado

**Solución:**
```python
# Asegurar que estas líneas estén al inicio (líneas 26-37)
if 'dark_theme' not in st.session_state: 
    st.session_state.dark_theme = True
```

---

**Error: `ValueError: All arrays must be of the same length`**

**Causa:** DataFrame con columnas de diferente longitud

**Solución:**
```python
# Verificar que todas las listas tengan el mismo número de elementos
eco_df = pd.DataFrame({
    'Escenario': ['A', 'B', 'C'],  # 3 elementos
    'Producción': [2.1, 4.5, 6.8],  # 3 elementos
    ...
})
```

---

**Error: `FileNotFoundError: data/parcelas.csv`**

**Causa:** Directorio `data/` no existe

**Solución:**
```bash
# Crear directorio manualmente
mkdir data

# O ejecutar init_data() que lo crea automáticamente
```

---

**Error: Streamlit no abre en el navegador**

**Causa:** Puerto 8501 ocupado

**Solución:**
```bash
# Especificar otro puerto
streamlit run app.py --server.port 8502

# O matar proceso en puerto 8501
netstat -ano | findstr :8501
taskkill /PID <PID> /F
```

---

**Problema: El dron no se mueve**

**Causa:** Velocidad en 0x o sistema pausado

**Solución:**
1. Verificar slider de velocidad en sidebar
2. Asegurar que esté en 1x, 2x o 3x
3. Verificar que `dron_estado` sea 'patrullando'

---

**Problema: Chat no responde**

**Causa:** NLP no detecta intención

**Solución:**
1. Usar palabras clave exactas (regar, humedad, dron)
2. Evitar frases muy complejas
3. Revisar consola para errores de NLP

### 11.2 Optimización de Rendimiento

**Problema: Sistema lento**

**Soluciones:**
1. Reducir historial de 50 a 20 registros:
   ```python
   if len(st.session_state.historial_humedad) < 20:  # Cambiar 50 por 20
   ```

2. Aumentar intervalo de actualización:
   ```python
   dt = {'1x': 5, '2x': 2.5, '3x': 1}[velocidad]  # Aumentar tiempos
   ```

3. Desactivar auto-riego si no se necesita:
   ```python
   st.session_state.riego_automatico = False
   ```

### 11.3 Backup y Restauración

**Crear Backup:**
```bash
# Copiar directorio completo
cp -r hydrosmart hydrosmart_backup_$(date +%Y%m%d)

# O solo datos
cp data/*.csv backup/
```

**Restaurar:**
```bash
# Copiar CSVs de backup a data/
cp backup/*.csv data/

# Reiniciar sistema
streamlit run app.py
```

---

## 12. REFERENCIAS TÉCNICAS

### 12.1 Documentación Oficial

**Streamlit:**
- Documentación: https://docs.streamlit.io
- API Reference: https://docs.streamlit.io/library/api-reference
- Session State: https://docs.streamlit.io/library/advanced-features/session-state

**Plotly:**
- Graph Objects: https://plotly.com/python/graph-objects/
- Subplots: https://plotly.com/python/subplots/

**Pandas:**
- DataFrame: https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html
- CSV I/O: https://pandas.pydata.org/docs/reference/io.html

### 12.2 Artículos Científicos

**Riego y Evapotranspiración:**
- Allen, R.G., Pereira, L.S., Raes, D., & Smith, M. (1998). *Crop evapotranspiration - Guidelines for computing crop water requirements*. FAO Irrigation and Drainage Paper 56.
- Villaseñor-López, M., et al. (2015). *Eficiencia del riego y productividad del agua en el Valle del Yaqui, Sonora*. ITSON.

**Agricultura de Precisión:**
- FAO. (2020). *El estado mundial de la agricultura y la alimentación*.
- CONACYT. (2024). *Precios de garantía para productos agrícolas básicos*.

### 12.3 Librerías Python

**Difflib (Fuzzy Matching):**
- Documentación: https://docs.python.org/3/library/difflib.html
- SequenceMatcher: https://docs.python.org/3/library/difflib.html#difflib.SequenceMatcher

**Matplotlib:**
- Heatmaps: https://matplotlib.org/stable/gallery/images_contours_and_fields/image_annotated_heatmap.html

### 12.4 Normatividad

**México:**
- NOM-001-SEMARNAT-2021: Límites de contaminantes en descargas de aguas residuales
- NOM-002-SEMARNAT-1996: Reúso de aguas residuales tratadas

**Internacional:**
- ISO 16122: Agricultura de precisión
- FAO Water Quality Guidelines

---

## APÉNDICE A: GLOSARIO DE TÉRMINOS

| Término | Definición |
|---------|------------|
| **CC** | Capacidad de Campo: Máxima cantidad de agua que el suelo puede retener |
| **PMP** | Punto de Marchitez Permanente: Humedad mínima antes de que la planta muera |
| **IEH** | Índice de Estrés Hídrico: Porcentaje de agua disponible para la planta |
| **ET₀** | Evapotranspiración de Referencia: Pérdida de agua por evaporación y transpiración |
| **Kc** | Coeficiente de Cultivo: Factor que ajusta ET₀ según tipo de cultivo |
| **Watermark** | Sensor de tensión de humedad del suelo (centibares) |
| **Vertisol** | Tipo de suelo arcilloso con alta contracción/expansión |
| **NLP** | Procesamiento de Lenguaje Natural (Natural Language Processing) |
| **Fuzzy Matching** | Algoritmo de coincidencia aproximada de texto |
| **Session State** | Almacenamiento de variables entre recargas de Streamlit |

---

**Documento elaborado por:** Hernandez Silva Lucia, Mancio Almanzar Erik Alejandro, Rúa Salinas Diana Itzel y Sanchez Sanchez Karen Itzel  
**Fecha:** Mayo 2026  
**Versión del documento:** 1.0  
**Licencia:** MIT License

---

**© 2026 HYDROSMART - Sistema de Riego Inteligente con IA**
