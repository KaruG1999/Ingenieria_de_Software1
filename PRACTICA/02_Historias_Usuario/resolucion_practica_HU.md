# Historias de Usuario - Versión Corregida teniendo en cuenta comentarios en clase práctica

## Problema 1: Alquiler de mobiliario

### Roles identificados:

- **Encargado de mobiliario**
- **Cliente**

---

#### Historia 1: Dar alta mobiliario

**ID:** Dar alta mobiliario

**TÍTULO:** Como encargado de mobiliario quiero dar de alta un mueble para incluirlo en el inventario disponible.

**REGLAS DE NEGOCIO:**

- No pueden existir códigos repetidos
- Para que el encargado pueda dar de alta el mobiliario debe autenticarse en el sistema

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Alta exitosa de mobiliario
**Dado** que el encargado está autenticado y el código "MOB001" no existe,
**Cuando** ingresa código "MOB001", tipo "Silla", fecha creación "01/01/2024", fecha último mantenimiento "15/01/2024", estado "libre", precio "$50" y confirma el alta,
**Entonces** el sistema registra el mueble en el inventario.

**Escenario 2:** Alta fallida por código repetido
**Dado** que el encargado está autenticado y el código "MOB001" ya existe,
**Cuando** intenta dar de alta un mueble con código "MOB001",
**Entonces** el sistema rechaza el alta por código duplicado.

---

#### Historia 2: Realizar reserva de alquiler

**ID:** Realizar reserva alquiler

**TÍTULO:** Como cliente quiero realizar una reserva de alquiler para asegurar mobiliario para mi evento.

**REGLAS DE NEGOCIO:**

- Por una política comercial de la marca una reserva tiene que incluir como mínimo 3 muebles
- Para realizar una reserva se debe abonar el 20% del total del alquiler

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Reserva exitosa
**Dado** que hay mobiliario disponible y las condiciones son adecuadas para un pago exitoso,
**Cuando** el cliente selecciona 5 muebles, ingresa fecha "15/03/2024", lugar "Salón Central", cantidad de días "2" y procede al pago,
**Entonces** el sistema procesa el pago del 20%, emite número de reserva único "R123456" y confirma la reserva.

**Escenario 2:** Reserva fallida por cantidad insuficiente de muebles
**Dado** que el cliente selecciona solo 2 muebles,
**Cuando** intenta realizar la reserva,
**Entonces** el sistema rechaza la reserva por no cumplir el mínimo de 3 muebles.

**Escenario 3:** Reserva fallida por error en pago
**Dado** que el cliente selecciona 4 muebles pero las condiciones no son adecuadas para un pago exitoso,
**Cuando** intenta realizar el pago del 20%,
**Entonces** el sistema rechaza la reserva por fallo en el pago.

---

#### Historia 3: Pagar con tarjeta de crédito

**ID:** Pagar tarjeta

**TÍTULO:** Como cliente quiero pagar con tarjeta de crédito para completar mi reserva.

**REGLAS DE NEGOCIO:**

- El pago de la reserva se realiza únicamente con tarjeta de crédito validando número de tarjeta y fondos a través de un servicio del banco

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Pago exitoso
**Dado** que la tarjeta "1234-5678-9012-3456" es válida y tiene fondos suficientes según el servicio del banco,
**Cuando** el cliente ingresa los datos de la tarjeta y confirma el pago,
**Entonces** el sistema valida con el banco, procesa el pago y retorna confirmación exitosa.

**Escenario 2:** Pago fallido por tarjeta inválida
**Dado** que la tarjeta ingresada no es válida según el servicio del banco,
**Cuando** el cliente intenta realizar el pago,
**Entonces** el sistema retorna error de validación de tarjeta.

**Escenario 3:** Pago fallido por fondos insuficientes
**Dado** que la tarjeta es válida pero no tiene fondos suficientes según el servicio del banco,
**Cuando** el cliente intenta realizar el pago,
**Entonces** el sistema retorna error por fondos insuficientes.

---

## Problema 2: Cadena hotelera

### Roles identificados:

- **Usuario**
- **Conserje**

---

#### Historia 1: Reservar hospedaje

**ID:** Reservar hospedaje

**TÍTULO:** Como usuario quiero reservar un hospedaje para asegurar mi estadía.

**REGLAS DE NEGOCIO:**

- La fecha de ingreso debe estar dentro de los 90 días a partir de la fecha actual
- Las estadías no pueden durar más de 15 días

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Reserva exitosa
**Dado** que la fecha de ingreso "15/03/2024" está dentro de 90 días y la estadía es de 10 días,
**Cuando** ingresa fecha ingreso, fecha egreso "25/03/2024", hotel "Plaza Central", cantidad personas "2" y confirma,
**Entonces** el sistema realiza la reserva y envía correo electrónico con código de reserva y enlace para continuar con el pago.

**Escenario 2:** Reserva fallida por fecha fuera de rango
**Dado** que la fecha de ingreso está a más de 90 días de la fecha actual,
**Cuando** intenta hacer la reserva,
**Entonces** el sistema rechaza la reserva por fecha fuera del rango permitido.

**Escenario 3:** Reserva fallida por estadía excesiva
**Dado** que la estadía solicitada supera los 15 días,
**Cuando** intenta reservar,
**Entonces** el sistema rechaza la reserva por exceder el máximo de días permitidos.

---

#### Historia 2: Realizar check in

**ID:** Realizar check in

**TÍTULO:** Como usuario quiero hacer check in para acceder a mi habitación.

**REGLAS DE NEGOCIO:**

- Los check in pueden realizarse después de las 10 am y hasta las 23:59 pm

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Check in exitoso
**Dado** que son las 14:00 pm y el código "RES123456" tiene reserva para la fecha actual,
**Cuando** ingresa el código en la terminal,
**Entonces** el sistema informa habitación asignada "205", manda mensaje a conserje para guiar al usuario y mensaje a botones para las valijas.

**Escenario 2:** Check in fallido por código inválido
**Dado** que el código ingresado no tiene reserva para la fecha actual,
**Cuando** intenta hacer check in,
**Entonces** el sistema informa que el código no es válido.

**Escenario 3:** Check in fallido por horario no permitido
**Dado** que son las 8:00 am (antes de las 10:00 am),
**Cuando** intenta realizar check in,
**Entonces** el sistema informa que aún no se encuentran habilitados los ingresos al hotel.

---

#### Historia 3: Realizar check out

**ID:** Realizar check out

**TÍTULO:** Como conserje quiero realizar el check out para liberar la habitación.

**REGLAS DE NEGOCIO:**

- Solo se puede realizar check out de habitaciones sin gastos

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Check out exitoso
**Dado** que la habitación "205" no tiene gastos pendientes,
**Cuando** ingresa número de habitación "205" y confirma check out,
**Entonces** el sistema libera la habitación y envía mensaje a las mucamas avisando que puede limpiarse.

**Escenario 2:** Check out fallido por gastos pendientes
**Dado** que la habitación "205" tiene gastos sin abonar,
**Cuando** intenta hacer check out,
**Entonces** el sistema informa que no puede hacerse hasta que no se abonen los gastos realizados.

---

## Problema 3: Venta de bebidas

### Roles identificados:

- **Persona**
- **Usuario registrado/premium**

---

#### Historia 1: Registrar usuario

**ID:** Registrar usuario

**TÍTULO:** Como persona quiero registrarme para poder comprar bebidas alcohólicas.

**REGLAS DE NEGOCIO:**

- Solo se permite que se registren al sitio personas mayores a 18 años
- El mail será utilizado como nombre de usuario por lo tanto debe ser único

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que la persona tiene 25 años y el mail "juan@email.com" no existe,
**Cuando** completa el registro con datos válidos,
**Entonces** el sistema genera contraseña y la envía al email ingresado.

**Escenario 2:** Registro rechazado por menor de edad
**Dado** que la persona tiene 17 años,
**Cuando** intenta registrarse,
**Entonces** el sistema muestra en pantalla el texto de la ley que impide la venta de bebidas alcohólicas a menores.

**Escenario 3:** Registro rechazado por mail existente
**Dado** que el mail "juan@email.com" ya está registrado,
**Cuando** intenta registrarse con ese mail,
**Entonces** el sistema rechaza el registro por mail duplicado.

---

#### Historia 2: Comprar bebidas

**ID:** Comprar bebidas

**TÍTULO:** Como usuario quiero comprar bebidas para adquirir productos alcohólicos.

**REGLAS DE NEGOCIO:**

- Si el usuario es premium se le hace un descuento del 20%
- Si el usuario seleccionó productos por un monto superior a los $4500 se le hace un 10% de descuento
- Si el usuario es premium y compra por un monto superior a $4500 se deben aplicar ambos descuentos

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Compra exitosa usuario regular sin descuento
**Dado** que el usuario está logueado, no es premium y selecciona productos por $3000,
**Cuando** finaliza la selección,
**Entonces** el sistema muestra total "$3000" sin descuentos aplicados.

**Escenario 2:** Compra con descuento por monto superior a $4500
**Dado** que el usuario no es premium y selecciona productos por $5000,
**Cuando** finaliza la compra,
**Entonces** el sistema aplica 10% de descuento e informa en pantalla total "$4500" menos el 10%.

**Escenario 3:** Compra usuario premium con ambos descuentos
**Dado** que el usuario es premium y selecciona productos por $5000,
**Cuando** finaliza la compra,
**Entonces** el sistema aplica descuento del 20% por ser premium y 10% por monto superior a $4500.

---

## Problema 4: Biblioteca

### Roles identificados:

- **Bibliotecaria**
- **Alumno/Socio**

---

#### Historia 1: Asociar alumno

**ID:** Asociar alumno

**TÍTULO:** Como bibliotecaria quiero asociar un alumno para que pueda solicitar préstamos.

**REGLAS DE NEGOCIO:**

- Para que un alumno pueda asociarse debe presentar el DNI

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Asociación exitosa
**Dado** que el alumno presenta DNI válido,
**Cuando** la bibliotecaria procesa la asociación,
**Entonces** el sistema otorga carnet con número de socio correspondiente.

---

#### Historia 2: Realizar préstamo

**ID:** Realizar préstamo

**TÍTULO:** Como bibliotecaria quiero realizar préstamos para que los socios puedan llevarse libros.

**REGLAS DE NEGOCIO:**

- Los préstamos se realizan exclusivamente a socios habilitados, que no posean más de tres préstamos vigentes y no tengan préstamos vencidos
- La bibliotecaria presta libros que se encuentren en buen estado

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Préstamo exitoso
**Dado** que el socio está habilitado, tiene 2 préstamos vigentes, no tiene vencidos y el libro está en buen estado,
**Cuando** solicita el préstamo,
**Entonces** la bibliotecaria registra el préstamo y entrega el libro.

**Escenario 2:** Préstamo rechazado por límite de préstamos
**Dado** que el socio ya tiene 3 préstamos vigentes,
**Cuando** solicita otro préstamo,
**Entonces** el sistema rechaza por haber alcanzado el límite máximo.

**Escenario 3:** Préstamo rechazado por préstamos vencidos
**Dado** que el socio tiene préstamos vencidos,
**Cuando** solicita un préstamo,
**Entonces** el sistema rechaza por tener deudas pendientes.

**Escenario 4:** Préstamo rechazado por libro deteriorado
**Dado** que el libro solicitado se encuentra deteriorado,
**Cuando** se intenta prestar,
**Entonces** el sistema rechaza el préstamo por estado del libro.

---

#### Historia 3: Devolver libro

**ID:** Devolver libro

**TÍTULO:** Como bibliotecaria quiero procesar devoluciones para actualizar el estado de los préstamos.

**REGLAS DE NEGOCIO:**

- Cuando el socio retorna un libro se verifica si el préstamo se encuentra vencido. En este caso, la bibliotecaria suspende al socio, que por 15 días no podrá solicitar nuevos préstamos

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Devolución en tiempo
**Dado** que el préstamo no está vencido,
**Cuando** el socio devuelve el libro,
**Entonces** el sistema registra la devolución exitosamente.

**Escenario 2:** Devolución con vencimiento
**Dado** que el préstamo está vencido,
**Cuando** se devuelve el libro,
**Entonces** la bibliotecaria suspende al socio por 15 días y el socio no podrá solicitar nuevos préstamos durante ese período.

---

## Problema 5: Manejo de licencias

### Roles identificados:

- **Empleado**
- **Administrativo**

---

#### Historia 1: Solicitar licencia médica

**ID:** Solicitar licencia

**TÍTULO:** Como empleado quiero solicitar una licencia médica para justificar mi reposo.

**REGLAS DE NEGOCIO:**

- Para poder solicitar una licencia el empleado debe tener más de 1 mes de antigüedad
- Podrá solicitar una licencia un empleado que no tenga una licencia vigente

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Solicitud exitosa
**Dado** que el empleado tiene más de 1 mes de antigüedad y no tiene licencia vigente,
**Cuando** ingresa CUIL, tipo, fecha de inicio, matrícula médico, diagnóstico y destinatario,
**Entonces** el sistema genera código de licencia y lo envía vía mail con confirmación y días otorgados.

**Escenario 2:** Solicitud rechazada por antigüedad insuficiente
**Dado** que el empleado tiene menos de 1 mes de antigüedad,
**Cuando** intenta solicitar licencia,
**Entonces** el sistema informa rechazo de la licencia.

**Escenario 3:** Solicitud rechazada por licencia vigente
**Dado** que el empleado tiene una licencia vigente,
**Cuando** intenta solicitar nueva licencia,
**Entonces** el sistema rechaza la solicitud.

---

#### Historia 2: Consultar licencias

**ID:** Consultar licencias

**TÍTULO:** Como administrativo quiero consultar licencias solicitadas para realizar seguimiento.

**REGLAS DE NEGOCIO:**

- Por una cuestión de costos se podrá imprimir un informe por mes para cada empleado

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Consulta exitosa
**Dado** que no se imprimió informe este mes para el empleado,
**Cuando** ingresa CUIL del empleado y rango de fechas,
**Entonces** el sistema imprime informe de las licencias solicitadas.

**Escenario 2:** Consulta rechazada por límite mensual
**Dado** que ya se imprimió un informe este mes para el empleado,
**Cuando** intenta imprimir otro,
**Entonces** el sistema rechaza por límite de un informe mensual por empleado.

---

## Problema 6: Pago Electrónico

### Roles identificados:

- **Empleado/Gerente**

---

#### Historia 1: Procesar pago de factura

**ID:** Procesar pago

**TÍTULO:** Como empleado quiero procesar el pago de una factura para completar la transacción.

**REGLAS DE NEGOCIO:**

- Cuando el 2do vencimiento está vencido se debe informar que la factura no se puede cobrar
- Cuando el 1er vencimiento está vencido hay que aplicar el recargo al monto original
- Si la factura no está vencida, se cobra el monto original

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Pago exitoso sin vencimiento
**Dado** que la factura no está vencida,
**Cuando** ingresa el código de pago electrónico,
**Entonces** el sistema se conecta con la central, recupera datos y cobra el monto original.

**Escenario 2:** Pago con recargo por primer vencimiento
**Dado** que el primer vencimiento está vencido pero no el segundo,
**Cuando** procesa el pago,
**Entonces** el sistema aplica el recargo al monto original.

**Escenario 3:** Pago rechazado por segundo vencimiento
**Dado** que el segundo vencimiento está vencido,
**Cuando** intenta procesar el pago,
**Entonces** el sistema informa que la factura no se puede cobrar por dicho motivo.

---

#### Historia 2: Registrar pagos del día

**ID:** Registrar pagos día

**TÍTULO:** Como gerente quiero registrar en la central los pagos del día para mantener actualizada la información.

**REGLAS DE NEGOCIO:**

- No deben enviarse dos veces las transacciones

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que la clave maestra es correcta y no se enviaron pagos del día,
**Cuando** solicita registrar pagos del día,
**Entonces** el sistema conecta a la central, envía transacciones y las marca como enviadas tras confirmación.

**Escenario 2:** Registro rechazado por envío duplicado
**Dado** que ya se enviaron los pagos del día,
**Cuando** intenta enviar segunda vez,
**Entonces** el sistema no permite el envío.

---

#### Historia 3: Ver estadísticas

**ID:** Ver estadísticas

**TÍTULO:** Como gerente quiero ver estadísticas de cobros para analizar el rendimiento.

**REGLAS DE NEGOCIO:**

- (No hay reglas explícitas en el enunciado)

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Estadísticas generadas exitosamente
**Dado** que la clave maestra es correcta,
**Cuando** ingresa rango de fechas,
**Entonces** el sistema muestra montos y cantidad de cobros realizados agrupando por empresa.

---

## Problema 7: Transferencias vehiculares

### Roles identificados:

- **Usuario registrado**

---

#### Historia 1: Iniciar trámite de transferencia

**ID:** Iniciar trámite

**TÍTULO:** Como usuario quiero iniciar un trámite de transferencia para transferir mi vehículo.

**REGLAS DE NEGOCIO:**

- Para que una transferencia se lleve a cabo con éxito, la patente ingresada no debe tener deudas y tanto el vendedor como el comprador deben ser mayores de 18 años

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Trámite iniciado exitosamente
**Dado** que la patente no tiene deudas y vendedor y comprador son mayores de 18 años,
**Cuando** ingresa patente, DNI vendedor y DNI comprador,
**Entonces** el sistema envía al mail del comprador código para realizar el pago.

**Escenario 2:** Trámite rechazado por deudas
**Dado** que la patente tiene deudas,
**Cuando** intenta iniciar el trámite,
**Entonces** el sistema informa el motivo del rechazo.

**Escenario 3:** Trámite rechazado por menor de edad
**Dado** que vendedor o comprador es menor de 18 años,
**Cuando** intenta iniciar el trámite,
**Entonces** el sistema informa el motivo del rechazo.

---

#### Historia 2: Consultar estado de transferencia

**ID:** Consultar estado

**TÍTULO:** Como usuario quiero consultar el estado de una transferencia para conocer el progreso.

**REGLAS DE NEGOCIO:**

- Se pueden hacer hasta tres consultas por mes

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Consulta exitosa
**Dado** que no se alcanzó el límite de 3 consultas mensuales,
**Cuando** ingresa una patente,
**Entonces** el sistema informa el estado de la transferencia.

**Escenario 2:** Consulta rechazada por límite alcanzado
**Dado** que ya se realizaron 3 consultas este mes,
**Cuando** intenta consultar nuevamente,
**Entonces** el sistema rechaza la consulta por límite mensual alcanzado.

---

## Problema 8: Concursos

### Roles identificados:

- **Docente**
- **Jefe del área de concursos**

---

#### Historia 1: Registrar docente

**ID:** Registrar docente

**TÍTULO:** Como docente quiero registrarme para inscribirme a concursos.

**REGLAS DE NEGOCIO:**

- El mail debe ser único y será utilizado como nombre de usuario
- Los dni permitidos para concursar son aquellos menores a 55 millones y mayores a 12 millones

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que el DNI está entre 12 y 55 millones y el mail es único,
**Cuando** completa DNI, nombre, apellido y mail,
**Entonces** el sistema manda a la casilla de correo la contraseña asignada automáticamente.

**Escenario 2:** Registro rechazado por DNI fuera de rango
**Dado** que el DNI no está entre 12 y 55 millones,
**Cuando** intenta registrarse,
**Entonces** el sistema rechaza el registro.

**Escenario 3:** Registro rechazado por mail existente
**Dado** que el mail ya existe en el sistema,
**Cuando** intenta registrarse,
**Entonces** el sistema rechaza por mail duplicado.

---

#### Historia 2: Inscribirse a concurso

**ID:** Inscribirse concurso

**TÍTULO:** Como docente quiero inscribirme a un concurso para participar en la selección.

**REGLAS DE NEGOCIO:**

- El docente no podrá inscribirse a más de 3 concursos

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Inscripción exitosa
**Dado** que el docente tiene menos de 3 inscripciones,
**Cuando** selecciona materia y acepta la inscripción,
**Entonces** el sistema imprime comprobante.

**Escenario 2:** Inscripción rechazada por límite alcanzado
**Dado** que el docente ya está inscripto en 3 concursos,
**Cuando** intenta inscribirse a otro,
**Entonces** el sistema rechaza por límite de 3 concursos.

---

#### Historia 3: Imprimir listado de inscriptos

**ID:** Imprimir listado

**TÍTULO:** Como jefe del área quiero imprimir listado de inscriptos para enviarlo al secretario administrativo.

**REGLAS DE NEGOCIO:**

- (No hay reglas explícitas en el enunciado)

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Listado impreso exitosamente
**Dado** que hay inscriptos en la materia seleccionada,
**Cuando** el jefe solicita el listado de una materia,
**Entonces** el sistema imprime listado con los inscriptos para envío al secretario administrativo.

---

## Problema 9: Créditos bancarios

### Roles identificados:

- **Cliente**
- **Gerente**

---

#### Historia 1: Iniciar trámite de crédito

**ID:** Iniciar trámite

**TÍTULO:** Como cliente quiero iniciar un trámite de crédito para solicitar financiamiento.

**REGLAS DE NEGOCIO:**

- El sistema acepta el inicio de trámite si el dni ingresado corresponde a un cliente del banco y si el crédito solicitado no supera los $400.000
- En caso de que no sea cliente del banco el sistema deberá enviar un correo electrónico al email ingresado con un instructivo para hacerse cliente
- Si el monto supera los $400.000 el sistema rechaza el inicio de trámite

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Trámite iniciado exitosamente
**Dado** que el DNI corresponde a un cliente y el crédito no supera $400.000,
**Cuando** completa los datos del trámite,
**Entonces** el sistema almacena el trámite para análisis del área económica e imprime número de comprobante.

**Escenario 2:** Rechazo por no ser cliente
**Dado** que el DNI no corresponde a un cliente del banco,
**Cuando** intenta iniciar trámite,
**Entonces** el sistema envía correo electrónico con instructivo para hacerse cliente.

**Escenario 3:** Rechazo por monto excesivo
**Dado** que el crédito supera los $400.000,
**Cuando** intenta iniciar trámite,
**Entonces** el sistema muestra "El monto solicitado excede el límite permitido".

---

#### Historia 2: Consultar estado de trámite

**ID:** Consultar estado

**TÍTULO:** Como cliente quiero consultar el estado de mi trámite para conocer su progreso.

**REGLAS DE NEGOCIO:**

- Si el cliente ingresa tres veces un código inexistente el sistema bloquea la ip del cliente por 24 horas

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Consulta exitosa
**Dado** que el número de comprobante es válido,
**Cuando** ingresa el número,
**Entonces** el sistema retorna informe con el estado del trámite.

**Escenario 2:** Consulta fallida por comprobante inexistente
**Dado** que el comprobante no existe,
**Cuando** intenta consultar,
**Entonces** el sistema muestra "trámite inexistente".

**Escenario 3:** Bloqueo por consultas inválidas
**Dado** que el cliente ingresó tres códigos inexistentes,
**Cuando** intenta una cuarta consulta,
**Entonces** el sistema bloquea la ip por 24 horas mostrando "Usted ha excedido el número de consultas inválidas".

---

#### Historia 3: Listar créditos aprobados

**ID:** Listar créditos

**TÍTULO:** Como gerente quiero obtener listado de créditos aprobados para realizar seguimiento.

**REGLAS DE NEGOCIO:**

- (No hay reglas explícitas en el enunciado)

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Listado generado exitosamente
**Dado** que las fechas ingresadas son válidas y hay créditos aprobados,
**Cuando** solicita el listado entre fechas,
**Entonces** el sistema muestra listado con los créditos aprobados.

**Escenario 2:** Listado vacío
**Dado** que no hay créditos aprobados en las fechas ingresadas,
**Cuando** solicita el listado,
**Entonces** el sistema muestra "No hay créditos aprobados en las fechas ingresadas".

**Escenario 3:** Listado rechazado por fechas inválidas
**Dado** que las fechas ingresadas no son válidas,
**Cuando** solicita el listado,
**Entonces** el sistema muestra "las fechas ingresadas no son válidas".

---

## Problema 10: Manejo de canchas de tenis

### Roles identificados:

- **Persona**
- **Usuario registrado**

---

#### Historia 1: Registrar persona

**ID:** Registrar persona

**TÍTULO:** Como persona quiero registrarme para solicitar turnos en canchas.

**REGLAS DE NEGOCIO:**

- Solo quiere que se registren personas mayores de edad (18 años o más)

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que la persona tiene 18 años o más,
**Cuando** completa el registro con datos válidos,
**Entonces** el sistema genera contraseña y la envía al correo ingresado.

**Escenario 2:** Registro rechazado por menor de edad
**Dado** que la persona tiene menos de 18 años,
**Cuando** intenta registrarse,
**Entonces** el sistema rechaza el registro por ser menor de edad.

---

#### Historia 2: Solicitar turno

**ID:** Solicitar turno

**TÍTULO:** Como usuario quiero solicitar un turno para usar una cancha de tenis.

**REGLAS DE NEGOCIO:**

- Si un usuario falla tres veces al iniciar sesión su cuenta sea bloqueada
- El sistema no debe permitir dar turno con menos de 2 días a la fecha en que se solicita

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Turno asignado exitosamente
**Dado** que la cancha está libre y la fecha tiene más de 2 días de anticipación,
**Cuando** ingresa cancha, fecha y hora,
**Entonces** el sistema asigna el turno informando "Su turno ha sido registrado con éxito".

**Escenario 2:** Turno rechazado por cancha ocupada
**Dado** que la cancha está ocupada en la fecha y hora solicitada,
**Cuando** solicita el turno,
**Entonces** el sistema informa "Cancha ocupada, por favor seleccione otro día y horario" y permite seleccionar nuevamente.

**Escenario 3:** Turno rechazado por anticipación insuficiente
**Dado** que la fecha solicitada tiene menos de 2 días de anticipación,
**Cuando** intenta solicitar el turno,
**Entonces** el sistema no permite dar el turno por no cumplir el mínimo de anticipación.

**Escenario 4:** Cuenta bloqueada por fallos de sesión
**Dado** que el usuario falló tres veces al iniciar sesión,
**Cuando** intenta iniciar sesión nuevamente,
**Entonces** el sistema bloquea la cuenta.

---

## Resumen de correcciones aplicadas según criterios del profesor (apuntes tomados en clase):

### ✅ **Reglas de negocio**: Solo las escritas textualmente en el enunciado

- Si o si deben estar explicitamente en el enunciado
- En caso de no estar en enunciado, debo considerarlo un escenario y es necesario controlar

### ✅ **Títulos en primera persona**: Todos usan "quiero", "deseo" o "necesito"

- "Como X quiero Y para Z"
- Enfoque en el beneficio personal del rol

### ✅ **No validaciones como escenarios**

- No incluí validaciones de formato, campos requeridos, etc.
- Me enfoqué en reglas de negocio y flujos funcionales

### ✅ **Una HU = Una funcionalidad**: Cada historia representa una función específica del sistema

- Dar alta mobiliario = funcionalidad completa
- Realizar reserva = funcionalidad completa
- Pagar con tarjeta = funcionalidad completa

### ✅ **Responde las 3 preguntas clave**:

- **¿Quién se beneficia?** → Rol claramente identificado
- **¿Qué se quiere?** → Acción específica en el título
- **¿Cuál es el beneficio?** → Propósito claro en el "para"
