# Historias de Usuario - Ingeniería de Software I

## ¿Qué es una Historia de Usuario?

Una **Historia de Usuario** es una descripción corta y simple de un requerimiento de un sistema, escrita en lenguaje común del usuario y desde su perspectiva.

### Características principales:
- Se utilizan en metodologías ágiles (XP, SCRUM)
- Sirven para especificar requisitos
- Están centradas en el usuario final

### Las 3 preguntas clave que debe responder:
1. **¿Quién se beneficia?** (rol del usuario)
2. **¿Qué se quiere?** (funcionalidad deseada)
3. **¿Cuál es el beneficio?** (valor que aporta)

## Estructura de una Historia de Usuario

### Anverso (Frente)

**ID:** Identificador único expresado como texto, generalmente de la forma `<verbo> <sustantivo>`

**TÍTULO:** Descripción en formato estándar:
```
Como <rol> quiero <algo> para <beneficio>
```

**REGLAS DE NEGOCIO:** Conjunto de reglas, normas y políticas que condicionan el modo de operación.

### Reverso (Dorso)

**CRITERIOS DE ACEPTACIÓN:** Criterios que determinan cuándo una historia cumple con las expectativas del cliente.

**Formato:**
```
Escenario N: título del criterio
Dado <un contexto inicial>,
Cuando <ocurre un evento>,
Entonces <garantiza uno o más resultados>
```

## Ejemplo Práctico: Sistema de Inscripción a Cursos

### Contexto del Sistema
Sistema web para inscripción a cursos de un Instituto donde:
- Las personas deben matricularse antes de inscribirse a cursos
- Se requieren datos personales (nombre, apellido, DNI, dirección)
- Cada DNI solo puede tener una matrícula
- Los cursos tienen cupo limitado (30 personas)
- Los pagos se realizan con tarjeta de crédito

### Roles identificados:
- **Persona:** No inscripta en el instituto
- **Matriculado:** Ya registrado en el instituto

## Historia de Usuario 1: Matricular Persona

### Anverso
- **ID:** Matricular persona
- **TÍTULO:** Como persona quiero matricularme al instituto para poder hacer los cursos
- **REGLAS DE NEGOCIO:** Un DNI no puede estar registrado dos veces con diferentes matrículas

### Reverso - Criterios de Aceptación

**Escenario 1: Matriculación exitosa**
- **Dado** que el DNI 22.222.222 no se encuentra matriculado y las condiciones son adecuadas para un pago exitoso
- **Cuando** la persona ingresa "Juan Perez", DNI 22.222.222, dirección 7 #123 y presiona "Matricularse"
- **Entonces** el sistema redirige al pago, procesa la matrícula y genera el número de matrícula

**Escenario 2: Matriculación fallida por matriculado existente**
- **Dado** que el DNI 12.123.123 ya está matriculado
- **Cuando** se intenta matricular con ese DNI
- **Entonces** el sistema informa que la persona ya está matriculada

**Escenario 3: Matriculación fallida por error en pago**
- **Dado** que el pago no puede procesarse correctamente
- **Cuando** se intenta matricular
- **Entonces** el sistema informa error de pago y no matricula

## Historia de Usuario 2: Inscribir Matriculado a Curso

### Anverso
- **ID:** Inscribir matriculado a curso
- **TÍTULO:** Como matriculado quiero inscribirme a un curso para adquirir más conocimiento
- **REGLAS DE NEGOCIO:** 
  - El curso tiene cupo de 30 inscriptos
  - Un matriculado solo se puede inscribir una vez a un mismo curso

### Reverso - Criterios de Aceptación

**Escenario 1: Inscripción exitosa**
- **Dado** que el matriculado no está inscripto al curso y hay cupo disponible
- **Cuando** selecciona el curso y presiona "Inscribirse"
- **Entonces** se procesa el pago, inscribe al matriculado y actualiza el cupo

**Escenario 2: Inscripción fallida por falta de cupo**
- **Dado** que el curso no tiene cupo disponible
- **Cuando** se intenta inscribir
- **Entonces** el sistema informa que no hay cupo

**Escenario 3: Ya inscripto en el curso**
- **Dado** que el matriculado ya está inscripto en ese curso
- **Cuando** intenta inscribirse nuevamente
- **Entonces** el sistema informa que ya está inscripto

## Historia de Usuario 3: Pagar con Tarjeta

### Anverso
- **ID:** Pagar con Tarjeta
- **TÍTULO:** Como persona o matriculado quiero pagar con tarjeta para matricularme o inscribirme a un curso
- **REGLAS DE NEGOCIO:** Solo se aceptan números correspondientes a tarjetas de crédito

### Reverso - Criterios de Aceptación

**Escenario 1: Pago exitoso**
- **Dado** que la tarjeta es válida y tiene saldo suficiente
- **Cuando** se ingresa el número y se presiona "Pagar"
- **Entonces** el sistema registra el pago exitosamente

**Escenario 2: Tarjeta inexistente**
- **Dado** que el número no corresponde a una tarjeta válida
- **Cuando** se intenta pagar
- **Entonces** el sistema retorna error por tarjeta inexistente

## Mejora del Sistema: Historia de Listar Cursos

### Historia de Usuario 4: Listar Cursos con Cupo

**ID:** Listar cursos con cupo
**TÍTULO:** Como matriculado quiero obtener un listado de cursos con cupo para poder seleccionar uno al momento de inscribirme

**Beneficio de esta historia:**
- Elimina el escenario de "falta de cupo" de la HU anterior
- Mejora la experiencia del usuario
- Solo muestra cursos disponibles y permite inscripción solo a cursos no tomados previamente

## Consejos para Redactar Buenas Historias de Usuario

1. **Mantener simplicidad:** Lenguaje claro y comprensible
2. **Enfoque en el valor:** Siempre especificar el beneficio
3. **Criterios medibles:** Los criterios de aceptación deben ser verificables
4. **Cobertura completa:** Incluir escenarios exitosos y de error
5. **Independencia:** Cada historia debe ser independiente de otras

## Formato Dado-Cuando-Entonces (Gherkin)

Este formato estructurado permite:
- **Dado:** Establece el contexto inicial
- **Cuando:** Define la acción que se ejecuta
- **Entonces:** Especifica el resultado esperado

Es un estándar que facilita la comunicación entre desarrolladores, testers y stakeholders, y permite automatizar pruebas de aceptación.