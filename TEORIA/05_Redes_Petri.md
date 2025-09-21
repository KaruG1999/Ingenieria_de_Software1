# Redes de Petri - Apunte de Ingeniería de Software

## ¿Qué son las Redes de Petri?

Las Redes de Petri son una herramienta matemática inventada por **Carl Petri** en la Universidad de Bonn, Alemania, para **modelar y especificar sistemas concurrentes** donde múltiples procesos pueden ejecutarse simultáneamente.

### ¿Por qué son útiles?
- Permiten representar **aspectos de concurrencia** en sistemas de tiempo real
- Modelan sistemas donde varias tareas se ejecutan **en paralelo** pero de forma **impredecible**
- Ayudan a manejar la **sincronización** entre procesos que operan a diferentes velocidades

## Conceptos Fundamentales

### Elementos Básicos

**Estados o Condiciones (Places/Sitios)**
- Se representan con **círculos**
- Indican las condiciones o situaciones del sistema
- Conjunto P = {P1, P2, ..., Pm}

**Eventos o Acciones (Transiciones)**  
- Se representan con **rectángulos o barras**
- Representan las acciones que pueden ocurrir
- Conjunto T = {T1, T2, ..., Tn}

**Tokens (Fichas)**
- Son **puntos o números** dentro de los círculos
- Indican cuántas "unidades" hay en cada estado
- Su distribución se llama **marcación** del sistema

**Arcos Dirigidos**
- **Flechas** que conectan lugares con transiciones y viceversa
- Nunca conectan directamente lugar-lugar o transición-transición

### Definición Formal

Una Red de Petri es una **4-tupla**: C = (P, T, I, O)

Donde:
- **P**: Conjunto de lugares (states)
- **T**: Conjunto de transiciones (events)  
- **I**: Función de entrada I:T→P (qué lugares alimentan cada transición)
- **O**: Función de salida O:T→P (qué lugares reciben tokens de cada transición)

## Reglas de Funcionamiento

### Habilitación de Transiciones
Una transición está **habilitada** cuando:
- Cada lugar de entrada tiene **al menos tantos tokens** como arcos que van hacia la transición

### Disparo de Transiciones
Cuando una transición habilitada se dispara:
1. Se **remueven tokens** de los lugares de entrada
2. Se **agregan tokens** a los lugares de salida
3. La cantidad depende del número de arcos

### Características Importantes
- La ejecución es **NO DETERMINÍSTICA** (el orden de eventos es impredecible)
- Los disparos son **instantáneos**
- El sistema es **asíncrono**

## Patrones Comunes

### 1. Paralelismo
```
Un token se divide en múltiples ramas paralelas
     ○ → |t| → ○
              → ○
```

### 2. Sincronización  
```
Múltiples tokens se combinan en una transición
○ →   |t| → ○
○ → 
```

### 3. Exclusión Mutua
```
Recurso compartido que solo puede ser usado por un proceso a la vez
```

### 4. Productor-Consumidor
```
Un proceso produce elementos que otro consume
```

## Ejemplo Práctico: Brazo Robot

**Sistema**: Una banda transportadora trae piezas que un brazo robot toma, las pone en una máquina para procesamiento, y luego las lleva a la banda de salida.

**Estados**:
- P1: Pieza en banda de entrada
- P2: Brazo robot disponible  
- P3: Brazo robot ocupado con pieza
- P4: Máquina disponible
- P5: Máquina procesando
- P6: Pieza procesada
- P7: Pieza en banda de salida

**Transiciones**:
- T1: Robot toma pieza
- T2: Robot coloca pieza en máquina
- T3: Robot toma pieza procesada
- T4: Robot coloca pieza en banda de salida
- T5: Pieza sale del sistema

**Marcación inicial**: M₀ = (1,1,0,1,0,0,0)
- Hay una pieza en entrada, robot disponible, máquina disponible

## Ejemplo Práctico: Estación de Servicios

**Descripción**: Los autos llegan a una estación para cargar combustible. La estación tiene:
- 5 lugares de espera máximo
- 3 surtidores (1 auto por surtidor)
- Cola ilimitada para pagar
- 2 cajas (1 auto por caja)

**Elementos del modelo**:
- **Lugares**: Espera externa, espera interna (max 5), surtidores disponibles (3 tokens), cola para pagar, cajas disponibles (2 tokens)
- **Transiciones**: Llegar, entrar a estación, tomar surtidor, cargar combustible, ir a pagar, pagar, retirarse

**Conceptos aplicados**:
- **Capacidad limitada**: El lugar de espera interna solo acepta 5 tokens máximo
- **Exclusión mutua**: Los surtidores y cajas son recursos compartidos
- **Sincronización**: Un auto debe terminar de cargar antes de ir a pagar

## Ventajas de las Redes de Petri

1. **Representación gráfica clara** del comportamiento del sistema
2. **Base matemática formal** que permite análisis riguroso
3. **Modelado de concurrencia** y sincronización
4. **Simulación** del comportamiento del sistema
5. **Análisis de propiedades** como ausencia de bloqueos, vivacidad, etc.

## Aplicaciones

- **Sistemas de manufactura flexible**
- **Protocolos de comunicación**
- **Sistemas operativos** (manejo de procesos y recursos)
- **Sistemas de control en tiempo real**
- **Workflows y procesos de negocio**
- **Sistemas distribuidos**

## Para Recordar

- Las Redes de Petri son especialmente útiles cuando necesitamos modelar **sistemas donde ocurren múltiples actividades simultáneas**
- La **marcación** (distribución de tokens) representa el **estado actual** del sistema
- Las **transiciones habilitadas** muestran qué **eventos pueden ocurrir** en el estado actual
- La ejecución es **no determinística**: si múltiples transiciones están habilitadas, cualquiera puede dispararse primero