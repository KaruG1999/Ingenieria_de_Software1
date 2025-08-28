# Síntesis Clase 2 - Ingeniería de Software I
## Técnicas de Elicitación de Requerimientos y Historias de Usuario

---

## 🎯 **Técnicas de Elicitación (Continuación)**

### **Métodos Interactivos**

#### **1. Planeación Conjunta de Requerimientos (JRP)**
- **Definición**: Proceso de reuniones de grupo altamente estructuradas para analizar problemas y definir requerimientos
- También conocido como **JAD** (Joint Application Design)

**Participantes clave:**
- **Facilitador**: Dirige las sesiones, habilidades de comunicación y negociación
- **Secretarios**: Registran la sesión y publican resultados
- **Equipos de TI**: Escuchan y toman nota de requerimientos
- **Patrocinador**: Miembro directivo con autoridad, responsable del proyecto
- **Usuarios y Gerentes**: Comunican y aprueban requerimientos

**✅ Ventajas:**
- Ahorro de tiempo
- Usuarios involucrados activamente
- Desarrollos creativos

**❌ Desventajas:**
- Difícil organizar horarios de involucrados
- Complejo encontrar grupo integrado y organizado

#### **2. Lluvia de Ideas (Brainstorming)**
- **Objetivo**: Generar ideas alentando a participantes a ofrecer tantas ideas como sea posible en corto tiempo
- **Principio**: Cuantas más ideas se sugieren, mejores resultados se conseguirán

**Principios fundamentales:**
- Producción grupal más efectiva que individual
- Ideas por "contagio" entre participantes
- Mejores ideas aparecen tarde
- Mejor elegir sobre variedad de soluciones

**Fases de aplicación:**
1. Descubrir hechos
2. Producir ideas
3. Descubrir soluciones

---

## 📚 **Métodos Discretos de Elicitación**

**Características:**
- Menos perturbadores que otros métodos
- Insuficientes por sí solos
- Deben combinarse con métodos interactivos

### **1. Muestreo de Documentación**
**Documentos útiles:**
- Organigrama (propietarios, usuarios clave)
- Memos, notas internas, minutas
- Solicitudes de proyectos anteriores
- Documentos de funcionalidad del negocio
- Declaración de misión y plan estratégico
- Políticas, restricciones, procedimientos
- Bases de datos y sistemas en funcionamiento
- Manuales de operación y entrenamiento

### **2. Investigación y Visitas al Sitio**
- Investigar el dominio del problema
- Buscar patrones de soluciones similares
- Consultar revistas especializadas
- Buscar problemas similares en internet
- Consultar otras organizaciones

### **3. Observación del Ambiente de Trabajo**
**Lineamientos:**
- Determinar quién y cuándo observar
- Obtener permisos y explicar propósito
- Mantener bajo perfil
- Tomar notas detalladas
- No interrumpir el trabajo

**✅ Ventajas:**
- Datos confiables
- Ver exactamente qué se hace
- Análisis de disposiciones físicas
- Económica comparada con otras técnicas

**❌ Desventajas:**
- Incomodidad de personas observadas
- Horarios incómodos para algunas actividades
- Tareas sujetas a interrupciones
- Comportamiento "artificial" del observado

---

## 📋 **Especificación de Requerimientos de Software**

### **Objetivos:**
1. Permitir que desarrolladores expliquen cómo entendieron lo que cliente pretende
2. Indicar a diseñadores qué funcionalidad tendrá el sistema
3. Indicar al equipo de pruebas qué demostraciones realizar

### **Propiedades de los Requerimientos:**
- **Necesario**: Su omisión provoca deficiencia
- **Conciso**: Fácil de leer y entender
- **Completo**: No necesita ampliarse
- **Consistente**: No contradictorio
- **No ambiguo**: Una sola interpretación
- **Verificable**: Puede testearse

### **Características Adicionales:**
- Correcta, completa, verificable
- Comprensible por consumidores
- Modificable y rastreable
- Independiente del diseño
- Organizada y concisa

### **Aspectos Básicos de Especificación:**
- **Funcionalidad**: ¿Qué debe hacer el software?
- **Interfaces Externas**: ¿Cómo interactúa con el medio?
- **Rendimiento**: Velocidad, disponibilidad, tiempo de respuesta
- **Atributos**: Portabilidad, seguridad, mantenibilidad
- **Restricciones de Diseño**: Estándares, lenguajes, límites

---

## 📝 **Técnicas de Especificación**

### **Técnicas Estáticas:**
- Describen sistema a través de entidades, atributos y relaciones
- No consideran cambios en el tiempo
- **Ejemplos**: Referencias indirectas, expresiones regulares, abstracciones de datos

### **Técnicas Dinámicas:**
- Consideran cambios que ocurren en el tiempo
- Sistema cambia de estado por estímulos
- **Ejemplos**: Tablas de decisión, diagramas de transición de estados, redes de Petri

---

## 👤 **Historias de Usuario**

### **Definición:**
Descripción corta y simple de un requerimiento desde la perspectiva del usuario, escrita en lenguaje común.

### **Esquema Básico:**
```
Como (rol) quiero (algo) para (beneficio)
```

### **Ejemplos:**
- "Como usuario registrado quiero loguearme para empezar a utilizar la aplicación"
- "Como secretaria quiero imprimir el listado de turnos para guardar la información"

### **Características Clave (INVEST):**
- **Independientes**: Unas de otras
- **Negociables**: Requieren discusión para esclarecer alcance
- **Valoradas**: Por clientes o usuarios
- **Estimables**: Tiempo entre 10 horas y 2 semanas
- **Pequeñas**: Fáciles de estimar
- **Verificables**: Cubren requerimientos funcionales

### **Criterios de Aceptación:**
- Definen si historia fue desarrollada según expectativas
- Formato: **Dado** (contexto inicial), **Cuando** (evento), **Entonces** (resultado)
- Máximo 4 criterios por historia
- Escritos por el cliente, no el desarrollador

### **Plantilla de Historia de Usuario:**
```
ID: [Identificador único]
TÍTULO: Como <rol> quiero <algo> para <beneficio>
REGLAS DE NEGOCIO: [Normas y políticas aplicables]
CRITERIOS DE ACEPTACIÓN:
- Escenario 1: Dado..., Cuando..., Entonces...
- Escenario 2: Dado..., Cuando..., Entonces...
```

### **✅ Beneficios:**
- Implementación rápida (días/semanas)
- Poco mantenimiento
- Relación cercana con cliente
- Entregas pequeñas
- Estimación fácil del esfuerzo
- Ideal para requisitos volátiles

### **❌ Limitaciones:**
- Sin criterios pueden ser ambiguas
- Requiere contacto permanente con cliente
- Difícil escalar a proyectos grandes
- Requiere desarrolladores competentes

---

## 📚 **Épicas**

### **Definición:**
Conjunto de Historias de Usuario agrupadas por denominador común que representa un objetivo alcanzable.

### **Características:**
- Abarcan varios equipos de desarrollo
- Recogen muchas historias de usuario
- Clientes determinan qué historias eliminar/añadir
- Estructuran temas e iniciativas
- Dan flexibilidad y agilidad al proyecto

### **Ejemplo:**
```
Épica: Como Vicepresidente de ventas quiero revisar desempeño histórico 
para identificar regiones y productos de mejor desempeño

Se subdivide en:
- Como VP quiero seleccionar período de tiempo para analizar desempeño
- Como VP quiero clasificar información por región y productos
```

---

## 🔑 **Conceptos Clave para Recordar**

1. **Elicitación**: Combinar métodos interactivos y discretos para obtener panorama completo
2. **JRP/JAD**: Reuniones estructuradas con roles específicos bien definidos
3. **Brainstorming**: Cantidad de ideas genera calidad de soluciones
4. **Observación**: Técnica económica pero con limitaciones de comportamiento artificial
5. **Requerimientos**: Deben ser necesarios, concisos, completos, consistentes, no ambiguos y verificables
6. **Historias de Usuario**: Formato simple pero poderoso para capturar necesidades del usuario
7. **INVEST**: Características esenciales de buenas historias de usuario
8. **Criterios de Aceptación**: Definen cuándo una historia está "terminada"
9. **Épicas**: Agrupan historias relacionadas hacia objetivos mayores