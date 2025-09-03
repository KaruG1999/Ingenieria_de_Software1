# Guía Paso a Paso - Historias de Usuario

## Proceso completo para crear HU correctas

### 📋 PASO 1: Identificar Requerimientos del Enunciado

**¿Cómo identifico los requerimientos?**
- Lee el enunciado completo identificando **acciones concretas** que se mencionan
- Busca frases como: "debe poder", "se requiere", "el sistema permite", "es necesario"
- Identifica **procesos de negocio** (no validaciones técnicas)

**Ejemplo del alquiler de mobiliario:**
- "dar de alta los diferentes mobiliarios" → Requerimiento
- "realizar una reserva de alquiler" → Requerimiento  
- "pago con tarjeta de crédito" → Requerimiento

### 👥 PASO 2: Identificar Roles de Usuario

**¿Cómo identifico los roles?**
- Busca **quién realiza cada acción** en el enunciado
- Ignora sistemas externos (bancos, AFIP) - no son roles de usuario
- Un rol = persona que interactúa con el sistema

**Preguntas clave:**
- ¿Quién ejecuta esta funcionalidad?
- ¿Qué tipos de usuarios se mencionan?
- ¿Hay diferentes niveles de permisos/acceso?

**Ejemplo:**
- "encargado del departamento de mobiliario" → Rol: **Encargado de mobiliario**
- "usuarios puedan realizar una reserva" → Rol: **Cliente**

### ⚙️ PASO 3: Identificar Funcionalidades

**¿Cómo identifico las funcionalidades?**
- Una funcionalidad = UN proceso completo del sistema
- Debe responder: ¿Qué hace el sistema para el usuario?
- Una HU = Una funcionalidad

**Criterio clave:** Si puedo explicar la funcionalidad en una oración simple, es una HU

**Ejemplo:**
- ✅ "Dar de alta mobiliario" → Una funcionalidad completa
- ✅ "Realizar reserva de alquiler" → Una funcionalidad completa
- ❌ "Validar datos de entrada" → No es una funcionalidad, es validación técnica

### 📝 PASO 4: Crear las Historias de Usuario

**Para cada funcionalidad identificada:**

#### 4.1 **ID:** 
- Verbo + sustantivo que resuma la acción
- Ejemplo: "Dar alta mobiliario", "Realizar reserva"

#### 4.2 **TÍTULO:** 
- Formato estricto: "Como [rol] quiero [acción] para [beneficio]"
- **Siempre en primera persona**
- El beneficio debe responder "¿para qué lo necesito?"

**Ejemplo correcto:**
```
Como encargado de mobiliario quiero dar de alta un mueble para incluirlo en el inventario disponible.
```

#### 4.3 **REGLAS DE NEGOCIO:**
**¿Cuándo es una regla de negocio?**

✅ **ES regla de negocio si:**
- Está escrita textualmente en el enunciado
- Define cómo debe operar el negocio
- Es una restricción/política empresarial
- Afecta el comportamiento del sistema

❌ **NO es regla de negocio si:**
- Es una validación técnica (formato, campos requeridos)
- Lo estás interpretando/deduciendo
- Es del sentido común de programación

**Ejemplos:**
- ✅ "No pueden existir códigos repetidos" (escrito en enunciado)
- ✅ "Una reserva debe incluir mínimo 3 muebles" (política comercial escrita)
- ❌ "El código debe ser alfanumérico" (validación técnica no mencionada)

#### 4.4 **CRITERIOS DE ACEPTACIÓN:**

**¿Cuándo es un criterio de aceptación?**

✅ **ES criterio de aceptación si:**
- Define comportamientos específicos del sistema
- Son casos de prueba funcionales
- Derivan de reglas de negocio o del enunciado
- Siguen formato Given-When-Then

**Escenarios que SIEMPRE debes incluir:**

1. **Escenario exitoso:** El camino feliz, cuando todo funciona
2. **Escenarios de fallo por reglas de negocio:** Cada regla violada = un escenario
3. **Escenarios derivados del enunciado:** Situaciones específicas mencionadas

**❌ NO incluir como escenarios:**
- Validaciones técnicas básicas
- Casos que no estén implícitos en el enunciado
- Sobre-ingeniería de casos edge

### 🔍 PASO 5: Escribir Escenarios (Given-When-Then)

**Estructura obligatoria:**

```
Escenario X: [Título descriptivo]
Dado [contexto inicial específico],
Cuando [acción concreta del usuario],
Entonces [resultado esperado del sistema].
```

**Reglas para escribir escenarios:**

1. **Dado:** Contexto específico con datos concretos
   - ❌ "Dado que los datos son válidos"
   - ✅ "Dado que el código 'MOB001' no existe y el encargado está autenticado"

2. **Cuando:** Acción clara y específica
   - ❌ "Cuando completa el formulario"
   - ✅ "Cuando ingresa código 'MOB001', tipo 'Silla', precio '$50' y presiona 'Dar de alta'"

3. **Entonces:** Resultado observable del sistema
   - ❌ "Entonces funciona correctamente"
   - ✅ "Entonces el sistema registra el mueble y confirma 'Mobiliario registrado exitosamente'"

### ✅ PASO 6: Verificación Final

**Checklist para cada HU:**

- [ ] **Responde las 3 preguntas:**
  - ¿Quién se beneficia? (rol claro)
  - ¿Qué se quiere? (acción específica)
  - ¿Cuál es el beneficio? (propósito claro)

- [ ] **Título en primera persona** ("quiero", "deseo", "necesito")

- [ ] **Reglas de negocio solo del enunciado** (literales, no interpretadas)

- [ ] **Al menos 3 escenarios:**
  - Uno exitoso
  - Al menos uno de fallo por regla de negocio
  - Casos adicionales del enunciado

- [ ] **Given-When-Then con datos específicos**

- [ ] **Una HU = Una funcionalidad completa**

---

## 🚨 Errores Comunes a Evitar

1. **Incluir validaciones técnicas como reglas de negocio**
2. **Crear escenarios para validaciones de formato**
3. **Interpretar/agregar información no escrita en el enunciado**
4. **Títulos en tercera persona**
5. **Escenarios vagos sin datos concretos**
6. **Mezclar múltiples funcionalidades en una HU**

---

## 📖 Ejemplo Completo Aplicando los Pasos

### Enunciado: "El encargado debe dar de alta mobiliario. No pueden existir códigos repetidos."

**PASO 1:** Requerimiento → "dar de alta mobiliario"
**PASO 2:** Rol → "encargado"  
**PASO 3:** Funcionalidad → "Dar alta mobiliario"
**PASO 4-6:** HU completa

```
ID: Dar alta mobiliario
TÍTULO: Como encargado de mobiliario quiero dar de alta un mueble para incluirlo en el inventario disponible.
REGLAS DE NEGOCIO:
- No pueden existir códigos repetidos

CRITERIOS DE ACEPTACIÓN:
Escenario 1: Alta exitosa
Dado que el código "MOB001" no existe,
Cuando ingresa código "MOB001", tipo "Silla" y confirma,
Entonces el sistema registra el mueble.

Escenario 2: Alta fallida por código repetido  
Dado que el código "MOB001" ya existe,
Cuando intenta dar de alta con código "MOB001",
Entonces el sistema rechaza por código duplicado.
```

Esta metodología te asegura historias de usuario que cumplan exactamente con los criterios académicos de tu materia.