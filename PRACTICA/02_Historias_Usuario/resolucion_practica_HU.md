# Resolución Práctica - Historias de Usuario

## Problema 1: Alquiler de mobiliario

### Roles identificados:
- **Encargado de mobiliario**
- **Cliente**

### Historias de Usuario:

---

#### Historia 1: Dar alta mobiliario

**ID:** Dar alta mobiliario

**TÍTULO:** Como encargado de mobiliario quiero dar de alta un mueble para poder incluirlo en el inventario disponible para alquiler.

**REGLAS DE NEGOCIO:**
- No pueden existir códigos de inventario repetidos
- El precio debe cargarse en dólares (política de franquicia)
- El encargado debe autenticarse para dar de alta mobiliario

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Alta exitosa de mobiliario
**Dado** que el encargado está autenticado y el código de inventario "MOB001" no existe en el sistema,
**Cuando** ingresa código "MOB001", tipo "Silla", fecha creación "01/01/2024", fecha último mantenimiento "15/01/2024", estado "libre" y precio "$50" y presiona "Dar de alta",
**Entonces** el sistema registra el mueble y confirma "Mobiliario registrado exitosamente".

**Escenario 2:** Alta fallida por código repetido
**Dado** que el encargado está autenticado y el código de inventario "MOB001" ya existe en el sistema,
**Cuando** intenta dar de alta un mueble con código "MOB001",
**Entonces** el sistema informa "El código de inventario ya existe, ingrese uno diferente".

**Escenario 3:** Alta fallida por falta de autenticación
**Dado** que el encargado no está autenticado en el sistema,
**Cuando** intenta acceder a la función de alta de mobiliario,
**Entonces** el sistema solicita autenticación antes de continuar.

---

#### Historia 2: Realizar reserva de alquiler

**ID:** Realizar reserva alquiler

**TÍTULO:** Como cliente quiero realizar una reserva de alquiler para poder asegurar el mobiliario para mi evento.

**REGLAS DE NEGOCIO:**
- Una reserva debe incluir mínimo 3 muebles
- Se debe abonar el 20% del total del alquiler
- Solo se acepta pago con tarjeta de crédito
- Se valida número de tarjeta y fondos a través del servicio del banco

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Reserva exitosa
**Dado** que hay mobiliario disponible y las condiciones son adecuadas para el pago,
**Cuando** el cliente selecciona 5 muebles, ingresa fecha "15/03/2024", lugar "Salón Central", cantidad de días "2" y realiza el pago del 20% con tarjeta válida,
**Entonces** el sistema procesa el pago, genera un número de reserva único y confirma "Reserva realizada exitosamente. Su número de reserva es: R123456".

**Escenario 2:** Reserva fallida por cantidad insuficiente de muebles
**Dado** que el cliente selecciona solo 2 muebles,
**Cuando** intenta realizar la reserva,
**Entonces** el sistema informa "Debe seleccionar al menos 3 muebles para realizar la reserva".

**Escenario 3:** Reserva fallida por error en el pago
**Dado** que el cliente selecciona 4 muebles pero la tarjeta no tiene fondos suficientes,
**Cuando** intenta realizar el pago del 20%,
**Entonces** el sistema informa "Error en el pago. Verifique los datos de su tarjeta y fondos disponibles".

---

#### Historia 3: Pagar con tarjeta

**ID:** Pagar tarjeta

**TÍTULO:** Como cliente quiero pagar con tarjeta de crédito para completar mi reserva de alquiler.

**REGLAS DE NEGOCIO:**
- Se valida número de tarjeta y fondos a través del servicio del banco
- Solo se acepta tarjeta de crédito

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Pago exitoso
**Dado** que la conexión con el banco es exitosa, la tarjeta "1234-5678-9012-3456" es válida y tiene fondos suficientes,
**Cuando** el cliente ingresa los datos de la tarjeta y presiona "Pagar",
**Entonces** el sistema valida con el banco, procesa el pago y retorna confirmación exitosa.

**Escenario 2:** Pago fallido por tarjeta inválida
**Dado** que la conexión con el banco es exitosa pero la tarjeta ingresada no es válida,
**Cuando** el cliente intenta realizar el pago,
**Entonces** el sistema retorna "Tarjeta de crédito no válida".

**Escenario 3:** Pago fallido por fondos insuficientes
**Dado** que la tarjeta es válida pero no tiene fondos suficientes,
**Cuando** el cliente intenta realizar el pago,
**Entonces** el sistema retorna "Fondos insuficientes en la tarjeta".

---

## Problema 2: Posgrado

### Roles identificados:
- **Empleado administrativo**
- **Alumno**

### Historias de Usuario:

---

#### Historia 1: Cargar carreras

**ID:** Cargar carreras

**TÍTULO:** Como empleado administrativo quiero cargar carreras de posgrado para que estén disponibles para inscripción.

**REGLAS DE NEGOCIO:**
- El nombre de la carrera no puede repetirse
- La duración máxima es de 5 años
- Se requiere: nombre, duración en años, costo y cantidad máxima de cuotas

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Carga exitosa de carrera
**Dado** que el nombre "Maestría en Informática" no existe en el sistema,
**Cuando** el empleado ingresa nombre "Maestría en Informática", duración "2 años", costo "$50000" y cantidad máxima de cuotas "12" y presiona "Cargar",
**Entonces** el sistema registra la carrera y confirma "Carrera cargada exitosamente".

**Escenario 2:** Carga fallida por nombre repetido
**Dado** que la carrera "Maestría en Informática" ya existe en el sistema,
**Cuando** el empleado intenta cargar una carrera con el mismo nombre,
**Entonces** el sistema informa "Ya existe una carrera con ese nombre".

**Escenario 3:** Carga fallida por duración excesiva
**Dado** que el empleado ingresa una duración de 6 años,
**Cuando** intenta cargar la carrera,
**Entonces** el sistema informa "La duración máxima permitida es de 5 años".

---

#### Historia 2: Registrar alumno

**ID:** Registrar alumno

**TÍTULO:** Como alumno quiero registrarme en el sistema para poder inscribirme a carreras de posgrado.

**REGLAS DE NEGOCIO:**
- Se requiere: nombre, apellido, nombre de usuario (único) y contraseña (más de 6 dígitos)
- El nombre de usuario debe ser único

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que el nombre de usuario "juan_perez" no existe en el sistema,
**Cuando** el alumno ingresa nombre "Juan", apellido "Pérez", usuario "juan_perez" y contraseña "123456789" y presiona "Registrarse",
**Entonces** el sistema registra al alumno y confirma "Registro exitoso".

**Escenario 2:** Registro fallido por nombre de usuario repetido
**Dado** que el nombre de usuario "juan_perez" ya existe,
**Cuando** un alumno intenta registrarse con ese mismo usuario,
**Entonces** el sistema informa "El nombre de usuario ya existe, elija otro".

**Escenario 3:** Registro fallido por contraseña corta
**Dado** que el alumno ingresa una contraseña de 5 dígitos,
**Cuando** intenta registrarse,
**Entonces** el sistema informa "La contraseña debe tener más de 6 dígitos".

---

#### Historia 3: Inscribir alumno a carrera

**ID:** Inscribir carrera

**TÍTULO:** Como alumno quiero inscribirme a una carrera de posgrado para poder cursarla.

**REGLAS DE NEGOCIO:**
- El alumno debe estar registrado y haber iniciado sesión
- Se debe abonar al momento de la inscripción
- Solo se acepta pago con tarjeta de crédito
- La tarjeta se valida a través del servicio del banco

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Inscripción exitosa
**Dado** que el alumno está autenticado, selecciona "Maestría en Informática", elige 6 cuotas, ingresa tarjeta válida con fondos,
**Cuando** presiona "Inscribirse",
**Entonces** el sistema procesa el pago, confirma la inscripción e imprime los comprobantes de inscripción y pago.

**Escenario 2:** Inscripción fallida por alumno no autenticado
**Dado** que el alumno no ha iniciado sesión,
**Cuando** intenta acceder a la inscripción,
**Entonces** el sistema solicita iniciar sesión primero.

**Escenario 3:** Inscripción fallida por error en el pago
**Dado** que el alumno está autenticado pero la tarjeta no tiene fondos,
**Cuando** intenta realizar el pago,
**Entonces** el sistema informa "Error en el pago. Verifique los datos de su tarjeta".

---

## Problema 3: Contratos

### Roles identificados:
- **Empleado de mesa de entradas**
- **Empleado de rendiciones**
- **Jefe de departamento**

### Historias de Usuario:

---

#### Historia 1: Confeccionar minuta

**ID:** Confeccionar minuta

**TÍTULO:** Como empleado de mesa de entradas quiero confeccionar una minuta para iniciar el proceso de contratación.

**REGLAS DE NEGOCIO:**
- Los montos no pueden superar $25.000
- La duración debe ser máximo 6 meses
- El sistema asocia automáticamente un número de minuta

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Minuta confeccionada exitosamente
**Dado** que los datos ingresados cumplen las reglas de negocio,
**Cuando** el empleado ingresa nombre "Juan Pérez", CUIT "20-12345678-9", tipo "Servicios profesionales", fecha inicio "01/03/2024", duración "3 meses" y monto "$20000" y presiona "Confeccionar",
**Entonces** el sistema genera automáticamente el número de minuta "MIN001" y confirma "Minuta confeccionada exitosamente".

**Escenario 2:** Minuta rechazada por monto excesivo
**Dado** que el empleado ingresa un monto de $30000,
**Cuando** intenta confeccionar la minuta,
**Entonces** el sistema informa "El monto no puede superar los $25.000".

**Escenario 3:** Minuta rechazada por duración excesiva
**Dado** que el empleado ingresa una duración de 8 meses,
**Cuando** intenta confeccionar la minuta,
**Entonces** el sistema informa "La duración máxima permitida es de 6 meses".

---

#### Historia 2: Aprobar minuta

**ID:** Aprobar minuta

**TÍTULO:** Como empleado de rendiciones quiero aprobar una minuta para que pueda convertirse en contrato.

**REGLAS DE NEGOCIO:**
- No se puede aprobar si la persona tiene 3 contratos vigentes
- No se puede aprobar si el CUIT está inhabilitado por AFIP
- Se verifica el estado del CUIT a través del servicio de AFIP

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Aprobación exitosa
**Dado** que la minuta "MIN001" existe, la persona no tiene 3 contratos vigentes y el CUIT está habilitado por AFIP,
**Cuando** el empleado ingresa "MIN001" y presiona "Aprobar",
**Entonces** el sistema muestra los datos de la minuta, verifica con AFIP y confirma "Minuta aprobada exitosamente".

**Escenario 2:** Aprobación rechazada por contratos vigentes
**Dado** que la persona ya tiene 3 contratos vigentes,
**Cuando** se intenta aprobar la minuta,
**Entonces** el sistema informa "No se puede aprobar. La persona ya tiene 3 contratos vigentes".

**Escenario 3:** Aprobación rechazada por CUIT inhabilitado
**Dado** que el CUIT está inhabilitado según AFIP,
**Cuando** se verifica el estado con AFIP,
**Entonces** el sistema informa "No se puede aprobar. El CUIT está inhabilitado por AFIP".

---

#### Historia 3: Verificar CUIT con AFIP

**ID:** Verificar CUIT

**TÍTULO:** Como sistema quiero verificar el estado de un CUIT con AFIP para validar la aprobación de minutas.

**REGLAS DE NEGOCIO:**
- Se debe enviar token de identificación y CUIT
- AFIP responde si el CUIT está habilitado o no

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Verificación exitosa - CUIT habilitado
**Dado** que el token es válido y el CUIT "20-12345678-9" está habilitado,
**Cuando** el sistema envía token y CUIT a AFIP,
**Entonces** AFIP responde "CUIT habilitado" y el sistema permite continuar el proceso.

**Escenario 2:** Verificación exitosa - CUIT inhabilitado
**Dado** que el token es válido pero el CUIT está inhabilitado,
**Cuando** el sistema consulta a AFIP,
**Entonces** AFIP responde "CUIT inhabilitado" y el sistema rechaza la operación.

**Escenario 3:** Verificación fallida por token inválido
**Dado** que el token enviado no es válido,
**Cuando** el sistema intenta conectarse con AFIP,
**Entonces** AFIP rechaza la conexión por token inválido.

---

#### Historia 4: Imprimir listado de minutas aprobadas

**ID:** Imprimir listado minutas

**TÍTULO:** Como empleado de rendiciones quiero imprimir un listado de minutas aprobadas para enviarlo al jefe de departamento.

**REGLAS DE NEGOCIO:**
- Solo se incluyen minutas aprobadas
- El listado es para que el jefe de departamento lo firme y eleve al decano

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Impresión exitosa con minutas aprobadas
**Dado** que existen minutas aprobadas en el sistema,
**Cuando** el empleado solicita imprimir el listado,
**Entonces** el sistema genera e imprime el listado con todas las minutas aprobadas.

**Escenario 2:** Listado vacío
**Dado** que no hay minutas aprobadas en el sistema,
**Cuando** el empleado solicita el listado,
**Entonces** el sistema informa "No hay minutas aprobadas para imprimir".

---

## Problema 4: Venta de bebidas

### Roles identificados:
- **Persona** (visitante)
- **Usuario** (registrado/premium)

### Historias de Usuario:

---

#### Historia 1: Registrar usuario

**ID:** Registrar usuario

**TÍTULO:** Como persona quiero registrarme en el sitio para poder comprar bebidas alcohólicas.

**REGLAS DE NEGOCIO:**
- Solo se permite registro a personas mayores de 18 años
- El mail debe ser único (será usado como nombre de usuario)
- El sistema genera automáticamente la contraseña

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que el mail "juan@email.com" no existe y la persona tiene 25 años,
**Cuando** ingresa nombre "Juan", apellido "Pérez", mail "juan@email.com", edad "25" y presiona "Registrarse",
**Entonces** el sistema genera una contraseña, la envía al mail y confirma "Registro exitoso. Contraseña enviada a su correo".

**Escenario 2:** Registro rechazado por menor de edad
**Dado** que la persona ingresa edad "17 años",
**Cuando** intenta registrarse,
**Entonces** el sistema muestra en pantalla el texto de la ley que impide la venta de bebidas alcohólicas a menores.

**Escenario 3:** Registro rechazado por mail existente
**Dado** que el mail "juan@email.com" ya existe en el sistema,
**Cuando** se intenta registrar con ese mail,
**Entonces** el sistema informa "El mail ingresado ya está registrado".

---

#### Historia 2: Realizar compra

**ID:** Realizar compra

**TÍTULO:** Como usuario quiero realizar una compra para adquirir bebidas alcohólicas.

**REGLAS DE NEGOCIO:**
- Usuario premium tiene 20% de descuento
- Compras superiores a $4500 tienen 10% de descuento
- Si es premium Y supera $4500, se aplican ambos descuentos
- Debe estar logueado para comprar

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Compra exitosa usuario regular sin descuento
**Dado** que el usuario está logueado, no es premium y selecciona productos por $3000,
**Cuando** finaliza la selección y presiona "Comprar",
**Entonces** el sistema muestra el total "$3000" y procede al pago.

**Escenario 2:** Compra con descuento por monto superior a $4500
**Dado** que el usuario no es premium pero selecciona productos por $5000,
**Cuando** finaliza la compra,
**Entonces** el sistema aplica 10% de descuento e informa "Total: $4500 (10% de descuento aplicado)".

**Escenario 3:** Compra usuario premium con ambos descuentos
**Dado** que el usuario es premium y selecciona productos por $5000,
**Cuando** finaliza la compra,
**Entonces** el sistema aplica 20% + 10% de descuento e informa el total con ambos descuentos.

---

## Problema 5: Casa de fotografía

### Roles identificados:
- **Cliente**
- **Empleado**

### Historias de Usuario:

---

#### Historia 1: Registrar cliente

**ID:** Registrar cliente

**TÍTULO:** Como cliente quiero registrarme para poder subir fotos e imprimirlas.

**REGLAS DE NEGOCIO:**
- Se requieren datos personales completos
- Nombre de usuario debe ser único

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que el nombre de usuario "juan123" no existe,
**Cuando** ingresa todos los datos requeridos con usuario "juan123" y presiona "Registrarse",
**Entonces** el sistema registra al cliente y confirma "Registro exitoso".

**Escenario 2:** Registro fallido por usuario existente
**Dado** que el usuario "juan123" ya existe,
**Cuando** se intenta registrar con ese usuario,
**Entonces** el sistema informa "El nombre de usuario ya existe".

---

#### Historia 2: Subir fotos

**ID:** Subir fotos

**TÍTULO:** Como cliente quiero subir mis fotos para poder imprimirlas.

**REGLAS DE NEGOCIO:**
- Máximo 50 fotos por pedido
- Se suben de a una foto
- Cliente debe estar autenticado

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Subida exitosa
**Dado** que el cliente está autenticado y ha subido 30 fotos,
**Cuando** sube una foto más,
**Entonces** el sistema acepta la foto y muestra "Foto subida exitosamente. Total: 31 fotos".

**Escenario 2:** Subida rechazada por límite alcanzado
**Dado** que el cliente ya subió 50 fotos,
**Cuando** intenta subir una foto más,
**Entonces** el sistema informa "Ha alcanzado el límite máximo de 50 fotos".

---

#### Historia 3: Pagar impresión

**ID:** Pagar impresión

**TÍTULO:** Como cliente quiero pagar la impresión de mis fotos para completar mi pedido.

**REGLAS DE NEGOCIO:**
- Cada foto cuesta $15
- Se paga con tarjeta de crédito
- La tarjeta se valida con el banco

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Pago exitoso
**Dado** que el cliente subió 10 fotos y la tarjeta es válida con fondos,
**Cuando** realiza el pago por $150,
**Entonces** el sistema procesa el pago, lo confirma y genera un código único de retiro.

**Escenario 2:** Pago rechazado por tarjeta inválida
**Dado** que la tarjeta ingresada no es válida,
**Cuando** se intenta procesar el pago,
**Entonces** el sistema informa "Tarjeta inválida. Verifique los datos".

---

#### Historia 4: Retirar fotos

**ID:** Retirar fotos

**TÍTULO:** Como empleado quiero registrar el retiro de fotos para completar el servicio al cliente.

**REGLAS DE NEGOCIO:**
- Se requiere código único válido
- Se registra fecha de retiro

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Retiro exitoso
**Dado** que el código "ABC123" es válido y corresponde a fotos pagadas,
**Cuando** el empleado ingresa el código y confirma la entrega,
**Entonces** el sistema registra la fecha de retiro y confirma "Fotos entregadas exitosamente".

**Escenario 2:** Retiro rechazado por código inválido
**Dado** que el código ingresado no existe,
**Cuando** se intenta registrar el retiro,
**Entonces** el sistema informa "Código inválido".

---

## Problema 6: Biblioteca

### Roles identificados:
- **Bibliotecaria**
- **Alumno/Socio**

### Historias de Usuario:

---

#### Historia 1: Asociar alumno

**ID:** Asociar alumno

**TÍTULO:** Como bibliotecaria quiero asociar un alumno para que pueda solicitar préstamos.

**REGLAS DE NEGOCIO:**
- Se requiere DNI y certificado de alumno regular
- Se otorga carnet con número de socio

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Asociación exitosa
**Dado** que el alumno presenta DNI y certificado válidos,
**Cuando** la bibliotecaria registra los datos,
**Entonces** el sistema genera un número de socio y otorga el carnet.

---

#### Historia 2: Realizar préstamo

**ID:** Realizar préstamo

**TÍTULO:** Como bibliotecaria quiero realizar un préstamo para que el socio pueda llevarse un libro.

**REGLAS DE NEGOCIO:**
- Solo a socios habilitados
- Máximo 3 préstamos vigentes por socio
- No debe tener préstamos vencidos
- El libro debe estar en buen estado

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Préstamo exitoso
**Dado** que el socio está habilitado, tiene 2 préstamos vigentes, no tiene vencidos y el libro está en buen estado,
**Cuando** solicita el préstamo,
**Entonces** la bibliotecaria registra el préstamo y entrega el libro.

**Escenario 2:** Préstamo rechazado por límite alcanzado
**Dado** que el socio ya tiene 3 préstamos vigentes,
**Cuando** solicita otro préstamo,
**Entonces** el sistema informa que ha alcanzado el límite máximo.

**Escenario 3:** Préstamo rechazado por préstamos vencidos
**Dado** que el socio tiene préstamos vencidos,
**Cuando** solicita un nuevo préstamo,
**Entonces** el sistema rechaza la solicitud por tener deudas pendientes.

---

#### Historia 3: Devolver libro

**ID:** Devolver libro

**TÍTULO:** Como bibliotecaria quiero registrar la devolución de un libro para actualizar el estado del préstamo.

**REGLAS DE NEGOCIO:**
- Se verifica si el préstamo está vencido
- Si está vencido, se suspende al socio por 15 días

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Devolución en tiempo
**Dado** que el préstamo no está vencido,
**Cuando** el socio devuelve el libro,
**Entonces** se registra la devolución exitosamente.

**Escenario 2:** Devolución con vencimiento
**Dado** que el préstamo está vencido,
**Cuando** se devuelve el libro,
**Entonces** el sistema registra la devolución y suspende al socio por 15 días.

---

## Problema 7: Mutual

### Roles identificados:
- **Persona** (solicitante de afiliación)
- **Afiliado**

### Historias de Usuario:

---

#### Historia 1: Afiliar persona

**ID:** Afiliar persona

**TÍTULO:** Como persona quiero afiliarme a la mutual para acceder a las prestaciones.

**REGLAS DE NEGOCIO:**
- Debe poseer tarjeta de crédito para pago automático
- Se otorga número de afiliado
- Puede tener a cargo pareja e hijos menores de 18 años

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Afiliación exitosa
**Dado** que la persona posee tarjeta de crédito válida,
**Cuando** completa el proceso de afiliación,
**Entonces** el sistema la registra como afiliada y le otorga un número de afiliado.

**Escenario 2:** Afiliación rechazada por falta de tarjeta
**Dado** que la persona no posee tarjeta de crédito,
**Cuando** intenta afiliarse,
**Entonces** el sistema rechaza la afiliación informando que requiere tarjeta de crédito.

---

#### Historia 2: Solicitar prestación ortodoncia

**ID:** Solicitar ortodoncia

**TÍTULO:** Como afiliado quiero solicitar prestación de ortodoncia para mi tratamiento dental.

**REGLAS DE NEGOCIO:**
- Solo una por afiliado
- Solo para menores de 15 años
- Afiliado desde al menos 9 meses
- Requiere historia clínica del profesional
- Pago del mes anterior al día

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Solicitud aprobada
**Dado** que el afiliado es menor de 15 años, está afiliado hace 10 meses, tiene el pago al día y presenta historia clínica,
**Cuando** solicita la prestación,
**Entonces** el sistema aprueba la solicitud de ortodoncia.

**Escenario 2:** Solicitud rechazada por edad
**Dado** que el afiliado tiene 16 años,
**Cuando** solicita ortodoncia,
**Entonces** el sistema rechaza la solicitud por superar el límite de edad.

**Escenario 3:** Solicitud rechazada por antigüedad insuficiente
**Dado** que el afiliado está afiliado hace 6 meses,
**Cuando** solicita ortodoncia,
**Entonces** el sistema rechaza por no cumplir los 9 meses de antigüedad.

---

#### Historia 3: Solicitar prestación plantillas

**ID:** Solicitar plantillas

**TÍTULO:** Como afiliado quiero solicitar prestación de plantillas para mi tratamiento podológico.

**REGLAS DE NEGOCIO:**
- Hasta 2 por año calendario
- Para cualquier afiliado
- Requiere indicación profesional y factura
- Pago del mes anterior al día

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Solicitud aprobada
**Dado** que el afiliado no ha solicitado plantillas este año, tiene pago al día y presenta documentación requerida,
**Cuando** solicita la prestación,
**Entonces** el sistema aprueba la solicitud.

**Escenario 2:** Solicitud rechazada por límite anual
**Dado** que el afiliado ya solicitó 2 plantillas este año,
**Cuando** solicita una tercera,
**Entonces** el sistema rechaza por haber alcanzado el límite anual.

---

## Problema 8: Teatro

### Roles identificados:
- **Empleado**
- **Cliente**
- **Vendedor de boletería**
- **Administrador**

### Historias de Usuario:

---

#### Historia 1: Reservar entradas

**ID:** Reservar entradas

**TÍTULO:** Como empleado quiero reservar entradas para clientes de forma gratuita.

**REGLAS DE NEGOCIO:**
- Solo presencial en el teatro
- Máximo 2 entradas por reserva
- Caducan 3 horas antes del evento
- Requiere datos de obra y espectador

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Reserva exitosa
**Dado** que hay disponibilidad para la función y el empleado está en el teatro,
**Cuando** ingresa datos de la obra y del espectador para 2 entradas,
**Entonces** el sistema registra la reserva con vencimiento 3 horas antes del evento.

**Escenario 2:** Reserva rechazada por exceso de entradas
**Dado** que se solicitan 3 entradas,
**Cuando** el empleado intenta hacer la reserva,
**Entonces** el sistema rechaza por exceder el límite de 2 entradas.

---

#### Historia 2: Comprar entrada web

**ID:** Comprar entrada web

**TÍTULO:** Como cliente quiero comprar entradas por web para asistir a una función.

**REGLAS DE NEGOCIO:**
- Pago solo con tarjeta de crédito
- Autorización a través del banco
- Se emite código de compra para retiro

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Compra exitosa
**Dado** que hay disponibilidad y la tarjeta es válida,
**Cuando** selecciona función, ingresa DNI, cantidad y realiza pago,
**Entonces** el sistema procesa la compra y emite código para retiro en boletería.

**Escenario 2:** Compra rechazada por tarjeta inválida
**Dado** que la tarjeta no es autorizada por el banco,
**Cuando** se intenta procesar el pago,
**Entonces** el sistema rechaza la compra por problemas con la tarjeta.

---

#### Historia 3: Retirar entradas con código

**ID:** Retirar entradas código

**TÍTULO:** Como vendedor de boletería quiero procesar códigos de compra para entregar las entradas correspondientes.

**REGLAS DE NEGOCIO:**
- Se requiere código válido
- Se imprimen las entradas correspondientes

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Retiro exitoso
**Dado** que el código "ABC123" es válido,
**Cuando** el vendedor ingresa el código,
**Entonces** el sistema verifica y imprime las entradas correspondientes.

**Escenario 2:** Retiro rechazado por código inválido
**Dado** que el código ingresado no existe,
**Cuando** se intenta procesar,
**Entonces** el sistema informa que el código no es válido.

---

#### Historia 4: Administrar programación

**ID:** Administrar programación

**TÍTULO:** Como administrador quiero gestionar la programación semanal para tener las obras disponibles para venta.

**REGLAS DE NEGOCIO:**
- Distribución semanal de obras en salas
- Debe estar disponible para venta de entradas

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Programación exitosa
**Dado** que el administrador tiene las obras y salas disponibles,
**Cuando** configura la distribución semanal,
**Entonces** el sistema actualiza la programación y la hace disponible para venta.

---

## Problema 9: Pago Electrónico

### Roles identificados:
- **Empleado**
- **Gerente**
- **Cliente**

### Historias de Usuario:

---

#### Historia 1: Procesar pago de factura

**ID:** Procesar pago factura

**TÍTULO:** Como empleado quiero procesar el pago de una factura para completar la transacción del cliente.

**REGLAS DE NEGOCIO:**
- Se conecta con central de cobro con token
- Si 2do vencimiento pasado: no se puede cobrar
- Si 1er vencimiento pasado: se aplica recargo
- Si no está vencida: monto original

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Pago exitoso sin vencimiento
**Dado** que la factura no está vencida y el token es válido,
**Cuando** el empleado ingresa el código de pago electrónico,
**Entonces** el sistema recupera los datos y cobra el monto original.

**Escenario 2:** Pago con recargo por 1er vencimiento
**Dado** que el 1er vencimiento está pasado pero no el 2do,
**Cuando** se procesa el pago,
**Entonces** el sistema aplica el recargo al monto original.

**Escenario 3:** Pago rechazado por 2do vencimiento
**Dado** que el 2do vencimiento está pasado,
**Cuando** se intenta cobrar,
**Entonces** el sistema informa que no se puede cobrar por vencimiento.

---

#### Historia 2: Registrar pagos del día

**ID:** Registrar pagos día

**TÍTULO:** Como gerente quiero registrar en la central los pagos del día para mantener actualizada la información.

**REGLAS DE NEGOCIO:**
- Solo una vez al día
- Requiere clave maestra
- No se pueden enviar transacciones duplicadas

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que la clave maestra es correcta y no se enviaron pagos hoy,
**Cuando** el gerente solicita enviar los pagos del día,
**Entonces** el sistema envía las transacciones y las marca como enviadas.

**Escenario 2:** Registro rechazado por envío duplicado
**Dado** que ya se enviaron los pagos del día,
**Cuando** el gerente intenta enviarlos nuevamente,
**Entonces** el sistema no permite el envío duplicado.

---

#### Historia 3: Ver estadísticas

**ID:** Ver estadísticas

**TÍTULO:** Como gerente quiero ver estadísticas de cobros para analizar el rendimiento.

**REGLAS DE NEGOCIO:**
- Requiere clave maestra
- Se agrupan por empresa
- Se especifica rango de fechas

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Estadísticas generadas exitosamente
**Dado** que la clave es correcta y el rango de fechas es válido,
**Cuando** el gerente solicita estadísticas,
**Entonces** el sistema muestra montos y cantidad de cobros agrupados por empresa.

---

## Problema 10: Un Aventón

### Roles identificados:
- **Usuario** (chofer/copiloto)

### Historias de Usuario:

---

#### Historia 1: Registrar usuario

**ID:** Registrar usuario

**TÍTULO:** Como persona quiero registrarme para poder usar el sistema de viajes compartidos.

**REGLAS DE NEGOCIO:**
- No puede haber correos duplicados
- Se requiere identificación correcta

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que el correo "juan@email.com" no existe,
**Cuando** ingresa usuario, correo y contraseña válidos,
**Entonces** el sistema registra al usuario exitosamente.

**Escenario 2:** Registro rechazado por correo duplicado
**Dado** que el correo ya existe,
**Cuando** se intenta registrar,
**Entonces** el sistema rechaza por correo duplicado.

---

#### Historia 2: Publicar viaje

**ID:** Publicar viaje

**TÍTULO:** Como usuario quiero publicar un viaje para compartir costos y encontrar acompañantes.

**REGLAS DE NEGOCIO:**
- Usuario debe estar autenticado
- Los viajes no pueden superponerse
- No puede publicar si adeuda calificaciones

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Publicación exitosa
**Dado** que el usuario está autenticado, no tiene viajes superpuestos y no adeuda calificaciones,
**Cuando** publica un viaje con fecha, hora y automóvil,
**Entonces** el sistema registra el viaje y lo hace disponible.

**Escenario 2:** Publicación rechazada por superposición
**Dado** que el usuario ya tiene un viaje en la misma fecha y hora,
**Cuando** intenta publicar otro,
**Entonces** el sistema rechaza por superposición de horarios.

**Escenario 3:** Publicación rechazada por calificaciones pendientes
**Dado** que el usuario adeuda calificaciones,
**Cuando** intenta publicar,
**Entonces** el sistema rechaza hasta completar las calificaciones pendientes.

---

#### Historia 3: Postularse a viaje

**ID:** Postularse viaje

**TÍTULO:** Como usuario quiero postularme a un viaje para acompañar a otro conductor.

**REGLAS DE NEGOCIO:**
- Usuario debe estar autenticado

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Postulación exitosa
**Dado** que el usuario está autenticado y el viaje está disponible,
**Cuando** se postula al viaje,
**Entonces** el sistema registra la postulación para que el chofer la evalúe.

---

#### Historia 4: Calificar usuarios

**ID:** Calificar usuarios

**TÍTULO:** Como usuario quiero calificar a otros usuarios para mantener el sistema de reputaciones.

**REGLAS DE NEGOCIO:**
- Solo después de viaje terminado
- Piloto califica copilotos y viceversa
- Calificación positiva suma 1 punto, negativa resta 1

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Calificación exitosa
**Dado** que el viaje terminó y el usuario participó,
**Cuando** califica positivamente a otro usuario,
**Entonces** el sistema suma 1 punto de reputación al calificado.

**Escenario 2:** Calificación negativa
**Dado** que el viaje terminó,
**Cuando** califica negativamente,
**Entonces** el sistema resta 1 punto de reputación.

---

## Problema 11: Concursos

### Roles identificados:
- **Docente**
- **Jefe del área de concursos**

### Historias de Usuario:

---

#### Historia 1: Registrar docente

**ID:** Registrar docente

**TÍTULO:** Como docente quiero registrarme para poder inscribirme a concursos.

**REGLAS DE NEGOCIO:**
- Mail debe ser único (será nombre de usuario)
- DNI debe estar entre 12 y 55 millones
- Sistema envía contraseña automática por mail

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que el DNI 30123456 está en rango válido y el mail no existe,
**Cuando** el docente completa registro con datos válidos,
**Entonces** el sistema lo registra y envía contraseña por mail.

**Escenario 2:** Registro rechazado por DNI inválido
**Dado** que el DNI ingresado es 60000000,
**Cuando** intenta registrarse,
**Entonces** el sistema rechaza por DNI fuera del rango permitido.

---

#### Historia 2: Inscribirse a concurso

**ID:** Inscribirse concurso

**TÍTULO:** Como docente quiero inscribirme a un concurso para participar en el proceso de selección.

**REGLAS DE NEGOCIO:**
- Máximo 3 concursos por docente
- Debe estar autenticado
- Se imprime comprobante

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Inscripción exitosa
**Dado** que el docente está autenticado y tiene menos de 3 inscripciones,
**Cuando** selecciona una materia y se inscribe,
**Entonces** el sistema registra la inscripción e imprime comprobante.

**Escenario 2:** Inscripción rechazada por límite
**Dado** que el docente ya está inscripto en 3 concursos,
**Cuando** intenta inscribirse a otro,
**Entonces** el sistema rechaza por exceder el límite.

---

#### Historia 3: Imprimir listado inscriptos

**ID:** Imprimir listado inscriptos

**TÍTULO:** Como jefe del área quiero imprimir listado de inscriptos para enviarlo al secretario administrativo.

**REGLAS DE NEGOCIO:**
- Requiere autenticación del jefe
- Se filtra por materia específica

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Listado generado exitosamente
**Dado** que el jefe está autenticado y hay inscriptos en la materia,
**Cuando** solicita el listado de una materia específica,
**Entonces** el sistema genera e imprime el listado de inscriptos.

---

## Problema 12: Créditos bancarios

### Roles identificados:
- **Cliente**
- **Gerente del banco**

### Historias de Usuario:

---

#### Historia 1: Iniciar trámite de crédito

**ID:** Iniciar trámite crédito

**TÍTULO:** Como cliente quiero iniciar un trámite de crédito para solicitar financiamiento.

**REGLAS DE NEGOCIO:**
- DNI debe corresponder a cliente del banco
- Monto máximo $400.000
- Si no es cliente: enviar instructivo por mail
- Si excede monto: rechazar con mensaje específico

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Trámite iniciado exitosamente
**Dado** que el DNI corresponde a un cliente y el monto es $350.000,
**Cuando** completa los datos y solicita el crédito,
**Entonces** el sistema acepta el trámite e imprime número de comprobante.

**Escenario 2:** Rechazo por no ser cliente
**Dado** que el DNI no corresponde a un cliente,
**Cuando** intenta iniciar trámite,
**Entonces** el sistema envía instructivo por mail para hacerse cliente.

**Escenario 3:** Rechazo por monto excesivo
**Dado** que el monto solicitado es $500.000,
**Cuando** intenta enviar la solicitud,
**Entonces** el sistema muestra "El monto solicitado excede el límite permitido".

---

#### Historia 2: Consultar estado de trámite

**ID:** Consultar estado trámite

**TÍTULO:** Como cliente quiero consultar el estado de mi trámite para conocer el progreso.

**REGLAS DE NEGOCIO:**
- Se requiere número de comprobante válido
- Tras 3 consultas inválidas se bloquea IP por 24 horas

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Consulta exitosa
**Dado** que el número de comprobante es válido,
**Cuando** el cliente consulta el estado,
**Entonces** el sistema retorna informe con el estado actual.

**Escenario 2:** Consulta fallida por comprobante inválido
**Dado** que el comprobante no existe,
**Cuando** se consulta,
**Entonces** el sistema muestra "trámite inexistente".

**Escenario 3:** Bloqueo por consultas inválidas
**Dado** que el cliente ingresó 3 códigos inexistentes,
**Cuando** intenta una cuarta consulta,
**Entonces** el sistema bloquea la IP por 24 horas.

---

#### Historia 3: Listar créditos aprobados

**ID:** Listar créditos aprobados

**TÍTULO:** Como gerente quiero obtener un listado de créditos aprobados para realizar seguimiento.

**REGLAS DE NEGOCIO:**
- Se especifica rango de fechas
- Solo créditos aprobados
- Fechas deben ser válidas

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Listado generado exitosamente
**Dado** que las fechas son válidas y hay créditos aprobados,
**Cuando** el gerente solicita el listado,
**Entonces** el sistema muestra los créditos aprobados en el rango.

**Escenario 2:** Listado vacío
**Dado** que no hay créditos aprobados en las fechas,
**Cuando** se solicita el listado,
**Entonces** el sistema muestra "No hay créditos aprobados en las fechas ingresadas".

---

## Problema 13: Venta de libros

### Roles identificados:
- **Visitante**
- **Usuario registrado**

### Historias de Usuario:

---

#### Historia 1: Registrar usuario (Paso 1)

**ID:** Registrar usuario paso1

**TÍTULO:** Como visitante quiero iniciar mi registro para poder comprar libros.

**REGLAS DE NEGOCIO:**
- Correo electrónico no debe existir en el sistema
- Clave debe tener 6 caracteres
- Sistema genera código de 16 dígitos y lo envía por correo

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro parcial exitoso
**Dado** que el correo "juan@email.com" no existe en el sistema,
**Cuando** ingresa nombre, apellido, DNI, correo válido y clave de 6 caracteres,
**Entonces** el sistema lo registra parcialmente, genera código de 16 dígitos y lo envía por correo.

**Escenario 2:** Registro rechazado por correo existente
**Dado** que el correo ya existe en el sistema,
**Cuando** intenta registrarse,
**Entonces** el sistema rechaza el registro por correo duplicado.

**Escenario 3:** Registro rechazado por clave corta
**Dado** que la clave tiene menos de 6 caracteres,
**Cuando** intenta registrarse,
**Entonces** el sistema rechaza por clave insuficiente.

---

#### Historia 2: Confirmar registro (Paso 2)

**ID:** Confirmar registro

**TÍTULO:** Como visitante quiero confirmar mi registro para completar el proceso de alta.

**REGLAS DE NEGOCIO:**
- Debe ingresar correo y código de 16 dígitos correcto
- Solo tras confirmación queda registrado definitivamente

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Confirmación exitosa
**Dado** que el correo y código de 16 dígitos coinciden con los enviados,
**Cuando** ingresa los datos en la página de confirmación,
**Entonces** el sistema lo registra definitivamente como usuario.

**Escenario 2:** Confirmación fallida por datos incorrectos
**Dado** que el código ingresado no coincide,
**Cuando** intenta confirmar,
**Entonces** el sistema rechaza la confirmación.

---

#### Historia 3: Comprar libro

**ID:** Comprar libro

**TÍTULO:** Como usuario registrado quiero comprar un libro para descargarlo.

**REGLAS DE NEGOCIO:**
- Solo usuarios registrados pueden comprar
- Nombre y apellido deben coincidir con titular de tarjeta
- Sistema valida con servidor de tarjeta

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Compra exitosa
**Dado** que el usuario está autenticado, ingresa ISBN válido y los datos de tarjeta coinciden,
**Cuando** selecciona "Comprar" y completa el pago,
**Entonces** el sistema procesa el pago y envía enlace de descarga por correo.

**Escenario 2:** Compra rechazada por datos no coincidentes
**Dado** que el nombre registrado no coincide con el titular de la tarjeta,
**Cuando** intenta comprar,
**Entonces** el sistema rechaza por datos inconsistentes.

---

## Problema 14: Manejo de tarjetas de crédito

### Roles identificados:
- **Personal del área comercial**
- **Gerente de sucursal**

### Historias de Usuario:

---

#### Historia 1: Autenticar usuario

**ID:** Autenticar usuario

**TÍTULO:** Como personal del banco quiero autenticarme para acceder a las funcionalidades del sistema.

**REGLAS DE NEGOCIO:**
- Credenciales son las mismas del sistema central del banco
- Sistema central envía token de autenticación si son correctas

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Autenticación exitosa
**Dado** que las credenciales son válidas en el sistema central,
**Cuando** el usuario ingresa sus credenciales,
**Entonces** el sistema central envía token válido y habilita funcionalidades.

**Escenario 2:** Autenticación fallida
**Dado** que las credenciales no son válidas,
**Cuando** intenta autenticarse,
**Entonces** el sistema central rechaza y no envía token.

---

#### Historia 2: Dar de alta tarjeta

**ID:** Dar alta tarjeta

**TÍTULO:** Como personal del banco quiero dar de alta una tarjeta para que el cliente pueda usarla.

**REGLAS DE NEGOCIO:**
- La persona debe ser cliente del banco
- No puede ser morosa en sistema SIVA
- SIVA proporciona número de tarjeta nuevo

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Alta exitosa
**Dado** que la persona es cliente, no es morosa en SIVA y los datos son válidos,
**Cuando** el personal completa el alta con nombre, DNI, CUIT y tipo de tarjeta,
**Entonces** SIVA confirma no morosidad, asigna número de tarjeta y el sistema registra el alta.

**Escenario 2:** Alta rechazada por morosidad
**Dado** que la persona es morosa según SIVA,
**Cuando** se verifica en el sistema SIVA,
**Entonces** el sistema rechaza el alta por morosidad.

**Escenario 3:** Alta rechazada por no ser cliente
**Dado** que la persona no es cliente del banco,
**Cuando** se intenta dar de alta,
**Entonces** el sistema rechaza por no ser cliente.

---

#### Historia 3: Dar de baja tarjeta

**ID:** Dar baja tarjeta

**TÍTULO:** Como personal del banco quiero dar de baja una tarjeta para desactivarla.

**REGLAS DE NEGOCIO:**
- Se requiere número de tarjeta
- Se elimina de base de datos del banco

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Baja exitosa
**Dado** que el número de tarjeta existe en el sistema,
**Cuando** el personal ingresa el número y confirma la baja,
**Entonces** el sistema elimina la tarjeta de la base de datos.

**Escenario 2:** Baja fallida por tarjeta inexistente
**Dado** que el número de tarjeta no existe,
**Cuando** se intenta dar de baja,
**Entonces** el sistema informa que la tarjeta no existe.

---

#### Historia 4: Listar operaciones por fechas

**ID:** Listar operaciones fechas

**TÍTULO:** Como gerente quiero obtener un listado de operaciones para realizar seguimiento.

**REGLAS DE NEGOCIO:**
- Solo el gerente puede acceder
- No se permiten fechas futuras
- Fecha inicio no puede ser mayor a fecha fin

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Listado generado exitosamente
**Dado** que el gerente está autenticado y las fechas son válidas,
**Cuando** solicita el listado entre fechas válidas,
**Entonces** el sistema muestra el listado de operaciones del período.

**Escenario 2:** Listado rechazado por fechas inválidas
**Dado** que la fecha de inicio es mayor a la fecha fin,
**Cuando** intenta generar el listado,
**Entonces** el sistema rechaza por rango de fechas inválido.

---

## Problema 15: Manejo de canchas de tenis

### Roles identificados:
- **Persona** (interesada en registrarse)
- **Usuario registrado**

### Historias de Usuario:

---

#### Historia 1: Registrar persona

**ID:** Registrar persona

**TÍTULO:** Como persona quiero registrarme para poder solicitar turnos en canchas de tenis.

**REGLAS DE NEGOCIO:**
- Solo mayores de 18 años
- Mail será usado como nombre de usuario
- Sistema genera contraseña automática

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que la persona tiene 25 años y el mail no existe,
**Cuando** completa registro con datos válidos,
**Entonces** el sistema la registra y envía contraseña generada por mail.

**Escenario 2:** Registro rechazado por menor de edad
**Dado** que la persona tiene 17 años,
**Cuando** intenta registrarse,
**Entonces** el sistema rechaza por ser menor de edad.

---

#### Historia 2: Solicitar turno

**ID:** Solicitar turno

**TÍTULO:** Como usuario quiero solicitar un turno para usar una cancha de tenis.

**REGLAS DE NEGOCIO:**
- Usuario debe estar autenticado
- Cuenta se bloquea tras 3 fallos de inicio de sesión
- No se permite turno con menos de 2 días de anticipación

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Turno asignado exitosamente
**Dado** que la cancha está libre y la fecha es con más de 2 días de anticipación,
**Cuando** el usuario solicita el turno,
**Entonces** el sistema asigna el turno e informa "Su turno ha sido registrado con éxito".

**Escenario 2:** Turno rechazado por cancha ocupada
**Dado** que la cancha está ocupada en el horario solicitado,
**Cuando** intenta reservar,
**Entonces** el sistema informa "Cancha ocupada, por favor seleccione otro día y horario".

**Escenario 3:** Turno rechazado por anticipación insuficiente
**Dado** que la fecha solicitada es mañana,
**Cuando** intenta solicitar el turno,
**Entonces** el sistema rechaza por no cumplir los 2 días mínimos de anticipación.

**Escenario 4:** Cuenta bloqueada por fallos de sesión
**Dado** que el usuario falló 3 veces al iniciar sesión,
**Cuando** intenta iniciar sesión nuevamente,
**Entonces** el sistema bloquea la cuenta.

---

## Problema 16: Procesamiento de imágenes

### Roles identificados:
- **Operario**
- **Supervisor**

### Historias de Usuario:

---

#### Historia 1: Autenticar operario

**ID:** Autenticar operario

**TÍTULO:** Como operario quiero autenticarme para acceder al sistema de procesamiento de imágenes.

**REGLAS DE NEGOCIO:**
- Se conecta al sistema general del observatorio
- Sistema retorna token si credenciales son correctas

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Autenticación exitosa
**Dado** que las credenciales son válidas en el sistema del observatorio,
**Cuando** el operario ingresa usuario y contraseña,
**Entonces** el sistema retorna token y habilita funcionalidades.

**Escenario 2:** Autenticación fallida
**Dado** que las credenciales no son válidas,
**Cuando** intenta autenticarse,
**Entonces** el sistema del observatorio rechaza el acceso.

---

#### Historia 2: Cargar imagen

**ID:** Cargar imagen

**TÍTULO:** Como operario quiero cargar una imagen para poder procesarla.

**REGLAS DE NEGOCIO:**
- Operario debe estar autenticado
- Imagen debe tener al menos 2 Megapixeles
- Se puede visualizar en escala de grises o color

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Carga exitosa
**Dado** que el operario está autenticado y selecciona imagen de 5 Megapixeles,
**Cuando** carga la imagen,
**Entonces** el sistema la acepta y ofrece opciones de visualización (grises/color).

**Escenario 2:** Carga rechazada por resolución insuficiente
**Dado** que la imagen seleccionada tiene 1.5 Megapixeles,
**Cuando** intenta cargarla,
**Entonces** el sistema rechaza por no cumplir el mínimo de 2 Megapixeles.

---

#### Historia 3: Recortar áreas de interés

**ID:** Recortar áreas

**TÍTULO:** Como operario quiero recortar áreas de interés para extraer partes específicas de la imagen.

**REGLAS DE NEGOCIO:**
- Debe haber imagen cargada previamente
- Máximo 4 áreas por imagen
- Las áreas no pueden superponerse

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Recorte exitoso
**Dado** que hay imagen cargada y se seleccionan 3 áreas sin superposición,
**Cuando** el operario marca las áreas y confirma,
**Entonces** el sistema procesa y almacena los recortes en disco.

**Escenario 2:** Recorte rechazado por superposición
**Dado** que una nueva área se superpone con otra existente,
**Cuando** intenta marcarla,
**Entonces** el sistema notifica el error por superposición.

**Escenario 3:** Recorte rechazado por límite alcanzado
**Dado** que ya se recortaron 4 áreas,
**Cuando** intenta recortar una quinta,
**Entonces** el sistema rechaza por exceder el límite máximo.

---

#### Historia 4: Listar imágenes procesadas

**ID:** Listar imágenes procesadas

**TÍTULO:** Como supervisor quiero ver un listado de imágenes procesadas para realizar seguimiento.

**REGLAS DE NEGOCIO:**
- Solo usuario supervisor puede acceder
- Se filtra por rango de fechas
- Máximo 20 imágenes por visualización

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Listado generado exitosamente
**Dado** que el supervisor está autenticado y hay 15 imágenes procesadas en el rango,
**Cuando** solicita el listado con fechas válidas,
**Entonces** el sistema muestra las 15 imágenes una debajo de otra.

**Escenario 2:** Listado limitado por máximo de visualización
**Dado** que hay 25 imágenes procesadas en el rango,
**Cuando** solicita el listado,
**Entonces** el sistema muestra solo las primeras 20 imágenes por limitaciones de visualización.

**Escenario 3:** Listado vacío
**Dado** que no hay imágenes procesadas en el rango de fechas,
**Cuando** solicita el listado,
**Entonces** el sistema informa que no hay imágenes para mostrar.

---

#### Historia 5: Cerrar sesión

**ID:** Cerrar sesión

**TÍTULO:** Como operario quiero cerrar sesión para finalizar el uso seguro del sistema.

**REGLAS DE NEGOCIO:**
- Usuario debe cerrar sesión al terminar

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Cierre de sesión exitoso
**Dado** que el usuario está autenticado,
**Cuando** solicita cerrar sesión,
**Entonces** el sistema cierra la sesión y requiere nueva autenticación para acceder.

---

## Resumen de Historias por Problema

### Problema 1 - Alquiler de mobiliario:
1. Dar alta mobiliario
2. Realizar reserva de alquiler  
3. Pagar con tarjeta

### Problema 2 - Posgrado:
1. Cargar carreras
2. Registrar alumno
3. Inscribir alumno a carrera

### Problema 3 - Contratos:
1. Confeccionar minuta
2. Aprobar minuta
3. Verificar CUIT con AFIP
4. Imprimir listado de minutas aprobadas

### Problema 4 - Venta de bebidas:
1. Registrar usuario
2. Realizar compra

### Problema 5 - Casa de fotografía:
1. Registrar cliente
2. Subir fotos
3. Pagar impresión
4. Retirar fotos

### Problema 6 - Biblioteca:
1. Asociar alumno
2. Realizar préstamo
3. Devolver libro

### Problema 7 - Mutual:
1. Afiliar persona
2. Solicitar prestación ortodoncia
3. Solicitar prestación plantillas

### Problema 8 - Teatro:
1. Reservar entradas
2. Comprar entrada web
3. Retirar entradas con código
4. Administrar programación

### Problema 9 - Pago Electrónico:
1. Procesar pago de factura
2. Registrar pagos del día
3. Ver estadísticas

### Problema 10 - Un Aventón:
1. Registrar usuario
2. Publicar viaje
3. Postularse a viaje
4. Calificar usuarios

### Problema 11 - Concursos:
1. Registrar docente
2. Inscribirse a concurso
3. Imprimir listado inscriptos

### Problema 12 - Créditos bancarios:
1. Iniciar trámite de crédito
2. Consultar estado de trámite
3. Listar créditos aprobados

### Problema 13 - Venta de libros:
1. Registrar usuario (Paso 1)
2. Confirmar registro (Paso 2)
3. Comprar libro

### Problema 14 - Manejo de tarjetas de crédito:
1. Autenticar usuario
2. Dar de alta tarjeta
3. Dar de baja tarjeta
4. Listar operaciones por fechas

### Problema 15 - Manejo de canchas de tenis:
1. Registrar persona
2. Solicitar turno

### Problema 16 - Procesamiento de imágenes:
1. Autenticar operario
2. Cargar imagen
3. Recortar áreas de interés
4. Listar imágenes procesadas
5. Cerrar sesión

---

**Total: 67 Historias de Usuario desarrolladas completamente con todos sus criterios de aceptación.**