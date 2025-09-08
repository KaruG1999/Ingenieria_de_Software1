# Ingeniería de Software I - Casos de Uso
## Apunte Teórico

### Definiciones Fundamentales

#### ¿Qué son los Casos de Uso?
Los **Casos de Uso** representan un proceso de modelado del problema en términos de los eventos que interactúan entre los usuarios y el sistema. Es una técnica fundamental en el desarrollo centrado en el usuario.

#### Desarrollo Centrado en el Usuario
El **desarrollo centrado en el usuario** es un enfoque de diseño y desarrollo de software que pone las necesidades, comportamientos y experiencias del usuario final en el centro del proceso de desarrollo. Se enfoca en entender cómo los usuarios interactúan con el sistema para crear soluciones que satisfagan sus necesidades reales.

### Elementos Principales

#### Actor
- **Definición**: Toda entidad que interactúa directamente con el sistema
- **Características**: 
  - Puede ser una persona, otro sistema o una entidad externa
  - Se representa con un ícono de figura humana en el diagrama
  - No forma parte del sistema, sino que interactúa con él

#### Caso de Uso
- **Definición**: Representa una funcionalidad en términos de la interacción del usuario
- **Características**:
  - Se representa con una elipse
  - El nombre debe ser breve y descriptivo (comenzar con un verbo)
  - Describe una funcionalidad específica del sistema

#### Diagrama de Casos de Uso
- **Definición**: Ilustra las relaciones entre los Casos de Uso y los actores
- **Propósito**: Proporcionar una vista general de las funcionalidades del sistema y sus interacciones

#### Escenarios
- **Definición**: Descripción detallada de cada Caso de Uso para llevar a cabo la funcionalidad
- **Propósito**: Especificar paso a paso cómo se ejecuta cada caso de uso

### Proceso de Modelado

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

### Relaciones en el Diagrama

#### Relación de Asociación
- **Descripción**: Conexión simple entre actor y caso de uso
- **Representación**: Línea continua
- **Uso**: Cuando un actor participa en un caso de uso

#### Relación de Extensión (<<extend>>)
- **Descripción**: Un caso de uso extiende a otro bajo ciertas condiciones
- **Representación**: Flecha punteada con etiqueta <<extend>>
- **Uso**: Para funcionalidades opcionales o condicionales

#### Relación de Inclusión (<<include>> o <<uses>>)
- **Descripción**: Un caso de uso incluye obligatoriamente a otro
- **Representación**: Flecha punteada con etiqueta <<include>>
- **Uso**: Para funcionalidades comunes reutilizables

#### Relación de Herencia
- **Descripción**: Especialización entre actores o casos de uso
- **Representación**: Flecha continua con punta triangular
- **Uso**: Para mostrar jerarquías

### Estructura del Escenario

#### Elementos Obligatorios:

**Nombre del caso de uso**: Nombre breve y descriptivo (comenzar con un verbo)

**Descripción**: Comentario general del propósito del CU

**Actores**: Una o más entidades, como figuran en el diagrama

**Precondiciones**: Condición necesaria que se asume como verdadera antes de comenzar a ejecutar el CU. En general, es la postcondición de otro CU

**Curso Normal**: 
- Secuencia de pasos numerada que reflejan la interacción entre el actor y el sistema
- Se divide en dos columnas:
  - Acciones del Actor
  - Acciones del Sistema

**Curso Alterno**: Pasos alternativos al curso normal. Pueden ser del actor o del sistema. Siempre se debe especificar si el CU termina o retoma a un paso del curso normal

**Postcondición**: Condición relacionada con el sistema que se da por verdadera luego de ejecutado el curso normal

### Beneficios de Modelar con Casos de Uso

1. **Comunicación mejorada**: Facilita la comunicación entre desarrolladores, analistas y usuarios finales
2. **Enfoque en el usuario**: Mantiene el foco en las necesidades del usuario
3. **Organización clara**: Estructura las funcionalidades del sistema de manera comprensible
4. **Base para pruebas**: Los escenarios sirven como base para crear casos de prueba
5. **Documentación**: Proporciona documentación clara de los requerimientos
6. **Planificación**: Ayuda en la estimación de esfuerzos y planificación del proyecto
7. **Validación**: Permite validar requerimientos con los stakeholders
8. **Trazabilidad**: Facilita el seguimiento desde requerimientos hasta implementación

### Consejos para Escribir Buenos Casos de Uso

1. **Nombrar con verbos**: Los casos de uso deben comenzar con un verbo (Ej: "Registrar usuario", "Procesar pago")
2. **Ser específicos**: Evitar ambigüedades en las descripciones
3. **Mantener granularidad adecuada**: No muy generales ni muy específicos
4. **Incluir cursos alternos**: Considerar escenarios de error y excepciones
5. **Usar lenguaje del dominio**: Emplear términos que entienda el cliente
6. **Ser consistentes**: Mantener el mismo nivel de detalle en todos los casos de uso