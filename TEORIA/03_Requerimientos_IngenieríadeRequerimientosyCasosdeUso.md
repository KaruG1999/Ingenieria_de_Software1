# Ingeniería de Software I - Clase 3
## Requerimientos, Ingeniería de Requerimientos y Casos de Uso

---

## 1. Tipos de Requerimientos

### 1.1 Requerimientos Funcionales
- **Describen** una interacción entre el sistema y su ambiente
- **Especifican** cómo debe comportarse el sistema ante determinado estímulo
- **Detallan** lo que el sistema debe hacer (o cómo NO debe comportarse)
- **Características:**
  - Independientes de la implementación
  - Se pueden expresar de distintas formas
  - Describen la funcionalidad del sistema

### 1.2 Requerimientos No Funcionales
Describen restricciones sobre el sistema que limitan las opciones en la construcción de la solución.

#### Clasificación:

**1. Requerimientos del Producto**
- Usabilidad, eficiencia, rendimiento
- Espacio, fiabilidad, portabilidad
- Estética, consistencia de interfaz
- Ayuda en línea, documentación

**2. Requerimientos Organizacionales**
- Políticas y procedimientos de la organización
- Entrega, implementación, estándares

**3. Requerimientos Externos**
- Interoperabilidad, aspectos legales
- Privacidad, seguridad, éticos

---

## 2. Ingeniería de Requerimientos

### 2.1 Definición
> La ingeniería de requerimientos es la **disciplina** para desarrollar una especificación completa, consistente y no ambigua, que servirá como base para acuerdos comunes entre todas las partes involucradas.

### 2.2 Proceso
- **Transforma** requerimientos declarados por clientes (hablados/escritos)
- **Genera** especificaciones precisas, no ambiguas, consistentes y completas
- **Incluye** funciones, interfaces, rendimiento y limitaciones

### 2.3 Importancia
- ✅ Gestiona necesidades del proyecto estructuradamente
- ✅ Mejora predicción de cronogramas
- ✅ Disminuye costos y retrasos
- ✅ Mejora calidad del software
- ✅ Mejora comunicación entre equipos
- ✅ Evita rechazos de usuarios finales

### 2.4 Proceso Iterativo
En la práctica, es un **proceso iterativo** donde las actividades se entrelazan:
1. Definición de requerimientos
2. Diseño del sistema y software
3. Implementación y prueba de unidad
4. Integración y prueba del sistema
5. Operación y mantenimiento

---

## 3. Estudio de Viabilidad

### 3.1 Propósito
Principalmente para **sistemas nuevos**. A partir de una descripción resumida, se elabora un informe que recomienda la conveniencia o no del desarrollo.

### 3.2 Preguntas Clave
- ¿El sistema contribuye a los objetivos generales de la organización?
- ¿Se puede implementar con la tecnología actual?
- ¿Se puede implementar con las restricciones de costo y tiempo?
- ¿Se puede integrar a otros sistemas existentes?

---

## 4. Validación de Requerimientos

### 4.1 Definición
**Proceso** de certificar la corrección del modelo de requerimientos contra las intenciones del usuario.

### 4.2 Conceptos Clave (IEEE)
- **Validación:** Hacer el software correcto *(evaluación al final del desarrollo)*
- **Verificación:** Hacer el software correctamente *(cumplimiento correcto de requerimientos)*

### 4.3 Importancia
- Los errores en requerimientos pueden generar **grandes costos** si se descubren tarde
- La validación requiere **participación activa del usuario**
- Validar en la fase de especificación evita correcciones costosas

### 4.4 Tipos de Verificaciones
- **Validez:** Para todos los usuarios
- **Consistencia:** Sin contradicciones
- **Completitud:** Todos los requerimientos incluidos
- **Realismo:** Se pueden implementar
- **Verificabilidad:** Se puede diseñar conjunto de pruebas

### 4.5 Técnicas de Validación
**Manuales o Automatizadas:**
- **Revisiones de requerimientos**
  - *Informales:* Con tantos stakeholders como sea posible
  - *Formales:* Equipo conduce al cliente explicando implicaciones
- **Construcción de prototipos**
- **Generación de casos de prueba**

---

## 5. Casos de Uso

### 5.1 Definición
**Proceso** de modelado de las funcionalidades del sistema en términos de eventos que interactúan entre usuarios y el sistema.

### 5.2 Origen y Aplicación
- Origen: Modelado orientado a objetos (Jacobson 1992)
- Aplicable a **cualquier metodología** de desarrollo
- Facilita y alienta la **participación de usuarios**

### 5.3 Beneficios
- ✅ Herramienta para capturar requerimientos funcionales
- ✅ Descompone el alcance en piezas manejables
- ✅ Medio de comunicación con usuarios
- ✅ Lenguaje común y fácil de entender
- ✅ Permite estimar alcance y esfuerzo
- ✅ Define línea base para planes de prueba
- ✅ Proporciona seguimiento de requisitos

### 5.4 Componentes

#### Diagrama de Casos de Uso
Ilustra las interacciones entre el sistema y los actores.

#### Escenarios (Narración del CU)
Descripción de la interacción entre actor y sistema para realizar la funcionalidad.

### 5.5 Elementos del Diagrama

#### Caso de Uso
- Representa un **objetivo individual** del sistema
- Describe secuencia de actividades e interacciones
- Debe estar acompañado de su respectivo escenario

#### Actores
- **Inicia** una actividad (CU) en el sistema
- Representa un **papel/rol** desempeñado por un usuario
- Puede ser: persona, sistema externo, dispositivo externo

#### Relaciones
1. **Asociaciones:** Entre actor y CU que interactúan
2. **Extensiones (Extends):** Un CU extiende funcionalidad de otro
3. **Uso/Inclusión (Uses):** Reduce redundancia combinando pasos comunes
4. **Herencia:** Actor hereda funcionalidades de otro(s) actor(es)

### 5.6 Estructura del Escenario

```
Nombre del caso de uso: [Verbo + objetivo]
Descripción: [Propósito corto y preciso]
Actores: [Actor principal que se beneficia]
Precondiciones: [Estado del sistema antes de ejecución]

Curso Normal:
  Acción del Actor          |  Acciones del Sistema
  Paso 1: ...              |  Paso 2: ...
  Paso 3: ...              |  Paso 4: ...

Curso Alterno: [Excepciones o variaciones del curso típico]
Postcondición: [Estado del sistema después de finalización exitosa]
```

### 5.7 Proceso de Modelado

#### Pasos:
1. **Identificar actores**
2. **Identificar casos de uso**
3. **Construir diagrama**
4. **Realizar escenarios**

#### Identificación de Actores - Preguntas Clave:
- ¿Quién proporciona entradas al sistema?
- ¿Quién recibe salidas del sistema?
- ¿Se requieren interfaces con otros sistemas?
- ¿Quién mantendrá la información?

#### Identificación de CU - Preguntas Clave:
- ¿Cuáles son las tareas principales del actor?
- ¿Qué información necesita/proporciona el actor?
- ¿Necesita el sistema/actor informar eventos o cambios?

### 5.8 Características Importantes

- **Funcionalidad concreta:** Cada CU debe representar una funcionalidad específica
- **Interacción:** Descripción debe contener más de un paso
- **Curso normal:** Uso limitado de condicionales (solo para excepciones)
- **Pre-condiciones:** No representar en cursos alternativos
- **"Uses":** Deben ser accedidos por al menos dos CU

---

## Ejemplo Práctico

### Sistema: Sitio Web de Artículos Periodísticos

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

```
Nombre: Iniciar sesión
Descripción: Usuario registrado inicia sesión con usuario y contraseña
Actores: Usuario Registrado
Precondiciones: ---

Curso Normal:
  Actor                                    |  Sistema
  Paso 1: Selecciona opción iniciar sesión |  Paso 2: Presenta pantalla login
  Paso 3: Ingresa usuario y contraseña     |  Paso 4: Verifica credenciales
                                          |  Paso 5: Inicia sesión y muestra menú

Curso Alterno: Paso 4 alternativo - Credenciales inválidas, notifica error, vuelve al paso 2
Postcondición: Sesión iniciada exitosamente, opciones de usuario registrado habilitadas
```

---

## Referencias
- Sommerville Ian, Capítulos 4, Ingeniería de software, Addison Wesley 2011
- Whitten y Bentley, Análisis de Sistemas Diseño y Métodos, Capítulo 6, Mc Graw Hill 2008