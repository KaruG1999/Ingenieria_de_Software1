# Práctica 1: Obtención de Requerimientos
## Ingeniería de Software I

---

## PARTE I - DEFINICIONES

### 1. ¿Qué es un requerimiento?
Un **requerimiento** es una condición o capacidad que necesita el usuario para resolver un problema o alcanzar un objetivo, o que debe satisfacer un sistema para cumplir un contrato, estándar o especificación. Es una característica del sistema que describe algo que el sistema debe ser capaz de hacer para satisfacer su propósito.

### 2. Requerimientos Funcionales y No Funcionales

#### Requerimientos Funcionales
Son las **funciones específicas** que debe realizar el sistema. Describen **QUÉ** debe hacer el sistema.
- **Ejemplos**: "El sistema debe permitir registrar asistencia", "El sistema debe generar reportes", "El sistema debe validar credenciales de usuario"

#### Requerimientos No Funcionales
Son las **características de calidad** del sistema. Describen **CÓMO** debe comportarse el sistema.
- **Ejemplos**: Rendimiento, seguridad, usabilidad, confiabilidad, escalabilidad
- "El sistema debe responder en menos de 2 segundos", "Debe estar disponible 99.9% del tiempo"

### 3. ¿Qué es un Stakeholder?
Un **stakeholder** es cualquier persona o grupo que se verá afectado por el sistema, directa o indirectamente. Incluye usuarios finales, ingenieros, gerentes, expertos del dominio, y cualquier entidad que tenga interés en el sistema.

### 4. Fuentes más importantes para obtención de información
1. **Documentación existente**: Manuales, procedimientos, bases de datos actuales
2. **Stakeholders**: A través de entrevistas, cuestionarios, observación
3. **Sistemas similares**: Especificaciones de sistemas que resuelven problemas parecidos
4. **Regulaciones y normativas**: Leyes, estándares del dominio
5. **Procesos actuales**: Observación del trabajo y flujos existentes

### 5. Puntos de Vista Genéricos
1. **Punto de vista de interactuadores**: Personas/sistemas que interactúan directamente con el sistema
2. **Punto de vista indirecto**: Stakeholders que no usan el sistema pero influyen en los requerimientos
3. **Punto de vista del dominio**: Características y restricciones del área de aplicación

### 6. Tres Problemas de Comunicación
1. **Dificultad para expresar claramente las necesidades** - Los usuarios no saben cómo articular lo que necesitan
2. **Cultura y vocabulario diferentes** - Diferencias terminológicas entre usuarios técnicos y no técnicos
3. **Conflictos personales o políticos** - Intereses contrapuestos entre diferentes grupos de usuarios

---

## PARTE II - PROBLEMAS

### Problema 1: Sistema de Registro de Asistencia Biométrica

#### **STAKEHOLDERS**
- **Usuarios directos**: Estudiantes, Jefe de Trabajos Prácticos, Profesor de la cátedra
- **Usuarios indirectos**: Oficina de alumnos, personal técnico de la facultad
- **Reguladores**: Autoridades de privacidad de datos de la facultad
- **Técnicos**: Administradores del sistema, personal de soporte IT

#### **PUNTOS DE VISTA**
- **Interactuadores**: 
  - Estudiantes (registran asistencia)
  - JTP (autoriza registro)
  - Profesor (consulta estados)
- **Indirectos**: 
  - Oficina de alumnos (provee listados)
  - Autoridades académicas (supervisión)
- **Dominio**: 
  - Reglamentación de privacidad
  - Políticas académicas de la facultad

#### **FUENTES DE INFORMACIÓN**
- **Documentación**: Reglamentos de asistencia, normativas de privacidad, listados actuales de alumnos
- **Stakeholders**: Entrevistas con profesores, JTP, estudiantes, personal administrativo
- **Sistemas existentes**: Otros sistemas de control de asistencia en la facultad
- **Observación**: Proceso actual de toma de asistencia

---

### Problema 2: Sistema de Gestión de Clínica Alérgica

#### **STAKEHOLDERS**
- **Usuarios directos**: Empleados administrativos, enfermeros, doctores, director de clínica
- **Usuarios indirectos**: Pacientes, familiares de pacientes
- **Reguladores**: Ministerio de Salud de Bs As, organismos de control sanitario
- **Técnicos**: Personal IT, administradores del sistema

#### **PUNTOS DE VISTA**
- **Interactuadores**: 
  - Empleados (registro de datos)
  - Enfermeros (controles y anotaciones)
  - Doctores (tratamientos e historias clínicas)
  - Director (consulta de historias)
- **Indirectos**: 
  - Pacientes (privacidad y acceso a sus datos)
  - Familiares (información sobre tratamientos)
- **Dominio**: 
  - Normativas del Ministerio de Salud
  - Protocolos médicos de alergias
  - Regulaciones de privacidad médica

#### **FUENTES DE INFORMACIÓN**
- **Documentación**: Normativas sanitarias, protocolos médicos actuales, formularios existentes
- **Stakeholders**: Entrevistas con personal médico, administrativo y directivo
- **Sistemas existentes**: Otros sistemas de gestión hospitalaria
- **Observación**: Flujo actual de atención de pacientes

---

## PARTE II-B: Conflictos entre Stakeholders

### ¿Por qué los requerimientos de distintos stakeholders podrían entrar en conflicto?

#### **En el Sistema de Asistencia Biométrica:**
1. **Privacidad vs Funcionalidad**: 
   - Estudiantes pueden preferir anonimato vs necesidad institucional de control
2. **Flexibilidad vs Control**: 
   - Profesores quieren flexibilidad en horarios vs JTP necesita control estricto
3. **Usabilidad vs Seguridad**: 
   - Usuarios quieren proceso rápido vs requerimientos de seguridad biométrica

#### **En el Sistema de Clínica:**
1. **Eficiencia vs Detalle**: 
   - Personal administrativo quiere procesos rápidos vs doctores necesitan información detallada
2. **Accesibilidad vs Privacidad**: 
   - Director quiere acceso completo vs pacientes quieren privacidad restringida
3. **Funcionalidad vs Costo**: 
   - Personal médico quiere todas las funcionalidades vs dirección quiere controlar costos

#### **Causas Generales de Conflictos:**
- **Diferentes prioridades**: Cada stakeholder valora aspectos distintos
- **Limitaciones de recursos**: No se pueden satisfacer todos los deseos
- **Perspectivas de rol**: Cada usuario ve el sistema desde su función específica
- **Intereses organizacionales**: Diferentes departamentos pueden tener objetivos contrapuestos
- **Experiencia técnica variable**: Diferentes niveles de comprensión tecnológica

#### **Estrategias para Resolver Conflictos:**
1. **Priorización**: Determinar qué requerimientos son críticos vs deseables
2. **Negociación**: Facilitar acuerdos entre stakeholders conflictivos
3. **Análisis de impacto**: Evaluar consecuencias de cada decisión
4. **Documentación clara**: Registrar decisiones y justificaciones
5. **Validación iterativa**: Verificar acuerdos con prototipos o demos