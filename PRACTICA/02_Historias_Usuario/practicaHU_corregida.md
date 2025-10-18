# Historias de Usuario - Versión Corregida según Criterios Docente

## Criterios y Sugerencias de la Profesora

**Checklist aplicado para mejorar las historias de usuario:**

- **Dado:** debe contener valores de verdad concretos (ej: nombre, DNI, email, usuario registrado, materia seleccionada).
- **Cuando:** describe la acción que realiza el usuario en el sistema.
- **Entonces:** no debe expresar verificaciones lógicas, sino **lo que el sistema muestra, genera o hace visible**.
- Siempre que se **almacene información** (registro, inscripción, listado), debe quedar explícito en el escenario.
- El diseño debe minimizar los errores del cliente → pensar escenarios con posibles equivocaciones y mensajes claros.
- Generalizar el rol cuando aplique (ej: "usuario del sistema" en lugar de separar docente/jefe si la acción es común).
- Si hay **registro y autenticación**, deben existir HU para:
  1.  Registro.
  2.  Inicio de sesión.
  3.  Cierre de sesión.

---

## Problema 1: Alquiler de mobiliario

### Roles identificados:

- **Encargado de mobiliario** -> Usuario de carga
- **Cliente**

---

#### Historia 1: Autenticación

**ID:** Iniciar sesión

**TÍTULO:** Como usuario de carga quiero autenticarme en el sistema para administrar el alta de mobiliario.

**REGLAS DE NEGOCIO:**

- Solo los usuarios de carga habilitados pueden acceder a funcionidad de alta de mobiliario

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Inicio de sesión exitoso
**Dado** que el encargado está registrado y su usuario y contraseña pertenecen a un usuario habilitado
**Cuando** ingresa email "encargqgmail.com", contraseña "abc123" confirma el inicio de sesión,
**Entonces** el sistema muestra en pantalla el panel de alta de mobiliario.

**Escenario 2:** Inicio de sesión fallido por correo invalido
**Dado** que el encargado está registrado pero ingresa un email que no pertenece a un usuario habilitado y contraseña,
**Cuando** ingresa email "luis@gmail.com", contraseña "abc123" y confirma el inico de sesion,
**Entonces** el sistema muestra el mensaje "Inicio de sesion fallido: email invalido".

#### Historia 2: Dar alta mobiliario

**ID:** Dar alta mobiliario

**TÍTULO:** Como encargado de mobiliario quiero dar de alta un mueble para incluirlo en el inventario disponible.

**REGLAS DE NEGOCIO:**

- No pueden existir códigos repetidos
- Para que el encargado pueda dar de alta el mobiliario debe autenticarse en el sistema

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Alta exitosa de mobiliario
**Dado** que el encargado está autenticado y el código "MOB001" no existe,
**Cuando** ingresa código "MOB001", tipo "Silla", fecha creación "01/01/2024", fecha último mantenimiento "15/01/2024", estado "libre", precio "$50" y confirma el alta,
**Entonces** el sistema registra el mueble en el inventario y muestra el mensaje "Mueble registrado exitosamente".

**Escenario 2:** Alta fallida por código repetido
**Dado** que el encargado está autenticado y el código "MOB001" ya existe en el inventario,
**Cuando** intenta dar de alta un mueble con código "MOB001", tipo "Mesa", fecha creación "02/01/2024", fecha último mantenimiento "16/01/2024", estado "libre" y precio "$100",
**Entonces** el sistema muestra el mensaje "El código de inventario ya existe".

---

#### Historia 3: Realizar reserva de alquiler

**ID:** Realizar reserva alquiler

**TÍTULO:** Como cliente quiero realizar una reserva de alquiler para asegurar mobiliario para mi evento.

**REGLAS DE NEGOCIO:**

- Por una política comercial de la marca una reserva tiene que incluir como mínimo 3 muebles
- Para realizar una reserva se debe abonar el 20% del total del alquiler

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Reserva exitosa
**Dado** que hay mobiliario disponible y las condiciones de pago son válidas,
**Cuando** el cliente selecciona 5 muebles (3 sillas a $50 cada una, 2 mesas a $100 cada una), ingresa fecha "15/03/2024", lugar "Salón Central", cantidad de días "2" y procede al pago del 20% ($70),
**Entonces** el sistema almacena la reserva, procesa el pago, emite número de reserva único "R123456" y muestra el mensaje "Reserva confirmada. Su número de reserva es R123456".

**Escenario 2:** Reserva fallida por cantidad insuficiente de muebles
**Dado** que el cliente desea alquilar solo 2 muebles y las condiciones depago son válidas,
**Cuando** selecciona 2 muebles (2 sillas a $50 cada una), ingresa fecha "15/03/2024", lugar "Salón Central", cantidad de días "2" e intenta realizar la reserva,
**Entonces** el sistema muestra el mensaje "Debe seleccionar al menos 3 muebles para realizar la reserva".

**Escenario 3:** Reserva fallida por error en pago
**Dado** que el hay mobiliario disponible pero las condiciones de pago no son exitosas,
**Cuando** ingresa los datos requeridos correctamente e intenta realizar el pago del 20% con una tarjeta sin fondos suficientes,
**Entonces** el sistema muestra el mensaje "Error en el procesamiento del pago. Verifique los datos de su tarjeta".

---

#### Historia 4: Pagar con tarjeta de crédito

**ID:** Pagar tarjeta

**TÍTULO:** Como cliente quiero pagar con tarjeta de crédito para completar mi reserva.

**REGLAS DE NEGOCIO:**

- El pago de la reserva se realiza únicamente con tarjeta de crédito validando número de tarjeta y fondos a través de un servicio del banco

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Pago exitoso
**Dado** que la tarjeta "1234-5678-9012-3456" es válida y tiene fondos suficientes según el servicio del banco,
**Cuando** el cliente ingresa número de tarjeta "1234-5678-9012-3456", código "123", vencimiento "12/25" y confirma el pago de $70,
**Entonces** el sistema valida con el banco, procesa el pago exitosamente y muestra el mensaje "Pago procesado correctamente".

**Escenario 2:** Pago fallido por tarjeta inválida
**Dado** que la tarjeta "0000-0000-0000-0000" no es válida según el servicio del banco,
**Cuando** el cliente ingresa esos datos y confirma el pago,
**Entonces** el sistema muestra el mensaje "Número de tarjeta inválido".

**Escenario 3:** Pago fallido por fondos insuficientes
**Dado** que la tarjeta "1234-5678-9012-3456" es válida pero no tiene fondos suficientes según el servicio del banco,
**Cuando** el cliente intenta realizar el pago de $70,
**Entonces** el sistema muestra el mensaje "Fondos insuficientes en la tarjeta".

**Escenario 4:** Pago fallido por fallo conexión con el servidor externo del banco
**Dada** la conexión con el servidor del banco fallida,
**Cuando** el cliente intenta realizar el pago ingresando los datos y presiona "pagar"
**Entonces** el sistema retorna el mensaje "Error por conexión con servidor".

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
**Dado** que la fecha actual es "01/01/2024", la fecha de ingreso "15/03/2024" está dentro de 90 días y la estadía es de 10 días,
**Cuando** ingresa fecha ingreso "15/03/2024", fecha egreso "25/03/2024", hotel "Plaza Central", cantidad personas "2" y confirma la reserva,
**Entonces** el sistema almacena la reserva, genera código de reserva "HOTEL789" y envía correo electrónico con el código y enlace de pago.

**Escenario 2:** Reserva fallida por fecha fuera de rango
**Dado** que la fecha actual es "01/01/2024" y la fecha de ingreso "15/06/2024" está a más de 90 días,
**Cuando** intenta hacer la reserva con esa fecha,
**Entonces** el sistema muestra el mensaje "La fecha de ingreso debe estar dentro de los 90 días".

**Escenario 3:** Reserva fallida por estadía excesiva
**Dado** que ingresa fecha ingreso "15/03/2024" y fecha egreso "05/04/2024" (estadía de 21 días),
**Cuando** intenta reservar,
**Entonces** el sistema muestra el mensaje "Las estadías no pueden durar más de 15 días".

---

#### Historia 2: Realizar check in

**ID:** Realizar check in

**TÍTULO:** Como usuario quiero hacer check in para acceder a mi habitación.

**REGLAS DE NEGOCIO:**

- Los check in pueden realizarse después de las 10 am y hasta las 23:59 pm

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Check in exitoso
**Dado** que son las 14:00 pm, la fecha actual es "15/03/2024" y el código "HOTEL789" tiene reserva vigente para esta fecha,
**Cuando** ingresa el código "HOTEL789" en la terminal,
**Entonces** el sistema muestra "Habitación asignada: 205", envía mensaje al conserje para guiar al usuario y mensaje a botones para las valijas.

**Escenario 2:** Check in fallido por código inválido
**Dado** que la fecha actual es "15/03/2024" y el código "HOTEL999" no tiene reserva para esta fecha,
**Cuando** ingresa el código "HOTEL999" en la terminal,
**Entonces** el sistema muestra "Código de reserva no válido para la fecha actual".

**Escenario 3:** Check in fallido por horario no permitido
**Dado** que son las 8:00 am (antes de las 10:00 am) y el código "HOTEL789" es válido,
**Cuando** intenta realizar check in,
**Entonces** el sistema muestra "Aún no se encuentran habilitados los ingresos al hotel".

---

#### Historia 3: Realizar check out

**ID:** Realizar check out

**TÍTULO:** Como conserje quiero realizar el check out para liberar la habitación.

**REGLAS DE NEGOCIO:**

- Solo se puede realizar check out de habitaciones sin gastos

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Check out exitoso
**Dado** que la habitación "205" está ocupada y no tiene gastos pendientes,
**Cuando** el conserje ingresa número de habitación "205" y confirma check out,
**Entonces** el sistema libera la habitación y envía mensaje a las mucamas "La habitación 205 puede limpiarse".

**Escenario 2:** Check out fallido por gastos pendientes
**Dado** que la habitación "205" está ocupada y tiene gastos sin abonar por $150,
**Cuando** el conserje intenta hacer check out,
**Entonces** el sistema muestra "No puede realizarse check out hasta que se abonen los gastos pendientes".

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
**Dado** que la persona tiene 25 años, nombre "Carlos López", apellido "González" y el mail "carlos@email.com" no existe en el sistema,
**Cuando** completa el registro con esos datos,
**Entonces** el sistema almacena los datos, genera contraseña "abc123" y la envía al email "carlos@email.com".

**Escenario 2:** Registro rechazado por menor de edad
**Dado** que la persona tiene 17 años, nombre "Ana Pérez" y mail "ana@email.com",
**Cuando** intenta registrarse,
**Entonces** el sistema muestra en pantalla el texto de la ley que impide la venta de bebidas alcohólicas a menores.

**Escenario 3:** Registro rechazado por mail existente
**Dado** que el mail "carlos@email.com" ya está registrado en el sistema,
**Cuando** la persona intenta registrarse con nombre "Pedro Martín", edad 30 años y mail "carlos@email.com",
**Entonces** el sistema muestra el mensaje "El email ya se encuentra registrado".

---

#### Historia 2: Iniciar sesión

**ID:** Iniciar sesión

**TÍTULO:** Como usuario registrado quiero iniciar sesión para acceder a la compra de bebidas.

**REGLAS DE NEGOCIO:**

- El inicio de sesión se realiza con email (usuario) y contraseña

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Inicio de sesión exitoso
**Dado** que el usuario "carlos@email.com" está registrado con contraseña "abc123",
**Cuando** ingresa email "carlos@email.com", contraseña "abc123" y presiona "Iniciar sesión",
**Entonces** el sistema valida las credenciales y muestra la pantalla principal con el catálogo de bebidas.

**Escenario 2:** Inicio de sesión fallido por credenciales incorrectas
**Dado** que el usuario "carlos@email.com" está registrado con contraseña "abc123",
**Cuando** ingresa email "carlos@email.com", contraseña "xyz999" y presiona "Iniciar sesión",
**Entonces** el sistema muestra "Credenciales inválidas. Intente nuevamente".

---

#### Historia 3: Comprar bebidas

**ID:** Comprar bebidas

**TÍTULO:** Como usuario quiero comprar bebidas para adquirir productos alcohólicos.

**REGLAS DE NEGOCIO:**

- Si el usuario es premium se le hace un descuento del 20%
- Si el usuario seleccionó productos por un monto superior a los $4500 se le hace un 10% de descuento
- Si el usuario es premium y compra por un monto superior a $4500 se deben aplicar ambos descuentos

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Compra exitosa usuario regular sin descuento
**Dado** que el usuario "carlos@email.com" está logueado, no es premium y selecciona productos por $3000,
**Cuando** finaliza la selección y confirma la compra,
**Entonces** el sistema muestra "Total a pagar: $3000" sin aplicar descuentos.

**Escenario 2:** Compra con descuento por monto superior a $4500
**Dado** que el usuario "carlos@email.com" no es premium y selecciona productos por $5000,
**Cuando** finaliza la compra,
**Entonces** el sistema aplica descuento del 10% y muestra "Total con descuento: $4500".

**Escenario 3:** Compra usuario premium con ambos descuentos
**Dado** que el usuario "premium@email.com" es premium y selecciona productos por $5000,
**Cuando** finaliza la compra,
**Entonces** el sistema aplica descuento del 20% por ser premium más 10% por monto superior a $4500 y muestra "Total con descuentos aplicados: $3600".

---

#### Historia 4: Cerrar sesión

**ID:** Cerrar sesión

**TÍTULO:** Como usuario quiero cerrar sesión para finalizar mi acceso de forma segura.

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Cierre de sesión exitoso
**Dado** que el usuario "carlos@email.com" tiene una sesión activa,
**Cuando** selecciona la opción "Cerrar sesión",
**Entonces** el sistema finaliza la sesión y muestra "Sesión cerrada correctamente".

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
**Dado** que el alumno presenta DNI "42.123.456" válido y nombre "María González",
**Cuando** la bibliotecaria procesa la asociación con esos datos,
**Entonces** el sistema registra al alumno, genera número de socio "S001" y muestra "Carnet otorgado. Número de socio: S001".

---

#### Historia 2: Realizar préstamo

**ID:** Realizar préstamo

**TÍTULO:** Como bibliotecaria quiero realizar préstamos para que los socios puedan llevarse libros.

**REGLAS DE NEGOCIO:**

- Los préstamos se realizan exclusivamente a socios habilitados, que no posean más de tres préstamos vigentes y no tengan préstamos vencidos
- La bibliotecaria presta libros que se encuentren en buen estado

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Préstamo exitoso
**Dado** que el socio "S001" está habilitado, tiene 2 préstamos vigentes, no tiene préstamos vencidos y el libro "Cuentos Infantiles" está en buen estado,
**Cuando** la bibliotecaria registra el préstamo del libro al socio "S001",
**Entonces** el sistema almacena el préstamo con fecha de vencimiento y muestra "Préstamo registrado exitosamente".

**Escenario 2:** Préstamo rechazado por límite de préstamos
**Dado** que el socio "S002" ya tiene 3 préstamos vigentes,
**Cuando** la bibliotecaria intenta registrar un nuevo préstamo,
**Entonces** el sistema muestra "El socio ha alcanzado el límite máximo de préstamos".

**Escenario 3:** Préstamo rechazado por préstamos vencidos
**Dado** que el socio "S003" tiene un préstamo vencido desde "15/02/2024",
**Cuando** la bibliotecaria intenta registrar un préstamo,
**Entonces** el sistema muestra "El socio tiene préstamos vencidos pendientes".

**Escenario 4:** Préstamo rechazado por libro deteriorado
**Dado** que el libro "Manual Escolar" se encuentra en estado deteriorado,
**Cuando** la bibliotecaria intenta prestarlo,
**Entonces** el sistema muestra "El libro no está disponible por encontrarse deteriorado".

---

#### Historia 3: Devolver libro

**ID:** Devolver libro

**TÍTULO:** Como bibliotecaria quiero procesar devoluciones para actualizar el estado de los préstamos.

**REGLAS DE NEGOCIO:**

- Cuando el socio retorna un libro se verifica si el préstamo se encuentra vencido. En este caso, la bibliotecaria suspende al socio, que por 15 días no podrá solicitar nuevos préstamos

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Devolución en tiempo
**Dado** que el préstamo del socio "S001" vence el "20/03/2024" y la fecha actual es "18/03/2024",
**Cuando** el socio devuelve el libro "Cuentos Infantiles",
**Entonces** el sistema registra la devolución y muestra "Devolución registrada exitosamente".

**Escenario 2:** Devolución con vencimiento
**Dado** que el préstamo del socio "S004" venció el "10/03/2024" y la fecha actual es "15/03/2024",
**Cuando** la bibliotecaria procesa la devolución del libro,
**Entonces** el sistema registra la devolución, suspende al socio por 15 días hasta "30/03/2024" y muestra "Socio suspendido hasta el 30/03/2024 por devolución tardía".

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
**Dado** que el empleado CUIL "20-42123456-7" tiene 6 meses de antigüedad y no tiene licencia vigente,
**Cuando** ingresa CUIL "20-42123456-7", tipo "presencial", fecha de inicio "15/03/2024", matrícula médico "MP12345", diagnóstico "gripe" y destinatario "titular",
**Entonces** el sistema almacena la licencia, genera código "LIC001" y envía email con confirmación de la licencia y 5 días otorgados.

**Escenario 2:** Solicitud rechazada por antigüedad insuficiente
**Dado** que el empleado CUIL "20-38765432-1" tiene 3 semanas de antigüedad (menos de 1 mes),
**Cuando** intenta solicitar una licencia,
**Entonces** el sistema muestra "Licencia rechazada. Debe tener más de 1 mes de antigüedad".

**Escenario 3:** Solicitud rechazada por licencia vigente
**Dado** que el empleado CUIL "20-42123456-7" tiene una licencia vigente hasta "20/03/2024",
**Cuando** intenta solicitar una nueva licencia,
**Entonces** el sistema muestra "No puede solicitar una licencia teniendo una vigente".

---

#### Historia 2: Consultar licencias

**ID:** Consultar licencias

**TÍTULO:** Como administrativo quiero consultar licencias solicitadas para realizar seguimiento.

**REGLAS DE NEGOCIO:**

- Por una cuestión de costos se podrá imprimir un informe por mes para cada empleado

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Consulta exitosa
**Dado** que no se imprimió informe este mes para el empleado CUIL "20-42123456-7",
**Cuando** el administrativo ingresa CUIL "20-42123456-7" y rango de fechas "01/03/2024" a "31/03/2024",
**Entonces** el sistema imprime informe con las licencias solicitadas en ese período y registra la impresión.

**Escenario 2:** Consulta rechazada por límite mensual
**Dado** que ya se imprimió un informe este mes para el empleado CUIL "20-42123456-7",
**Cuando** el administrativo intenta imprimir otro informe para el mismo empleado,
**Entonces** el sistema muestra "Ya se imprimió el informe mensual para este empleado".

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
**Dado** que la fecha actual es "15/03/2024", el código de pago "123456789" tiene 1er vencimiento "20/03/2024", 2do vencimiento "30/03/2024" y monto original "$500",
**Cuando** el empleado ingresa el código "123456789",
**Entonces** el sistema se conecta con la central, recupera los datos de la factura y muestra "Monto a cobrar: $500".

**Escenario 2:** Pago con recargo por primer vencimiento
**Dado** que la fecha actual es "25/03/2024", el código "987654321" tiene 1er vencimiento "20/03/2024", 2do vencimiento "30/03/2024", monto "$500" y recargo "$50",
**Cuando** el empleado procesa el pago,
**Entonces** el sistema aplica el recargo y muestra "Monto a cobrar con recargo: $550".

**Escenario 3:** Pago rechazado por segundo vencimiento
**Dado** que la fecha actual es "05/04/2024", el código "111222333" tiene 2do vencimiento "30/03/2024" vencido,
**Cuando** el empleado intenta procesar el pago,
**Entonces** el sistema muestra "La factura no se puede cobrar por segundo vencimiento vencido".

---

#### Historia 2: Registrar pagos del día

**ID:** Registrar pagos día

**TÍTULO:** Como gerente quiero registrar en la central los pagos del día para mantener actualizada la información.

**REGLAS DE NEGOCIO:**

- No deben enviarse dos veces las transacciones

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** que la clave maestra "MASTER123" es correcta y no se enviaron los pagos del día "15/03/2024",
**Cuando** el gerente ingresa la clave e inicia el envío de pagos,
**Entonces** el sistema se conecta a la central, envía las transacciones y muestra "Pagos registrados exitosamente" después de recibir confirmación.

**Escenario 2:** Registro rechazado por envío duplicado
**Dado** que ya se enviaron los pagos del día "15/03/2024" a la central,
**Cuando** el gerente intenta enviar nuevamente,
**Entonces** el sistema muestra "Los pagos del día ya fueron enviados".

---

#### Historia 3: Ver estadísticas

**ID:** Ver estadísticas

**TÍTULO:** Como gerente quiero ver estadísticas de cobros para analizar el rendimiento.

**REGLAS DE NEGOCIO:**

- Requiere clave maestra

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Estadísticas generadas exitosamente
**Dado** que la clave maestra "MASTER123" es correcta,
**Cuando** el gerente ingresa la clave y el rango de fechas "01/03/2024" a "31/03/2024",
**Entonces** el sistema muestra las estadísticas con montos y cantidad de cobros agrupados por empresa: "Empresa A: $15.000 (25 cobros), Empresa B: $8.500 (12 cobros)".

**Escenario 2:** Estadísticas rechazadas por clave incorrecta
**Dado** que la clave maestra ingresada "WRONG123" es incorrecta,
**Cuando** el gerente intenta acceder a las estadísticas,
**Entonces** el sistema muestra "Clave maestra incorrecta".

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
**Dado** que el usuario registrado tiene patente "ABC123" sin deudas, DNI del vendedor "42.123.456" (mayor de 18 años) y DNI del comprador "38.765.432" (mayor de 18 años),
**Cuando** ingresa patente "ABC123", DNI del vendedor "42.123.456" y DNI del comprador "38.765.432",
**Entonces** el sistema valida las condiciones, almacena el trámite y envía al email del comprador código "TRANS001" para realizar el pago.

**Escenario 2:** Trámite rechazado por deudas
**Dado** que la patente "DEF456" tiene deudas pendientes por $1500,
**Cuando** el usuario intenta iniciar el trámite con esa patente,
**Entonces** el sistema muestra "La patente tiene deudas pendientes".

**Escenario 3:** Trámite rechazado por menor de edad
**Dado** que el DNI del comprador "12.345.678" corresponde a un menor de 18 años,
**Cuando** intenta iniciar la transferencia,
**Entonces** el sistema muestra "El comprador y el vendedor deben ser mayores de edad".

---

#### Historia 2: Consultar estado de transferencia

**ID:** Consultar estado

**TÍTULO:** Como usuario quiero consultar el estado de una transferencia para conocer el progreso.

**REGLAS DE NEGOCIO:**

- Se pueden hacer hasta tres consultas por mes

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Consulta exitosa
**Dado** que el usuario registrado tiene menos de 3 consultas este mes y la patente "ABC123" tiene transferencia en curso con estado "En proceso de pago",
**Cuando** ingresa la patente "ABC123",
**Entonces** el sistema muestra "Estado de transferencia ABC123: En proceso de pago" y registra la consulta.

**Escenario 2:** Consulta rechazada por límite alcanzado
**Dado** que el usuario ya realizó 3 consultas este mes,
**Cuando** intenta consultar el estado de una transferencia,
**Entonces** el sistema muestra "Ha alcanzado el límite mensual de 3 consultas".

---

## Problema 8: Concursos

### Roles identificados:

- **Docente**
- **Jefe del área de concursos**

---

#### Historia 1: Registrar docente

**ID:** Registrar docente

**TÍTULO:** Como docente quiero poder inscribirme en el sistema para concursar por un puesto en mi cátedra correspondiente.

**REGLAS DE NEGOCIO:**

- El mail es único y utilizado como nombre de usuario
- El sistema debe enviar automáticamente la contraseña generada al correo registrado
- Solo pueden registrarse docentes con DNI mayor a 12 millones y menor a 55 millones

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Registro exitoso
**Dado** el DNI "42.652.123" dentro del límite permitido, el nombre "Juan Pérez" y el email "juanperez@email.com" no registrado previamente,
**Cuando** el docente ingresa los datos y presiona "Registrarse",
**Entonces** el sistema almacena los datos, envía al email la contraseña asignada y muestra el mensaje "Se registró correctamente. Ingrese con su nombre de usuario (email) y contraseña".

**Escenario 2:** Registro fallido por email repetido
**Dado** que el email "juanperez@email.com" ya está registrado en el sistema,
**Cuando** el docente ingresa el nombre "Juan Pérez", DNI "42.652.123" y el mismo email,
**Entonces** el sistema muestra el mensaje "El email ya se encuentra registrado".

**Escenario 3:** Registro fallido por DNI fuera de rango
**Dado** el DNI "65.562.123" fuera del rango permitido,
**Cuando** el docente ingresa el nombre "Juan Pérez", DNI "65.562.123" y el email "juanperez@email.com",
**Entonces** el sistema muestra el mensaje "El DNI ingresado está fuera del rango permitido".

---

#### Historia 2: Inscribir docente a concurso

**ID:** Inscribir docente a concurso

**TÍTULO:** Como docente quiero inscribirme al concurso para poder ejercer en un puesto este cuatrimestre.

**REGLAS DE NEGOCIO:**

- Un docente no podrá inscribirse a más de 3 concursos
- El sistema debe emitir un comprobante de inscripción detallado

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Inscripción exitosa
**Dado** que el docente Juan Pérez, DNI "42.652.123" ya está registrado y tiene 2 materias seleccionadas,
**Cuando** confirma su inscripción a "Matemática 0" y "Matemática 1" presionando "Inscribirse",
**Entonces** el sistema almacena la inscripción, muestra el mensaje "Inscripción exitosa" e imprime un comprobante con el detalle de las materias seleccionadas.

**Escenario 2:** Inscripción fallida por exceso de materias
**Dado** que el docente Juan Pérez desea inscribirse a "Matemática 0", "Matemática 1", "Matemática 3" y "Matemática 4",
**Cuando** selecciona las 4 materias y presiona "Inscribirse",
**Entonces** el sistema muestra el mensaje "Se excede el número máximo de materias permitidas (3)".

---

#### Historia 3: Imprimir listado de docentes inscriptos a determinada materia

**ID:** Imprimir listado de docentes inscriptos a determinada materia

**TÍTULO:** Como jefe del área de concursos, quiero imprimir un listado de inscriptos en una materia para enviarlo al secretario administrativo, de manera que se cumpla con la ordenanza 123/19 de la UNLP.

**REGLAS DE NEGOCIO:**

- El listado debe poder ser impreso y elevado siguiendo el circuito administrativo de la ordenanza 123/19 (jefe de concursos → secretario administrativo → decano)

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Generación exitosa del listado
**Dado** que el jefe del área de concursos, usuario "jefe01", ha iniciado sesión correctamente,
**Cuando** selecciona la materia "Matemática 1" con docentes inscriptos y solicita generar el listado,
**Entonces** el sistema genera y muestra el listado con los inscriptos en la materia y habilita su impresión.

**Escenario 2:** Materia sin inscriptos
**Dado** que el jefe del área de concursos selecciona la materia "Matemática 2", que no tiene inscriptos,
**Cuando** solicita generar el listado,
**Entonces** el sistema muestra el mensaje "No hay inscriptos registrados en esta materia" y no genera el listado.

---

#### Historia 4: Iniciar sesión

**ID:** Iniciar sesión docente/jefe

**TÍTULO:** Como usuario del sistema (docente o jefe de área de concursos), quiero poder iniciar sesión para acceder a las funcionalidades disponibles según mi rol.

**REGLAS DE NEGOCIO:**

- El inicio de sesión se realiza con email (usuario) y contraseña
- Cada rol (docente o jefe de concursos) tiene permisos específicos
- Un usuario no podrá acceder a ninguna funcionalidad sin haber iniciado sesión previamente

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Inicio de sesión exitoso
**Dado** que el usuario "juanperez@email.com" está registrado con la contraseña "abc123",
**Cuando** ingresa esos datos y presiona "Iniciar sesión",
**Entonces** el sistema valida las credenciales y muestra la pantalla principal con las opciones correspondientes a su rol.

**Escenario 2:** Inicio de sesión fallido por contraseña incorrecta
**Dado** que el usuario "juanperez@email.com" está registrado con la contraseña "abc123",
**Cuando** ingresa el email correcto pero la contraseña "xyz999" y presiona "Iniciar sesión",
**Entonces** el sistema muestra el mensaje "Credenciales inválidas. Intente nuevamente".

**Escenario 3:** Inicio de sesión fallido por usuario no registrado
**Dado** que no existe el usuario "docenteX@email.com" en el sistema,
**Cuando** ingresa ese email con cualquier contraseña y presiona "Iniciar sesión",
**Entonces** el sistema muestra el mensaje "El usuario no se encuentra registrado".

---

#### Historia 5: Cerrar sesión

**ID:** Cerrar sesión usuario

**TÍTULO:** Como usuario del sistema (docente o jefe de área de concursos), quiero poder cerrar sesión para finalizar mi acceso y proteger mis datos.

**REGLAS DE NEGOCIO:**

- El cierre de sesión finaliza la sesión activa del usuario
- Una vez cerrada la sesión, no se puede acceder a funcionalidades sin volver a iniciar sesión

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Cierre de sesión exitoso
**Dado** que el usuario "jefe01" inició sesión previamente,
**Cuando** selecciona la opción "Cerrar sesión",
**Entonces** el sistema finaliza la sesión y muestra el mensaje "Sesión finalizada correctamente".

**Escenario 2:** Intento de acceder sin sesión activa
**Dado** que un usuario no tiene ninguna sesión activa,
**Cuando** intenta acceder a la pantalla de inscripción a concursos,
**Entonces** el sistema redirige a la pantalla de inicio de sesión y muestra el mensaje "Debe iniciar sesión para continuar".

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
**Dado** que el DNI "42.123.456" corresponde a un cliente del banco y el crédito solicitado es de "$300.000" (no supera $400.000),
**Cuando** completa DNI "42.123.456", nombre "Juan Pérez", apellido "García", email "juan@email.com", tipo de crédito "personal" y monto "$300.000",
**Entonces** el sistema almacena el trámite para análisis del área económica e imprime comprobante número "CRED001".

**Escenario 2:** Rechazo por no ser cliente
**Dado** que el DNI "38.765.432" no corresponde a un cliente del banco,
**Cuando** intenta iniciar trámite con ese DNI y email "nuevo@email.com",
**Entonces** el sistema envía correo electrónico a "nuevo@email.com" con instructivo para hacerse cliente.

**Escenario 3:** Rechazo por monto excesivo
**Dado** que el DNI "42.123.456" es cliente del banco pero solicita crédito por "$500.000" (supera $400.000),
**Cuando** intenta iniciar el trámite con ese monto,
**Entonces** el sistema muestra "El monto solicitado excede el límite permitido".

---

#### Historia 2: Consultar estado de trámite

**ID:** Consultar estado

**TÍTULO:** Como cliente quiero consultar el estado de mi trámite para conocer su progreso.

**REGLAS DE NEGOCIO:**

- Si el cliente ingresa tres veces un código inexistente el sistema bloquea la ip del cliente por 24 horas

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Consulta exitosa
**Dado** que el número de comprobante "CRED001" existe y tiene estado "En análisis",
**Cuando** el cliente ingresa el número "CRED001",
**Entonces** el sistema muestra informe "Estado del trámite CRED001: En análisis por área económica".

**Escenario 2:** Consulta fallida por comprobante inexistente
**Dado** que el número de comprobante "CRED999" no existe en el sistema,
**Cuando** el cliente ingresa "CRED999",
**Entonces** el sistema muestra "Trámite inexistente" y registra el intento fallido.

**Escenario 3:** Bloqueo por consultas inválidas
**Dado** que el cliente desde IP "192.168.1.100" ya ingresó tres códigos inexistentes ("CRED999", "CRED888", "CRED777"),
**Cuando** intenta una cuarta consulta con código inexistente,
**Entonces** el sistema bloquea la IP por 24 horas y muestra "Usted ha excedido el número de consultas inválidas".

---

#### Historia 3: Listar créditos aprobados

**ID:** Listar créditos

**TÍTULO:** Como gerente quiero obtener listado de créditos aprobados para realizar seguimiento.

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Listado generado exitosamente
**Dado** que hay créditos aprobados entre "01/03/2024" y "31/03/2024",
**Cuando** el gerente ingresa fechas válidas "01/03/2024" a "31/03/2024",
**Entonces** el sistema muestra listado "Créditos aprobados: CRED001 - Juan Pérez - $300.000, CRED005 - María López - $150.000".

**Escenario 2:** Listado vacío
**Dado** que no hay créditos aprobados entre "01/02/2024" y "28/02/2024",
**Cuando** el gerente solicita el listado para esas fechas,
**Entonces** el sistema muestra "No hay créditos aprobados en las fechas ingresadas".

**Escenario 3:** Listado rechazado por fechas inválidas
**Dado** que las fechas ingresadas "32/13/2024" a "40/15/2024" no son válidas,
**Cuando** el gerente solicita el listado,
**Entonces** el sistema muestra "Las fechas ingresadas no son válidas".

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
**Dado** que la persona tiene 25 años, nombre "Diego Fernández", apellido "Torres", mail "diego@email.com" único y domicilio "Calle 50 N°123",
**Cuando** completa el registro con esos datos,
**Entonces** el sistema almacena los datos, genera contraseña "tennis456" y la envía al correo "diego@email.com".

**Escenario 2:** Registro rechazado por menor de edad
**Dado** que la persona tiene 17 años, nombre "Sofia Ruiz" y mail "sofia@email.com",
**Cuando** intenta registrarse,
**Entonces** el sistema muestra "Debe ser mayor de 18 años para registrarse".

---

#### Historia 2: Iniciar sesión

**ID:** Iniciar sesión usuario

**TÍTULO:** Como usuario registrado quiero iniciar sesión para solicitar turnos en canchas.

**REGLAS DE NEGOCIO:**

- Si un usuario falla tres veces al iniciar sesión su cuenta sea bloqueada

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Inicio de sesión exitoso
**Dado** que el usuario "diego@email.com" está registrado con contraseña "tennis456",
**Cuando** ingresa email "diego@email.com", contraseña "tennis456" y presiona "Iniciar sesión",
**Entonces** el sistema valida las credenciales y muestra la pantalla principal con las opciones de reserva.

**Escenario 2:** Inicio de sesión fallido
**Dado** que el usuario "diego@email.com" está registrado con contraseña "tennis456",
**Cuando** ingresa email "diego@email.com", contraseña "wrong123" y presiona "Iniciar sesión",
**Entonces** el sistema muestra "Credenciales inválidas" y registra el intento fallido.

**Escenario 3:** Cuenta bloqueada por fallos repetidos
**Dado** que el usuario "diego@email.com" ya falló tres veces consecutivas al iniciar sesión,
**Cuando** intenta iniciar sesión nuevamente,
**Entonces** el sistema muestra "Cuenta bloqueada por múltiples intentos fallidos" y no permite el acceso.

---

#### Historia 3: Solicitar turno

**ID:** Solicitar turno

**TÍTULO:** Como usuario quiero solicitar un turno para usar una cancha de tenis.

**REGLAS DE NEGOCIO:**

- El sistema no debe permitir dar turno con menos de 2 días a la fecha en que se solicita

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Turno asignado exitosamente
**Dado** que la fecha actual es "15/03/2024", la cancha "Cancha 1" está libre el "18/03/2024" a las "14:00" (más de 2 días de anticipación),
**Cuando** el usuario selecciona cancha "Cancha 1", fecha "18/03/2024" y hora "14:00",
**Entonces** el sistema asigna el turno y muestra "Su turno ha sido registrado con éxito".

**Escenario 2:** Turno rechazado por cancha ocupada
**Dado** que la cancha "Cancha 2" está ocupada el "20/03/2024" a las "16:00",
**Cuando** el usuario solicita ese turno,
**Entonces** el sistema muestra "Cancha ocupada, por favor seleccione otro día y horario" y permite seleccionar nuevamente.

**Escenario 3:** Turno rechazado por anticipación insuficiente
**Dado** que la fecha actual es "15/03/2024" y el usuario solicita turno para "16/03/2024" (menos de 2 días),
**Cuando** intenta solicitar el turno,
**Entonces** el sistema muestra "Debe solicitar el turno con al menos 2 días de anticipación".

---

#### Historia 4: Cerrar sesión

**ID:** Cerrar sesión usuario

**TÍTULO:** Como usuario quiero cerrar sesión para finalizar mi acceso de forma segura.

**CRITERIOS DE ACEPTACIÓN:**

**Escenario 1:** Cierre de sesión exitoso
**Dado** que el usuario "diego@email.com" tiene una sesión activa,
**Cuando** selecciona la opción "Cerrar sesión",
**Entonces** el sistema finaliza la sesión y muestra "Sesión cerrada correctamente".

**Escenario 2:** Intento de acceso sin sesión activa
**Dado** que el usuario no tiene sesión activa,
**Cuando** intenta acceder a la pantalla de solicitud de turnos,
**Entonces** el sistema redirige al login y muestra "Debe iniciar sesión para continuar".

---

## Resumen de mejoras aplicadas según criterios docente:

### ✅ **Valores concretos en "Dado":**

- DNI específicos: "42.123.456", "38.765.432"
- Nombres completos: "Juan Pérez", "María González"
- Emails únicos: "carlos@email.com", "diego@email.com"
- Fechas exactas: "15/03/2024", "20/03/2024"
- Montos específicos: "$500", "$300.000"
- Códigos de ejemplo: "MOB001", "HOTEL789", "CRED001"

### ✅ **"Entonces" observables:**

- Mensajes exactos mostrados al usuario
- Registros almacenados en el sistema
- Emails enviados con contenido específico
- Estados y códigos generados
- Acciones visibles del sistema

### ✅ **Almacenamiento explícito:**

- "el sistema almacena la reserva"
- "el sistema registra el mueble en el inventario"
- "el sistema almacena el trámite"
- "el sistema registra al alumno"

### ✅ **HU completas de autenticación:**

- Registro de usuario
- Inicio de sesión
- Cierre de sesión
- Manejo de bloqueos por intentos fallidos

### ✅ **Escenarios de error con mensajes específicos:**

- Códigos repetidos, fechas inválidas, fondos insuficientes
- Mensajes de error claros y accionables
- Validaciones de reglas de negocio explícitas

### ✅ **Reglas de negocio textuales:**

- Solo las mencionadas explícitamente en los enunciados
- No validaciones técnicas o de formato
- Enfoque en lógica de negocio funcional
