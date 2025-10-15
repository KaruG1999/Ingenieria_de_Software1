# Diagramas de Transición de Estados (DTE)

## ¿Qué son?

Los DTE permiten **modelar el comportamiento del sistema en función del tiempo**. Son especialmente útiles para:
- Sistemas de tiempo real
- Modelado de procesos
- Sistemas de control

---

## Elementos Fundamentales

### 1. Estado
- Identifica un **período de tiempo NO instantáneo**
- Representa cuando el sistema está esperando u operando
- **Nomenclatura**: Verbos en gerundio (ej: *Configurando*, *Esperando*, *Procesando*)

### 2. Transición
Relaciona estados con una única dirección. Tiene 3 componentes:

#### a) **Evento** (obligatorio)
- Suceso que provoca el cambio de estado
- **Forma impersonal** (ej: *"Se presionó tecla"*)
- NO es un verbo en infinitivo

#### b) **Condición** (opcional)
- Impide el cambio de estado aunque ocurra el evento
- Es una condición lógica evaluable
- Ejemplo: `[temperatura > 0]`

#### c) **Acción** (opcional)
- Tareas instantáneas durante la transición
- **Verbo en infinitivo** desde la perspectiva del sistema
- Ejemplo: *"habilitar teclado"*, *"incrementar contador"*

**Formato**: `Evento [Condición] / Acción`

### 3. Estados Especiales
- **Estado Inicial**: ÚNICO (círculo negro)
- **Estado Final**: VARIOS posibles (círculo con borde doble)

---

## ⚠️ ASPECTOS CRÍTICOS A TENER EN CUENTA

### 1. Perspectiva del Sistema
> **IMPORTANTE**: El modelado se realiza desde el punto de vista del **SISTEMA**, NO del usuario.

- ❌ Incorrecto: "Presionar botón" (acción del usuario)
- ✅ Correcto: "Se presionó botón" (evento para el sistema)

### 2. Lenguaje Natural
- Escribir en lenguaje natural, NO en código
- ❌ Incorrecto: `intentos++` o `i++`
- ✅ Correcto: *"incrementar contador de intentos"*

### 3. Condiciones Mutuamente Excluyentes
> **Cuando un evento se comparte entre múltiples transiciones, las condiciones deben garantizar que A LO SUMO UNA se active**

Ejemplo:
```
Se presiona botón <+> [temperatura < 300] / incrementar temperatura
Se presiona botón <+> [temperatura es 300] / emitir pitido de error
```

### 4. Consistencia del Sistema
Las acciones deben ser coherentes a lo largo del diagrama:
- Si `acciones1` incluye *"habilitar teclado numérico"*
- Entonces `acciones3` debe incluir *"deshabilitar teclado numérico"*

---

## Convenciones de Nomenclatura

| Elemento | Formato | Ejemplo |
|----------|---------|---------|
| **Estados** | Verbo en gerundio | Configurando, Esperando, Funcionando |
| **Eventos** | Forma impersonal | Se presionó tecla, Transcurre un segundo |
| **Condiciones** | Expresión lógica | [temperatura > 0], [cantidad dígitos < 3] |
| **Acciones** | Verbo infinitivo (sistema) | habilitar teclado, incrementar contador |

---

## Ejemplo Práctico: Microondas

### Estados principales:
1. **Configurando Tiempo** → Usuario ingresa 4 dígitos
2. **Configurando Temperatura** → Ajuste entre 0-300°C
3. **Funcionando** → Cuenta regresiva y operación

### Transición clave:
```
Estado: Configurando Tiempo
Evento: Se presiona dígito
Condición: [cantidad dígitos < 3]
Acción: incrementar cantidad de dígitos, actualizar contador, mostrar en display
Próximo Estado: Configurando Tiempo (mismo estado)
```

### Validaciones importantes:
```
Se presiona botón <inicio> [temperatura > 0 y puerta cerrada] / iniciar funcionamiento
Se presiona botón <inicio> [temperatura es 0 o puerta abierta] / emitir pitido de error
```

---

## ✅ Checklist para una Buena Planificación

- [ ] ¿Todos los estados están nombrados con verbos en gerundio?
- [ ] ¿Los eventos están en forma impersonal (no son acciones del usuario)?
- [ ] ¿Las acciones están escritas desde la perspectiva del sistema?
- [ ] ¿Las transiciones con el mismo evento tienen condiciones mutuamente excluyentes?
- [ ] ¿El sistema es consistente (habilitar/deshabilitar, abrir/cerrar)?
- [ ] ¿Se modelaron todas las situaciones de error/operación inválida?
- [ ] ¿Está definido el comportamiento del botón de apagado desde todos los estados?
- [ ] ¿Las acciones están en lenguaje natural (no en código)?
- [ ] ¿Existe UN SOLO estado inicial?
- [ ] ¿Se consideraron los eventos temporales (ej: "Transcurre un segundo")?

---

## Errores Comunes a Evitar

1. **Confundir acciones del usuario con eventos del sistema**
2. **Usar sintaxis de programación en lugar de lenguaje natural**
3. **No considerar condiciones mutuamente excluyentes**
4. **Olvidar la consistencia en habilitar/deshabilitar componentes**
5. **No modelar situaciones de error o casos límite**
6. **Usar nombres de estados que no sean verbos en gerundio**

---

## Recordatorio Final

> El DTE debe ser **claro, completo y consistente**. Cada transición debe estar justificada y cada estado debe tener al menos una forma de salida (excepto estados finales).


#### Apunte de clase 

- Apagado no se modeliza como estado 
- Evaluar limites -> el sistema debe reaccionar "avisa" 