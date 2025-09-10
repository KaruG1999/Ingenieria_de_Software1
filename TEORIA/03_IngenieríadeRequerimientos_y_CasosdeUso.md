# Ingeniería de Software I - Casos de Uso
## Apunte Teórico

## Tipos de Requerimientos

### Requerimientos Funcionales
- **Describen** una interacción entre el sistema y su ambiente
- **Especifican** cómo debe comportarse el sistema ante determinado estímulo
- **Detallan** lo que el sistema debe hacer (o cómo NO debe comportarse)
- **Características:**
  - Independientes de la implementación
  - Se pueden expresar de distintas formas
  - Describen la funcionalidad del sistema

### Requerimientos No Funcionales
Describen restricciones sobre el sistema que limitan las opciones en la construcción de la solución.

#### Clasificación:

**1. Requerimientos del Producto**
- **Usabilidad**: estética, documentación de usuario, facilidad de uso
- **Rendimiento**: uso de recursos, tiempos de respuesta, eficiencia
- **Fiabilidad**: disponibilidad, facilidad de recuperación
- Espacio, portabilidad
- Consistencia de interfaz
- Ayuda en línea, documentación

**2. Requerimientos Organizacionales**
- Políticas y procedimientos de la organización
- Entrega, implementación, estándares

**3. Requerimientos Externos**
- Interoperabilidad, aspectos legales
- Privacidad, seguridad, éticos

## Ingeniería de Requerimientos

### Definición
La ingeniería de requerimientos es la **disciplina** para desarrollar una especificación completa, consistente y no ambigua, que servirá como base para acuerdos comunes entre todas las partes involucradas.

### Proceso
- **Transforma** requerimientos declarados por clientes (hablados/escritos)
- **Genera** especificaciones precisas, no ambiguas, consistentes y completas
- **Incluye** funciones, interfaces, rendimiento y limitaciones

### Importancia
- ✅ Gestiona necesidades del proyecto estructuradamente
- ✅ Mejora predicción de cronogramas
- ✅ Disminuye costos y retrasos
- ✅ Mejora calidad del software
- ✅ Mejora comunicación entre equipos
- ✅ Evita rechazos de usuarios finales

### Proceso Iterativo
En la práctica, es un **proceso iterativo** donde las actividades se entrelazan:
1. Definición de requerimientos
2. Diseño del sistema y software
3. Implementación y prueba de unidad
4. Integración y prueba del sistema
5. Operación y mantenimiento

## Estudio de Viabilidad

### Propósito
Principalmente para **sistemas nuevos**. A partir de una descripción resumida, se elabora un informe que recomienda la conveniencia o no del desarrollo.

### Preguntas Clave
- ¿El sistema contribuye a los objetivos generales de la organización?
- ¿Se puede implementar con la tecnología actual?
- ¿Se puede implementar con las restricciones de costo y tiempo?
- ¿Se puede integrar a otros sistemas existentes?

## Validación de Requerimientos

### Definición
La **validación de requerimientos** es el proceso de certificar la corrección del modelo de requerimientos contra las intenciones del usuario. Su **objetivo** es comprobar que los requerimientos reflejan correctamente lo que el usuario necesita.

### Conceptos Fundamentales (IEEE)
- **Validación:** Hacer el software correcto *(evaluación al final del desarrollo)*
- **Verificación:** Hacer el software correctamente *(cumplimiento correcto de requerimientos)*

### Aspectos a Verificar

#### Tipos de Verificaciones:
- **Validez**: Los requerimientos son los que el usuario realmente necesita. Para todos los usuarios
- **Consistencia**: No hay contradicciones entre requerimientos. Sin contradicciones
- **Completitud**: No faltan requerimientos importantes. Todos los requerimientos incluidos
- **Realismo**: Los requerimientos pueden implementarse con la tecnología, tiempo y costo disponibles. Se pueden implementar
- **Verificabilidad**: Se pueden diseñar pruebas que verifiquen los requerimientos. Se puede diseñar conjunto de pruebas

### Importancia
- Los errores en requerimientos pueden generar **grandes costos** si se descubren tarde
- La validación requiere **participación activa del usuario** (imprescindible para la validación)
- Validar en la fase de especificación evita correcciones costosas
- **Nota importante**: No es posible probar formalmente que un modelo de requerimientos sea correcto; sólo se puede obtener un alto grado de confianza

### Técnicas de Validación
**Manuales o Automatizadas:**
- **Revisiones de requerimientos**
  - *Informales:* Se discuten requerimientos con tantos stakeholders como sea posible
  - *Formales:* El equipo de desarrollo guía al cliente explicando implicancias y alcances
- **Construcción de prototipos**
- **Generación de casos de prueba**

## Definiciones Fundamentales de Casos de Uso

### ¿Qué son los Casos de Uso?
Los **Casos de Uso** representan un proceso de modelado del problema en términos de los eventos que interactúan entre los usuarios y el sistema. Es una técnica fundamental en el desarrollo centrado en el usuario.

### Desarrollo Centrado en el Usuario
El **desarrollo centrado en el usuario** es un enfoque de diseño y desarrollo de software que pone las necesidades, comportamientos y experiencias del usuario final en el centro del proceso de desarrollo. Se enfoca en entender cómo los usuarios interactúan con el sistema para crear soluciones que satisfagan sus necesidades reales.

### Origen y Aplicación
- Origen: Modelado orientado a objetos (Jacobson 1992)
- Aplicable a **cualquier metodología** de desarrollo
- Facilita y alienta la **participación de usuarios**

## Elementos Principales

### Actor
- **Definición**: Toda entidad que interactúa directamente con el sistema
- **Características**: 
  - Puede ser una persona, otro sistema o una entidad externa
  - Se representa con un ícono de figura humana en el diagrama
  - No forma parte del sistema, sino que interactúa con él
  - **Inicia** una actividad (CU) en el sistema
  - Representa un **papel/rol** desempeñado por un usuario
  - Puede ser: persona, sistema externo, dispositivo externo

### Caso de Uso
- **Definición**: Representa una funcionalidad en términos de la interacción del usuario
- **Características**:
  - Se representa con una elipse
  - El nombre debe ser breve y descriptivo (comenzar con un verbo)
  - Describe una funcionalidad específica del sistema
  - Representa un **objetivo individual** del sistema
  - Describe secuencia de actividades e interacciones
  - Debe estar acompañado de su respectivo escenario

### Diagrama de Casos de Uso
- **Definición**: Ilustra las relaciones entre los Casos de Uso y los actores
- **Propósito**: Proporcionar una vista general de las funcionalidades del sistema y sus interacciones

### Escenarios
- **Definición**: Descripción detallada de cada Caso de Uso para llevar a cabo la funcionalidad
- **Propósito**: Especificar paso a paso cómo se ejecuta cada caso de uso
- **Descripción de la interacción**: Entre actor y sistema para realizar la funcionalidad

## Proceso de Modelado

### Pasos del Proceso:
1. **Identificar los actores**
   - Buscar todas las entidades que interactúan con el sistema
   - Considerar personas, sistemas externos, dispositivos

2. **Identificar los casos de uso**
   - Determinar las funcionalidades que debe proveer el sistema
   - Nombrarlos con verbos descriptivos

3. **Construir el diagrama**
   - Relacionar actores con casos de uso
   - Establecer relaciones entre casos de uso

4. **Realizar los escenarios**
   - Describir detalladamente cada caso de uso

### Identificación de Actores - Preguntas Clave:
- ¿Quién proporciona entradas al sistema?
- ¿Quién recibe salidas del sistema?
- ¿Se requieren interfaces con otros sistemas?
- ¿Quién mantendrá la información?

### Identificación de CU - Preguntas Clave:
- ¿Cuáles son las tareas principales del actor?
- ¿Qué información necesita/proporciona el actor?
- ¿Necesita el sistema/actor informar eventos o cambios?

## Relaciones en el Diagrama

### Relación de Asociación
- **Descripción**: Conexión simple entre actor y caso de uso. Relación básica entre un actor y un CU donde existe interacción
- **Representación**: Línea continua
- **Uso**: Cuando un actor participa en un caso de uso

### Relación de Extensión (<<extend>>)
- **Descripción**: Un caso de uso extiende a otro bajo ciertas condiciones. Modela un **comportamiento opcional o alternativo** que amplía la funcionalidad de un CU base en casos especiales
- **Representación**: Flecha punteada con etiqueta <<extend>>
- **Uso**: Para funcionalidades opcionales o condicionales

### Relación de Inclusión (<<include>> o <<uses>>)
- **Descripción**: Un caso de uso incluye obligatoriamente a otro. Se utiliza para **reducir redundancia**, agrupando pasos comunes de varios CU en uno reutilizable
- **Representación**: Flecha punteada con etiqueta <<include>>
- **Uso**: Para funcionalidades comunes reutilizables

### Relación de Herencia
- **Descripción**: Especialización entre actores o casos de uso. Permite abstraer un comportamiento común en un actor "padre" que es heredado por actores "hijo"
- **Representación**: Flecha continua con punta triangular
- **Uso**: Para mostrar jerarquías

## Estructura del Escenario

### Elementos Obligatorios:

**Nombre del caso de uso**: Nombre breve y descriptivo (comenzar con un verbo)

**Descripción**: Comentario general del propósito del CU

**Actores**: Una o más entidades, como figuran en el diagrama

**Precondiciones**: Restricción del estado del sistema antes de ejecutar el caso de uso. Condición necesaria que se asume como verdadera antes de comenzar a ejecutar el CU. En general, es la postcondición de otro CU. Ejemplo: que otro CU se haya ejecutado previamente.

**Curso Normal**: 
- **Curso normal**: Secuencia típica de pasos realizados por el actor y el sistema sin errores ni excepciones
- Secuencia de pasos numerada que reflejan la interacción entre el actor y el sistema
- Se divide en dos columnas:
  - Acciones del Actor
  - Acciones del Sistema

**Curso Alterno**: **Curso alterno**: Variaciones o excepciones que pueden ocurrir durante el curso normal. Describen cómo el sistema y los actores responden a dichas situaciones. Pasos alternativos al curso normal. Pueden ser del actor o del sistema. Siempre se debe especificar si el CU termina o retoma a un paso del curso normal

**Postcondición**: **Poscondición**: Restricción del estado del sistema después de la finalización exitosa del caso de uso. Condición relacionada con el sistema que se da por verdadera luego de ejecutado el curso normal. Ejemplo: datos guardados en BD, recibo emitido.

## Características Importantes

- **Funcionalidad concreta:** Cada CU debe representar una funcionalidad específica
- **Interacción:** Descripción debe contener más de un paso
- **Curso normal:** Uso limitado de condicionales (solo para excepciones)
- **Pre-condiciones:** No representar en cursos alternativos
- **"Uses":** Deben ser accedidos por al menos dos CU

## Beneficios de Modelar con Casos de Uso

### Beneficios Principales:
- ✅ Herramienta para capturar requerimientos funcionales
- ✅ Descompone el alcance en piezas manejables
- ✅ Medio de comunicación con usuarios
- ✅ Lenguaje común y fácil de entender
- ✅ Permite estimar alcance y esfuerzo
- ✅ Define línea base para planes de prueba
- ✅ Proporciona seguimiento de requisitos

### Beneficios Adicionales:
1. **Comunicación mejorada**: Facilita la comunicación entre desarrolladores, analistas y usuarios finales
2. **Enfoque en el usuario**: Mantiene el foco en las necesidades del usuario
3. **Organización clara**: Estructura las funcionalidades del sistema de manera comprensible
4. **Base para pruebas**: Los escenarios sirven como base para crear casos de prueba
5. **Documentación**: Proporciona documentación clara de los requerimientos
6. **Planificación**: Ayuda en la estimación de esfuerzos y planificación del proyecto
7. **Validación**: Permite validar requerimientos con los stakeholders
8. **Trazabilidad**: Facilita el seguimiento desde requerimientos hasta implementación

## Consejos para Escribir Buenos Casos de Uso

1. **Nombrar con verbos**: Los casos de uso deben comenzar con un verbo (Ej: "Registrar usuario", "Procesar pago")
2. **Ser específicos**: Evitar ambigüedades en las descripciones
3. **Mantener granularidad adecuada**: No muy generales ni muy específicos
4. **Incluir cursos alternos**: Considerar escenarios de error y excepciones
5. **Usar lenguaje del dominio**: Emplear términos que entienda el cliente
6. **Ser consistentes**: Mantener el mismo nivel de detalle en todos los casos de uso

## Ejemplos Prácticos de Aplicación

### Recordatorio de Ejemplos Vistos en Práctica

**Actor "usuario" en Sokoban**: puede iniciar/terminar partida, mover jugador, reiniciar nivel.

**Actor "sistema"**: cambia de nivel y carga niveles automáticamente.

Estos ejemplos demuestran cómo los actores pueden incluir tanto entidades humanas como sistemas automatizados que interactúan con el software principal.

### Ejemplo Práctico: Sistema de Artículos Periodísticos

#### Actores Identificados:
- Usuario Anónimo
- Usuario Registrado  
- Servidor Externo (Banco)

#### Casos de Uso Identificados:
- Leer Artículo
- Descargar Artículo
- Registrar Usuario
- Modificar Datos Personales
- Iniciar Sesión
- Cerrar Sesión
- Verificar Tarjeta

#### Ejemplo de Escenario: "Iniciar Sesión"

**Nombre**: Iniciar sesión
**Descripción**: Usuario registrado inicia sesión con usuario y contraseña
**Actores**: Usuario Registrado
**Precondiciones**: ---

**Curso Normal**:
| Acciones del Actor | Acciones del Sistema |
|-------------------|---------------------|
| Paso 1: Selecciona opción iniciar sesión | Paso 2: Presenta pantalla login |
| Paso 3: Ingresa usuario y contraseña | Paso 4: Verifica credenciales |
| | Paso 5: Inicia sesión y muestra menú |

**Curso Alterno**: Paso 4 alternativo - Credenciales inválidas, notifica error, vuelve al paso 2

**Postcondición**: Sesión iniciada exitosamente, opciones de usuario registrado habilitadas