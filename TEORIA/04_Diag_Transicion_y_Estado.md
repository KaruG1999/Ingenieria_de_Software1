# Diagramas de Transición de Estados (DTE)

## Contexto: Técnicas de Especificación de Requerimientos

Después de estudiar **Casos de Uso** (técnica estática), ahora exploramos las **técnicas dinámicas** que consideran cómo cambia el sistema a lo largo del tiempo.

### Clasificación de Técnicas

#### Técnicas Estáticas
- Describen el sistema a través de entidades, atributos y relaciones
- **No consideran cambios en el tiempo**
- Útiles cuando el tiempo no es factor crítico
- Ejemplos: Referencias indirectas, expresiones regulares, abstracciones de datos

#### Técnicas Dinámicas
- **Consideran cambios a lo largo del tiempo**
- El sistema está en estados particulares hasta que un estímulo lo obliga a cambiar
- Ejemplos: DTE, Tablas de decisión, Redes de Petri

---

## ¿Qué son los Diagramas de Transición de Estados?

### Definición
Los **DTE** modelan sistemas como **Máquinas de Estado Finito** que reaccionan a eventos específicos, cambiando de un estado a otro según una función de transición.

### Función Matemática
```
f(Si, Cj) = Sk
```
- **Si**: Estado actual
- **Cj**: Condición/evento que ocurre
- **Sk**: Estado resultante

### Definición Formal (Autómata Finito)
Un autómata finito es una **5-tupla (S,Σ,T,s,A)**:
- **Σ**: Alfabeto (conjunto de eventos/símbolos)
- **S**: Conjunto de estados
- **T**: Función de transición
- **s**: Estado inicial
- **A**: Estados finales/de aceptación

---

## Elementos Clave

### 🔵 Estados
- **Situación** en la que se encuentra el sistema en un momento dado
- Representados por círculos o rectángulos redondeados

### ➡️ Transiciones
- **Cambios** entre estados causados por eventos
- Representadas por flechas dirigidas
- Formato: `evento [condición] / acción`

### ⚡ Eventos
- **Sucesos significativos** que influyen en el comportamiento del sistema
- Ocurren en un punto específico del tiempo
- **Obligatorios** en cada transición

### Componentes de una Transición
- **Evento**: Obligatorio (ej: presionar botón)
- **Condición**: Opcional (ej: [credenciales_correctas])
- **Acción**: Opcional (ej: /mostrar_mensaje)

---

## Notación UML para DTE

### Tipos de Estados
```
○ → Estado Inicial (círculo negro)
◎ → Estado Final (círculo con borde)
⬜ → Estado Básico (rectángulo redondeado)
📦 → Estado Compuesto (con sub-estados)
```

---

## Metodología de Construcción

### Pasos para crear un DTE:

1. **Identificar los estados** del sistema
2. **Explotar estados complejos** si es necesario (crear sub-estados)
3. **Identificar el estado inicial**
4. **Definir transiciones** con eventos, condiciones y acciones
5. **Verificar consistencia**:
   - ✅ Todos los estados están definidos
   - ✅ Todos los estados son alcanzables
   - ✅ Se puede salir de todos los estados
   - ✅ El sistema responde a todas las condiciones posibles

---

## Ejemplo Práctico: Sistema de Autenticación

### Estados Identificados:
- **Pantalla de Inicio**
- **Formulario de Ingreso** 
- **Sesión Activa**
- **Finalizado**

### Diagrama:
```
[Inicio] → (Pantalla de Inicio)
           ↓ Ingresar
         (Formulario de Ingreso)
           ↓ Autenticar[credenciales_correctas]
         (Sesión Activa)
           ↓ Cerrar Sesión | timeout(5min)
         (Pantalla de Inicio)

Desde cualquier estado: cerrar_app → [Fin]
```

### Transiciones Detalladas:
- `Ingresar` → Pantalla de Inicio → Formulario de Ingreso
- `Autenticar [credenciales_correctas]` → Formulario → Sesión Activa
- `Autenticar [credenciales_incorrectas]` → Formulario → Formulario (/mostrar_error)
- `Cerrar Sesión` → Sesión Activa → Pantalla de Inicio
- `timeout(5min)` → Sesión Activa → Pantalla de Inicio
- `cerrar_app` → Cualquier Estado → Finalizado

---

## Características Importantes de los DTE

### Alcance del Modelo
- **Un DTE representa TODO el sistema**, no uno por cada requerimiento
- **Diferencia clave** con Casos de Uso (CU) o Historias de Usuario (HU): 
  - CU/HU: Un modelo por cada funcionalidad específica
  - DTE: Un modelo integrador que muestra el comportamiento global

### Ventajas de los DTE

### ✅ Beneficios:
- **Mejora la comprensión**: Mapa visual claro del comportamiento
- **Previene errores**: Detecta fallos de lógica en etapa de diseño
- **Valida el diseño**: Confirma que todos los requisitos están considerados
- **Facilita las pruebas**: Proporciona base para casos de prueba

### ❌ Limitaciones:
- **Complejidad**: Pueden volverse inmanejables con muchos estados
- **Enfoque único**: Modela un solo objeto/componente
- **Sin concurrencia**: No ideal para sistemas concurrentes

---

## ¿Cuándo usar DTE?

### Casos de Uso Ideales:
- 🕒 **Sistemas de tiempo real** (control de máquinas/dispositivos)
- 🖥️ **Interfaces de usuario complejas** (cambios de pantalla)
- 🔢 **Sistemas con estados finitos** (válvulas abiertas/cerradas)
- 🎮 **Algoritmos de control** (comportamiento basado en estado actual)

---

## Diferencia con Casos de Uso

| Aspecto | Casos de Uso | DTE |
|---------|-------------|-----|
| **Enfoque** | Funcional (qué hace) | Comportamental (cómo reacciona) |
| **Perspectiva** | Externa (usuario) | Interna (sistema) |
| **Tiempo** | Secuencia de pasos | Estados y transiciones |
| **Nivel** | Alto nivel | Detalle de implementación |

---

## Conclusión

Los **DTE** son herramientas poderosas para modelar el **comportamiento dinámico** de sistemas que cambian de estado en respuesta a eventos. Complementan perfectamente a los **Casos de Uso**, proporcionando una vista interna detallada de cómo el sistema reacciona y evoluciona a lo largo del tiempo.

Son especialmente útiles en **sistemas reactivos** donde el estado actual determina el comportamiento futuro del sistema.

---

*📚 Referencias: Pfleeger Cap. 4, Sommerville Cap. 5*

--- 

# Ejemplo Completo: Reloj Cronómetro - DTE

## Descripción del Sistema

### Hardware
Reloj digital con **pantalla** y **4 botones**:
- **B1**: Fecha/Start/Stop
- **B2**: Set/Reset  
- **B3**: Cronómetro/Reloj
- **B4**: Luz

### Funciones del Sistema
- Inicialmente (al colocar la pila) visualiza la hora prefijada
- Visualizar la hora actual
- Visualizar la fecha  
- Modificar hora y fecha
- Encender la luz por 5 segundos
- Iniciar / Detener / Resetear cronómetro
- Deja de funcionar al finalizarse la pila

---

## Aplicación de la Metodología DTE

### 1. Identificación de Estados

**Estados identificados:**
- **Visualizando Hora**
- **Visualizando Fecha** 
- **Visualizando Funciones Cronómetro**
- **Cronometrando**
- **Configurando Hora y Fecha**

### 2. Identificación de Estados Complejos

**Estado complejo detectado: Configurando Hora y Fecha**
- Permite modificar múltiples dígitos:
  - Hora (horas, minutos, segundos)
  - Fecha (día, mes, año)
- Se navega entre dígitos con B3
- Se modifican valores con B1

### 3. Estado Inicial

**Estado inicial:** `Visualizando Hora`
- **Evento disparador:** Se coloca la pila
- El sistema inicia mostrando la hora prefijada

---

## Análisis de Transiciones por Estado

### 4. Condiciones y Acciones para cada Estado

#### 📱 Estado: Visualizando Hora
```
B1 → Visualizando Fecha
B2 → Configurando Hora y Fecha  
B3 → Visualizando Funciones Cronómetro
B4 / Encender Luz por 5 seg → Visualizando Hora
```

#### 📅 Estado: Visualizando Fecha  
```
B1 → Visualizando Hora
B2 → Visualizando Hora
B3 → Visualizando Hora
B4 / Encender Luz por 5 seg → Visualizando Fecha
```
*Nota: Desde fecha, cualquier botón excepto B4 regresa a visualizar hora*

#### ⚙️ Estado: Configurando Hora y Fecha
```
B1 / Modificar Dígito → Configurando Hora y Fecha
B2 → Visualizando Hora
B3 / Pasar al siguiente dígito → Configurando Hora y Fecha  
B4 / Encender Luz por 5 seg → Configurando Hora y Fecha
```
*Secuencia de dígitos: Hora → Minuto → Segundo → Día → Mes → (cicla)*

#### ⏱️ Estado: Visualizando Funciones Cronómetro
```
B1 / Start → Cronometrando
B2 / Reset cronómetro → Visualizando Funciones Cronómetro
B3 → Visualizando Hora
B4 / Encender Luz por 5 seg → Visualizando Funciones Cronómetro
```

#### 🏃 Estado: Cronometrando
```
B1 / Stop → Visualizando Funciones Cronómetro  
B2 / Reset y Stop → Visualizando Funciones Cronómetro
B3 → Visualizando Hora
B4 / Encender Luz por 5 seg → Cronometrando
```

---

## Diagrama de Transición de Estados

### Representación Gráfica

```
                    [Se coloca la pila]
                            ↓
                   ┌─(Visualizando Hora)─┐
                   │         ↑          │
              B1   │         │          │ B3
                   ↓         │B1,B2,B3  ↓
        (Visualizando    ────┘    (Visualizando Funciones)
             Fecha)                     ↓ B1/Start
                                  (Cronometrando)
                                        ↑ B1/Stop
                                        └─────┘
                   
              B2   │                           
                   ↓                           
           (Configurando Hora)                 
                   ↑ B1,B3                    
                   └─────┘                    

    Transiciones globales desde cualquier estado:
    • B4 / Encender Luz → (mismo estado)
    • Se termina la pila → [FIN]
```

### 5. Verificación de Consistencia

#### ✅ Checklist de Consistencia:

**¿Se han definido todos los estados?**
- ✅ 5 estados principales identificados
- ✅ Estado inicial y final definidos

**¿Se pueden alcanzar todos los estados?**  
- ✅ Visualizando Hora: Estado inicial
- ✅ Visualizando Fecha: B1 desde Hora
- ✅ Configurando Hora: B2 desde Hora  
- ✅ Funciones Cronómetro: B3 desde Hora
- ✅ Cronometrando: B1 desde Funciones

**¿Se puede salir de todos los estados?**
- ✅ Todos los estados tienen transiciones de salida definidas
- ✅ Ningún estado "trampa" detectado

**¿El sistema responde a todas las condiciones posibles?**
- ✅ Los 4 botones tienen respuesta definida en cada estado
- ✅ Condiciones anormales: Se termina la pila → FIN
- ✅ Función luz (B4) disponible globalmente

---

## Tabla de Transiciones Completa

| Estado Actual | B1 | B2 | B3 | B4 | Pila Vacía |
|---------------|----|----|----|----|------------|
| **Visualizando Hora** | Fecha | Config | Cronómetro | Luz/Hora | FIN |
| **Visualizando Fecha** | Hora | Hora | Hora | Luz/Fecha | FIN |
| **Configurando Hora** | Modificar/Config | Hora | Siguiente/Config | Luz/Config | FIN |
| **Funciones Cronómetro** | Start/Cronometrando | Reset/Funciones | Hora | Luz/Funciones | FIN |
| **Cronometrando** | Stop/Funciones | Reset/Funciones | Hora | Luz/Cronometrando | FIN |

---

## Características Destacadas del Ejemplo

### 🔄 Auto-transiciones
- **B4 (Luz)**: Regresa al mismo estado después de 5 segundos
- **Configurando Hora**: B1 y B3 mantienen el estado mientras modifican

### 🔁 Transiciones Bidireccionales  
- **Funciones ⟷ Cronometrando**: Start/Stop con B1

### 🌐 Transiciones Globales
- **B4**: Funciona desde cualquier estado
- **Pila vacía**: Termina el sistema desde cualquier estado

### 🏗️ Estados Complejos
- **Configurando Hora**: Maneja múltiples sub-estados internos (dígitos)

---

## Validación del Diseño

### ✅ Requisitos Cumplidos:
1. **Visualización**: Hora y fecha ✅
2. **Configuración**: Modificación de hora/fecha ✅  
3. **Cronómetro**: Start/Stop/Reset ✅
4. **Iluminación**: Luz temporal ✅
5. **Navegación**: Cambio entre modos ✅
6. **Robustez**: Manejo de pila vacía ✅

### 📋 Casos de Prueba Sugeridos:
- Secuencia normal: Hora → Fecha → Hora
- Configuración completa: Modificar todos los dígitos
- Cronómetro: Start → Stop → Reset
- Transiciones de luz desde cada estado
- Comportamiento con pila vacía

---

*💡 Este ejemplo demuestra cómo un DTE puede modelar completamente el comportamiento de un sistema con múltiples modos de operación, estados complejos y transiciones globales.*