# Redes de Petri - Resumen

## ¿Qué es una Red de Petri?

Una **Red de Petri** es una herramienta de modelado que permite representar sistemas dinámicos y concurrentes mediante grafos dirigidos con eventos discretos.

---

## Componentes Principales

### 1. **Sitio (Place)** ⭕
- Representa un **estado o condición** del sistema
- Se dibuja como un **círculo**
- Puede contener tokens (marcas)

### 2. **Transición** ▭
- Representa un **evento o acción**
- Se dibuja como un **rectángulo o barra**
- Modela el cambio de un estado a otro

### 3. **Arco** →
- **Relaciona sitios con transiciones** o viceversa
- Es **unidireccional** (indicado con flecha)
- ⚠️ **NUNCA** conecta sitio con sitio ni transición con transición

### 4. **Token (Marca)** ●
- Puntos negros que se colocan **dentro de los sitios**
- **Función:** habilitar o deshabilitar transiciones
- Controlan la ejecución de la red

---

## Funcionamiento

### Transición Habilitada
Una transición está **habilitada** cuando:
- Hay **al menos UN token** por cada arco que llega a ella

**Ejemplo:**
```
● → [T] ✓ Habilitada (1 token entrante)
●● → [T] ✓ Habilitada (2 tokens entrantes)
  → [T] ✗ Deshabilitada (0 tokens)
```

### Propagación de Tokens
Cuando una transición se dispara:
1. **Instante i:** Absorbe tantos tokens como arcos de entrada tenga
2. **Instante i+Δ:** Produce tantos tokens como arcos de salida tenga

**Ejemplos:**
- 1 token entra → 1 token sale
- 1 token entra → 2 tokens salen
- 2 tokens entran → 1 token sale

---

## Convenciones Importantes

### 🟢 Convención de Inicio
- **Transición fuente** (sin entradas): genera cantidad ilimitada de tokens
- Puede haber más de una en la red

### 🔴 Convención de Fin
- **Transición final** (sin salidas): elimina tokens de la red
- Puede haber más de una

### ⚠️ Regla de No Bloqueo
- **Toda transición debe tener oportunidad de ser habilitada alguna vez**
- No crear transiciones que nunca puedan ejecutarse

### 📝 Nombres Obligatorios
- Todos los estados y transiciones deben tener **nombres distintos**
- Transiciones pueden nombrase según:
  - La etapa que **termina**
  - La etapa que **comienza**

---

## Tips para Armar Soluciones

### ✅ Modelar Colas
```
[Llega] → (Esperando) → [Comienza Proceso]
```

### ✅ Modelar Recursos Limitados
Usar un sitio con tokens para representar disponibilidad:
```
(Cobrador libre: ●) → [Comienza Inscripción]
                    ← [Finaliza Inscripción]
```
- El token representa que el recurso está disponible
- Se consume al usarse y se devuelve al liberarse

### ✅ Sincronización (N elementos simultáneos)
Usar **múltiples arcos** hacia una transición:
```
(Jugador 1: ●)  ↘
                [Comienza Partido]
(Jugador 2: ●)  ↗
```
- Necesita 2 tokens para habilitarse
- Modela que 2 jugadores deben estar presentes

### ✅ Alternativas (OR)
Usar **múltiples transiciones** desde un mismo sitio:
```
              → [Opción A]
(Estado: ●) ↗
              → [Opción B]
```

---

## Errores Comunes a Evitar

❌ **NO conectar sitio con sitio directamente**
```
(A) → (B)  ✗ INCORRECTO
(A) → [T] → (B)  ✓ CORRECTO
```

❌ **NO olvidar devolver recursos**
```
(Recurso: ●) → [Usa] → ... ← [Libera] → (Recurso)
                                          ↑ IMPORTANTE
```

❌ **NO crear transiciones que nunca se habiliten**
```
(Vacío) → [T] → ...  ✗ Nunca se ejecutará
```

❌ **NO confundir cantidad de arcos con peso**
- Si necesitas 2 tokens, usa **2 arcos separados**
- No hay "arcos con peso" en el modelo básico

---

## Caso Práctico: Campeonato de Tenis

### Problema Resumido
1. Jugadores llegan y esperan en fila
2. Un cobrador atiende de a uno
3. Esperan oponente (necesitan 2 para jugar)
4. Juegan en una de 2 canchas disponibles
5. Van al vestuario y se retiran

### Solución Paso a Paso

#### Paso 1: Llegada de jugadores
```
[Llega jugador] → (Jugador esperando para pagar)
    ↑ Transición fuente
```

#### Paso 2: Cobrador (recurso único)
```
(Cobrador libre: ●) ──┐
                      ↓
(Esperando) → [Comienza Inscripción] → (Abonando)
              ↓
[Finaliza Inscripción] → (Esperando oponente)
              ↓
          (Cobrador libre: ●) Devuelve el recurso
```

#### Paso 3: Sincronización de 2 jugadores
```
(Esperando oponente: ●●) 
         ↓↓
    [Comienza partido]
```
Usa **2 arcos** para requerir 2 jugadores simultáneos

#### Paso 4: Canchas (2 recursos)
```
(Cancha 1 libre: ●) → [Comienza partido 1] → (Jugando en cancha 1)
(Cancha 2 libre: ●) → [Comienza partido 2] → (Jugando en cancha 2)
```

#### Paso 5: Finalización
```
[Finaliza partido] → (Utilizando vestuario) → [Se retira del club]
                     ↑ 2 jugadores salen    ↑ Transición final
```

---

## Variante: Modelar Parejas vs Individuos

### Opción A: Modelar individuos (2 arcos)
```
[Comienza partido] ⇉ (Jugando en cancha)
                      2 tokens = 2 jugadores
```

### Opción B: Modelar pareja (1 arco)
```
[Comienza partido] → (Jugando en cancha)
                      1 token = 1 pareja
```

⚠️ **IMPORTANTE:** Al modelar como pareja, al retirarse del vestuario deben separarse (usar 2 arcos de salida)

---

## Checklist Final

Antes de entregar tu solución, verifica:

- [ ] Todos los sitios y transiciones tienen nombres distintos
- [ ] Los arcos solo conectan sitios con transiciones (nunca sitio-sitio)
- [ ] Hay transición fuente para generar tokens iniciales
- [ ] Hay transición final para consumir tokens
- [ ] Los recursos limitados tienen tokens que representan disponibilidad
- [ ] Los recursos se devuelven después de usarse
- [ ] Las sincronizaciones usan múltiples arcos correctamente
- [ ] Todas las transiciones pueden habilitarse en algún momento
- [ ] La red modela correctamente el flujo del problema

---

## Resumen en Una Frase

> **Las Redes de Petri modelan sistemas mediante sitios (estados), transiciones (eventos) y tokens (que habilitan transiciones), permitiendo representar concurrencia, sincronización y recursos compartidos.**