# Tablas de Decisión y Análisis Estructurado

## Parte 1: Tablas de Decisión

### ¿Qué es una Tabla de Decisión?

Es una herramienta que permite presentar de forma **concisa** las reglas lógicas para decidir acciones a ejecutar en función de condiciones específicas.

**Describe el sistema como un conjunto de:**
- **CONDICIONES:** satisfechas por el sistema en un momento dado
- **REGLAS:** para reaccionar ante estímulos cuando se reúnen determinados conjuntos de condiciones
- **ACCIONES:** a ser tomadas como resultado

---

## Estructura de una Tabla de Decisión

```
                REGLA1  REGLA2  REGLA3  ...
CONDICIONES:
  COND1           V       V       F      ...
  COND2           V       F       V      ...
  ...
  
ACCIONES:
  ACCION1         X               X      ...
  ACCION2                 X              ...
  ...
```

### Características Importantes
- Las condiciones son **simples** y toman solo valores **Verdadero (V)** o **Falso (F)**
- Cantidad de reglas: **2^N** donde N = cantidad de condiciones
- **X** marca qué acciones se ejecutan en cada regla

---

## Cómo Construir una Tabla de Decisión

### Paso 1: Identificar condiciones y acciones

Del enunciado, extraer:
- ¿Qué condiciones se evalúan?
- ¿Qué acciones se pueden tomar?

### Paso 2: Completar la tabla

**⚠️ REGLAS IMPORTANTES:**

**a) Condiciones opuestas:**
- Si hay condiciones excluyentes, colocar solo una
- La negativa se obtiene por la otra
- Ejemplo: Si hay "Es cliente" NO poner "No es cliente"
- Si hay n condiciones excluyentes, colocar n-1

**b) Condiciones atómicas:**
- Cada condición debe ser **indivisible**
- No combinar múltiples preguntas en una condición

### Paso 3: Construir las reglas

Generar todas las combinaciones posibles (2^N)

---

## Ejemplo Práctico: Remisión de Mercadería

**Enunciado:**
- Si el comprador NO es cliente → imprime mensaje de aviso y NO se remite
- Si NO hay stock y el comprador es cliente → NO se remite
- Si hay stock y el comprador es cliente → se remite

**Solución:**

```
                    REGLA1  REGLA2  REGLA3  REGLA4
CONDICIONES:
  Es cliente          V       V       F       F
  Hay stock           V       F       V       F
  
ACCIONES:
  Imprime mensaje                     X       X
  Se remite           X
  No se remite                X       X       X
```

**Análisis:** 2^2 = 4 reglas posibles

---

## Tipos de Especificaciones

### ✅ Especificaciones Completas
Determinan acciones para **todas las reglas posibles**

### ⚠️ Especificaciones Redundantes
Reglas con las **mismas condiciones** que determinan **acciones iguales**

### ❌ Especificaciones Contradictorias
Reglas con las **mismas condiciones** que especifican **acciones distintas**

**Ejemplo de Contradicción:**
```
        R1    R2
C1      V     V
C2      V     V
C3      V     V
A1      X          ← Mismas condiciones
A2            X    ← Acciones diferentes = CONTRADICCIÓN
```

**Ejemplo de Redundancia:**
```
        R1    R2
C1      V     V
C2      V     V
C3      V     V
A1      X     X    ← Mismas condiciones
A2      X     X    ← Mismas acciones = REDUNDANCIA
```

---

## Reducción de Complejidad (Simplificación)

### Usando el guion [—]

Combinar reglas donde una alternativa **no representa diferencia** en el resultado.

**El guion significa:** "La condición puede ser V o F, y aún así se realizará la acción"

**Ejemplo:**

**Antes (sin reducir):**
```
            R1    R2
C1          V     V
C2          V     F
A1          X     X
```

**Después (reducido):**
```
            R1
C1          V
C2          —
A1          X
```

### Aplicación con Álgebra de Boole

**Ejemplo de reducción:**

```
ORIGINAL:
            V     V     F     F
            V     F     V     F
A1                      X     X
A2          X
A3                X     X     X

REDUCIDO:
            V     F     
            V     —     
A1                X     
A2          X
A3                X     
```

---

## Ejemplo Completo: Incremento Salarial

**Enunciado:**
- Empleado altamente productivo → plus de productividad
- Empleado encargado → plus de encargado
- Infracción grave → elimina cualquier plus y descuenta 10%

**Tabla completa (8 reglas = 2^3):**

```
                                    V  V  V  V  F  F  F  F
Altamente productivo                V  V  F  F  V  V  F  F
Encargado                           V  F  V  F  V  F  V  F
Infracción grave                    V  F  V  F  V  F  V  F

Plus productividad                     X  X  X     X  X  X
Plus encargado                         X  X  X     X  X  X
Elimina cualquier plus              X     X     X
Descuento 10%                       X     X     X
No incrementa salario                                    X
```

---

## Checklist para Tablas de Decisión

Verificar siempre:

- [ ] ¿Están todas las condiciones identificadas?
- [ ] ¿Las condiciones son atómicas?
- [ ] ¿Eliminé condiciones opuestas redundantes?
- [ ] ¿Tengo 2^N reglas?
- [ ] ¿La tabla está completa? (todas las reglas tienen acciones)
- [ ] ¿No hay contradicciones? (mismas condiciones, diferentes acciones)
- [ ] ¿Puedo simplificar con guiones?
- [ ] ¿Es precisa y sin ambigüedades?

---

## Errores Comunes a Evitar

❌ **Incluir condiciones opuestas**
```
INCORRECTO:
  Es cliente
  No es cliente
  
CORRECTO:
  Es cliente (el "No es cliente" es F)
```

❌ **Condiciones no atómicas**
```
INCORRECTO:
  Cliente frecuente con descuento
  
CORRECTO:
  Es cliente frecuente
  Tiene descuento
```

❌ **Olvidar reglas**
```
Si hay 3 condiciones, debe haber 2^3 = 8 reglas
No omitir combinaciones
```

❌ **No verificar completitud**
```
Todas las reglas deben tener al menos una acción definida
```

---

## Parte 2: Análisis Estructurado - DFD

### ¿Qué es el Análisis Estructurado?

Técnica que permite lograr una **representación gráfica** para:
- Comprender más profundamente el sistema
- Comunicar a los usuarios lo comprendido
- No especifica aspectos físicos de implementación
- **Énfasis:** en el procesamiento y transformación de datos

---

## Diagrama de Flujo de Datos (DFD)

### Definición
Herramienta que visualiza un sistema como una **red de procesos funcionales** conectados por "conductos" y almacenamientos de datos.

**También llamado:** Diagrama de burbujas

**Representa:** La transformación de entradas a salidas

**Ideal para:** Sistemas operacionales donde las funciones son más importantes y complejas que los datos.

---

## Componentes de un DFD

### 1. Entidad Externa (Rectángulo)
```
┌─────────┐
│ Cliente │
└─────────┘
```
- Elemento del sistema que produce o recibe información
- Puede ser: hardware, persona, otro programa, otro sistema
- **NO forma parte del sistema a modelar**

### 2. Proceso (Círculo/Burbuja)
```
    ┌─────────┐
    │ Ingresar│
    │ nuevo   │
    │ cliente │
    └─────────┘
```
- Representa una **transformación** aplicada a los datos
- Modifica o procesa información

### 3. Flujo de Datos (Flecha)
```
────────────────────────────────────────────→
        Datos Nuevo Cliente
```
- Representa uno o más elementos de datos
- Indica la **dirección** del flujo

### 4. Almacén de Datos (Rectángulo abierto)
```
┌────────────────────────────────────────────
│ Clientes
└────────────────────────────────────────────
```
- Representa un lugar donde se guardan datos
- Puede ser: base de datos, archivo, tabla, etc.

---

## Diccionario de Datos

**Definición:** Listado organizado de todos los datos pertinentes al sistema.

### Características
- ✅ Permite revisar consistencia
- ✅ Representa el contenido de la información
- ✅ Define el significado de los flujos y almacenes
- ✅ Definición sin ambigüedades

### Un dato debe contener:
- **Tipo:** (String, Integer, Date, etc.)
- **Nombre:** identificador único
- **Descripción:** explicación clara de su propósito
- **Almacén:** (si aplica) donde se guarda

---

## Desarrollo de DFDs - Enfoque Jerárquico

### Perspectiva: De arriba hacia abajo (Top-Down)

### Pasos para Crear un DFD:

#### 1. Redactar lista de actividades
Identificar:
- Entidades externas
- Flujos de datos
- Procesos
- Almacenes de datos

#### 2. Crear Diagrama de Contexto
- Nivel más alto
- **Un solo proceso** que representa TODO el sistema
- Muestra entidades externas
- Muestra flujos desde/hacia el sistema
- **Panorama global:** entradas y salidas básicas

```
                  Datos entrada
┌─────────┐  ─────────────────────→  ┌─────────────┐
│ Entidad │                          │   Sistema   │
│ Externa │  ←─────────────────────  │   (único)   │
└─────────┘      Datos salida        └─────────────┘
```

#### 3. Dibujar Diagrama 0 (Nivel 0)
- Ampliación del Diagrama de contexto
- Entradas/salidas del contexto **permanecen**
- Incluye hasta **9 procesos** (máximo recomendado)
- Muestra almacenes de datos
- Muestra nuevos flujos internos

```
┌─────────┐       ┌─────────┐       ┌─────────┐
│Proceso 1│ ────→ │Proceso 2│ ────→ │Proceso 3│
└─────────┘       └─────────┘       └─────────┘
                       ↓
                  ┌─────────────────
                  │ Almacén datos
                  └─────────────────
```

#### 4. Dibujar Diagramas Hijos
- Un diagrama por cada proceso del Diagrama 0
- Descompone procesos en subprocesos
- Entradas/salidas del proceso padre **permanecen**
- Pueden aparecer nuevos almacenes y flujos

---

## Nivelación de DFD

### Nivelación Ascendente
**Agrupa** burbujas con algún criterio
- Combinar procesos relacionados
- Simplificar el diagrama

### Nivelación Descendente
**Descompone** burbujas funcionalmente
- Detalla cada proceso
- Muestra subprocesos internos

**Ejemplo de jerarquía:**
```
Contexto (Sistema completo)
    ↓
Nivel 0 (Procesos principales)
    ↓
Nivel 1 (Detalle de cada proceso)
    ↓
Nivel 2 (Más detalle si es necesario)
```

---

## Reglas y Buenas Prácticas para DFD

### ✅ Hacer:
- Mantener las entradas/salidas al descomponer
- Nombrar claramente todos los elementos
- Usar verbos para procesos ("Validar", "Calcular", "Registrar")
- Usar sustantivos para flujos y almacenes
- Máximo 9 procesos por nivel (legibilidad)
- Numerar procesos (1.0, 2.0, 3.0 en Nivel 0; 1.1, 1.2 en hijos)

### ❌ Evitar:
- Procesos sin entradas o sin salidas
- Flujos que no conectan nada
- Almacenes que no se leen ni escriben
- "Pozos negros" (procesos que solo reciben datos)
- "Generación espontánea" (procesos que solo generan datos)

---

## Ejemplo de Evolución de DFD

### Diagrama de Contexto
```
┌─────────┐                        ┌─────────────────┐
│         │   Pedido               │                 │
│ Cliente │ ────────────────────→  │ Sistema Ventas  │
│         │                        │                 │
│         │ ←────────────────────  │                 │
└─────────┘   Confirmación         └─────────────────┘
```

### Nivel 0 (Descomposición)
```
┌─────────┐     Pedido      ┌─────────────┐
│         │ ──────────────→ │  Validar    │
│ Cliente │                 │   Pedido    │
│         │                 └─────────────┘
│         │                        ↓
│         │                 Pedido Validado
│         │                        ↓
│         │                 ┌─────────────┐      ┌──────────────
│         │                 │  Procesar   │ ───→ │ Pedidos
│         │                 │   Pedido    │      └──────────────
│         │                 └─────────────┘
│         │                        ↓
│         │                 Confirmación
│         │ ←───────────────────────
└─────────┘
```

---

## Tips para Exámenes

### Para Tablas de Decisión:
1. **Contar condiciones** → calcular 2^N reglas
2. **Verificar opuestos** → incluir solo una
3. **Completar sistemáticamente** → patrón V/F
4. **Buscar simplificaciones** → usar guiones
5. **Verificar completitud** → todas las reglas con acciones

### Para DFD:
1. **Comenzar con contexto** → visión global
2. **Identificar entidades externas** → quién está fuera
3. **Listar procesos principales** → 5-9 procesos en Nivel 0
4. **Mantener balance** → entradas/salidas coinciden
5. **Usar diccionario** → definir todos los flujos

---

## Cuándo Usar Cada Técnica

### Tablas de Decisión
**Ideal para:**
- Lógica de negocio compleja
- Múltiples condiciones interrelacionadas
- Reglas de validación
- Políticas y procedimientos
- Cálculos con muchas condiciones

### DFD
**Ideal para:**
- Mostrar flujo de información
- Sistemas con énfasis en procesamiento de datos
- Visualizar transformaciones
- Comunicar con usuarios no técnicos
- Documentar sistemas operacionales

---

## Resumen Final

### Tablas de Decisión
> Herramienta para modelar **lógica de decisión compleja** mediante condiciones (V/F), reglas (2^N) y acciones, permitiendo verificar completitud y detectar inconsistencias.

### DFD (Análisis Estructurado)
> Representación gráfica del **flujo y transformación de datos** a través de procesos, mostrando entidades externas, flujos, procesos y almacenes en una jerarquía de niveles (contexto → nivel 0 → niveles hijos).