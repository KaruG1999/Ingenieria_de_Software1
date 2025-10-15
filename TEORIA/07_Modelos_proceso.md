# Modelos de Proceso de Software

## 📚 Conceptos Fundamentales

### ¿Qué es un Proceso?

Un proceso es un **conjunto ordenado de tareas** que seguimos para crear un producto o proveer un servicio. Las tareas se realizan en un orden específico.

> **💡 Ejemplo cotidiano:** No puedes cocinar una torta antes de mezclar los ingredientes. Este orden lógico es lo que define un proceso.

### ¿Qué es un Proceso de Software?

Es un **conjunto de actividades y resultados asociados** que producen un producto de software.

## 🔄 Actividades Fundamentales

Todo proceso de software incluye estas cuatro actividades básicas:

### 1. **Especificación del Software** (Ingeniería de Requerimientos)
- Comprender y definir qué servicios necesita el sistema
- Identificar restricciones de operación y desarrollo
- **En resumen:** ¿Qué debe hacer el software?

### 2. **Desarrollo del Software**
- Convertir la especificación en un sistema ejecutable
- Incluye diseño y programación
- Se crean estructuras, modelos de datos, interfaces, etc.
- **En resumen:** Construir el software

### 3. **Validación del Software**
- Verificar que el sistema cumple con las especificaciones
- Asegurar que satisface las expectativas del cliente
- Incluye pruebas, inspecciones y revisiones
- **En resumen:** ¿Funciona correctamente?

### 4. **Evolución del Software**
- Mantenimiento continuo del sistema
- Realizar cambios y mejoras
- **En resumen:** Adaptar el software a nuevas necesidades

## 📋 ¿Qué es un Modelo de Proceso?

> **Definición ISO 12207-1:** Marco de referencia que contiene los procesos, actividades y tareas involucradas en el desarrollo, explotación y mantenimiento de un producto de software, abarcando su vida completa.

Es una **representación simplificada** que muestra cómo se organiza el trabajo en un proyecto de software.

### Características de un Modelo de Proceso:

✓ Establece todas las actividades necesarias  
✓ Utiliza recursos y está sujeto a restricciones  
✓ Genera productos intermedios y finales  
✓ Cada actividad tiene entradas y salidas definidas  
✓ Las actividades se organizan en secuencia  
✓ Existen principios que orientan las metas  

### Términos Equivalentes:
- Modelo de proceso
- Paradigma de software
- Ciclo de vida del software

---

## 🏗️ Tipos de Modelos

### Modelos Prescriptivos vs Descriptivos

**Modelos Prescriptivos:** Prescriben cómo *debería* hacerse el trabajo (elementos, actividades, flujo de trabajo).

**Modelos Descriptivos:** Describen cómo se hace *en la realidad*.

> **💭 Ideal:** Ambos modelos deberían coincidir

---

## 🔨 Modelos Tradicionales

### 1. Modelo en Cascada (Waterfall)

```
Requisitos → Diseño → Implementación → Pruebas → Mantenimiento
    ↓          ↓            ↓              ↓           ↓
```

**Características:**
- Cada etapa debe completarse antes de pasar a la siguiente
- Secuencial y lineal
- Fácil de explicar y entender

**❌ Dificultades:**
- No hay resultados concretos hasta el final
- "Congelar" una fase es poco realista
- Los errores más graves se encuentran al final
- Dificultad para eliminar fallas en etapas tardías
- No maneja bien los cambios de requisitos
- La necesidad de pruebas aumenta exponencialmente al final

**✅ Útil cuando:**
- Los requisitos están muy claros y son estables
- El proyecto es simple y predecible

### 2. Modelo en V

```
Requisitos ←→ Pruebas de Aceptación
    ↓                    ↑
  Diseño  ←→  Pruebas de Sistema
    ↓                    ↑
Diseño Detallado ←→ Pruebas de Integración
    ↓                    ↑
Codificación ←→ Pruebas Unitarias
```

**Características:**
- Relaciona cada fase de desarrollo con su fase de prueba correspondiente
- Si hay problemas en validación, se vuelve al lado izquierdo
- Énfasis en verificación y validación

### 3. Modelo de Prototipos

> **Concepto clave:** Un prototipo es un producto **parcialmente desarrollado** que permite examinar aspectos del sistema antes de construirlo completamente.

#### Tipos de Prototipos:

| Aspecto | Descartable | Evolutivo |
|---------|-------------|-----------|
| **Desarrollo** | Rápido y sin rigor | Riguroso |
| **Qué construir** | Solo partes problemáticas | Partes bien entendidas primero |
| **Objetivo** | Desecharlo después | Convertirlo en el sistema final |
| **Funcionalidad** | Limitada o nula | Completa gradualmente |

**✅ Proyectos candidatos:**
- Usuarios que no pueden definir requisitos inicialmente
- Sistemas con énfasis en interfaz de usuario
- Cuando hay aspectos técnicos por explorar
- Usuarios que no trabajan bien con modelos abstractos

**📌 Para asegurar el éxito:**
- Debe ser barato (< 10% del costo total)
- Desarrollarse rápidamente
- Permitir experimentación
- Equipo reducido
- Herramientas adecuadas

---

## 🌀 Modelos Evolutivos

Estos modelos se adaptan a la **evolución de los requisitos** en el tiempo.

### 1. Modelo de Desarrollo por Fases

El sistema se entrega en **piezas funcionales**. Dos sistemas en paralelo: operacional y en desarrollo.

#### Tipos:

**📦 Incremental:**
- Particiona el sistema por funcionalidad
- Cada entrega agrega un subsistema nuevo
```
Entrega 1: Módulo A
Entrega 2: Módulo A + Módulo B
Entrega 3: Módulo A + B + C
```

**🔄 Iterativo:**
- Entrega un sistema completo desde el principio
- Cada versión aumenta la funcionalidad
```
Versión 1: Sistema completo básico
Versión 2: Sistema con funcionalidad mejorada
Versión 3: Sistema con funcionalidad avanzada
```

### 2. Modelo en Espiral (Boehm)

Combina desarrollo con **gestión de riesgos**. Cada ciclo tiene cuatro sectores:

```
1. Establecimiento de objetivos
         ↓
2. Valoración y reducción del riesgo
         ↓
3. Desarrollo y validación
         ↓
4. Planeación
         ↓
   (vuelve al 1)
```

**Ventajas:**
- Incorpora objetivos de calidad
- Elimina errores tempranamente
- Permite iteraciones y vuelta atrás
- Identifica alternativas no atractivas al inicio
- Cada ciclo incluye revisión completa

**Características únicas:**
- Cada ciclo empieza identificando objetivos, alternativas y restricciones
- Se completa con revisión que incluye plan para el siguiente ciclo
- Ideal para proyectos grandes y complejos

---

## 🎯 Tips para Elegir un Modelo

| Situación | Modelo Recomendado |
|-----------|-------------------|
| Requisitos claros y estables | Cascada |
| Énfasis en pruebas | Modelo en V |
| Requisitos inciertos | Prototipos |
| Necesidad de entregas tempranas | Incremental |
| Proyecto complejo con riesgos | Espiral |
| Requisitos cambiantes | Iterativo/Evolutivo |

---

## 📖 Referencias Bibliográficas

- Sommerville, Capítulo 2, *Ingeniería de Software*, Pearson 2011
- Pressman, Capítulo 2, *Ingeniería de Software: Un enfoque práctico*, McGraw Hill 2021
- Pfleeger, Capítulo 2, *Software Engineering: Theory and Practice*, Prentice Hall 2010
- Norma ISO 12207-1

---

## 💡 Conceptos Clave para Recordar

1. **No existe un modelo perfecto** - cada proyecto requiere evaluar qué modelo se adapta mejor
2. **Los modelos tradicionales** funcionan bien cuando los requisitos son claros
3. **Los modelos evolutivos** son mejores cuando hay incertidumbre
4. **El prototipado** ayuda a clarificar requisitos ambiguos
5. **La gestión de riesgos** es fundamental en proyectos complejos (Espiral)
6. **Las entregas incrementales** generan valor temprano para el cliente