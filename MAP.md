# 🧭 MAP.md — Python Garden · Cyber Archives
## python04_cyber_archives — Safe I/O & Resilient Programs

Este documento es **MI mapa de aprendizaje y diseño**.  
Representa cómo evoluciona mi forma de pensar la interacción entre
un programa Python y el **mundo exterior**: archivos, streams y errores reales.

No es una lista de ejercicios.
Es una **arquitectura mental progresiva**, visual y defendible.

---

## 🌱 Idea central del módulo

Pasar de:

❌ “mi programa lee y escribe archivos”  
a  
✅ “mi programa interactúa con recursos externos de forma segura”

Principio clave:

👉 El mundo exterior es **inestable**  
👉 El programa debe **protegerse y seguir funcionando**

---

## 🧭 Mapa visual del módulo (ex0 → ex4)

Piensa el módulo como una **evolución controlada del contacto con el mundo exterior**.

---

## 🟢 ex0 — Ancient Text Recovery  
👉 Primer contacto con I/O + control manual

### Arquitectura
main()
├─ logs (print)
├─ read_ancient_text()
│ ├─ open()
│ ├─ readlines()
│ └─ finally → close()
├─ formateo de líneas
└─ cierre limpio


### Idea clave
ARCHIVO ──▶ leer ──▶ mostrar


### Aprendo
- `FileNotFoundError`
- `try / finally`
- Que el I/O puede fallar
- Que los recursos **siempre** deben cerrarse

---

## 🟡 ex1 — Archive Creation  
👉 Escritura segura + separación de datos

### Arquitectura
main()
├─ get_lines() ← datos puros
├─ preview (print)
├─ write_archive()
│ ├─ open("w")
│ ├─ write()
│ └─ finally → close()
└─ confirmación


### Idea clave
datos ──▶ escribir ──▶ archivo


### Aprendo
- Separar **qué se escribe** de **cómo se escribe**
- Control del output
- Gestión manual de recursos (todavía)

---

## 🔵 ex2 — Stream Management  
👉 Canales de comunicación (streams)

### Arquitectura
Usuario
│
▼
stdin (input)
│
▼
programa
│
├─ stdout → mensajes normales
└─ stderr → alertas / diagnósticos


### Idea clave
ENTRADA ≠ SALIDA ≠ ALERTA


### Aprendo
- Existen **tres flujos distintos**
- No todo es `print`
- Un programa serio **no mezcla mensajes**

---

## 🟣 ex3 — Vault Security  
👉 RAII real con `with`

### Arquitectura
main()
├─ read_classified() ← with open("r")
├─ format_line() ← lógica pura
├─ write_protocol() ← with open("w")
└─ logs de seguridad


### Idea clave
adquirir ──▶ usar ──▶ liberar (automático)


### Aprendo
- Context managers (`with`)
- Cierre automático incluso si algo falla
- Ya no dependo de `finally`

👉 **Esto es nivel profesional**

---

## 🔴 ex4 — Crisis Response  
👉 El mundo real: errores múltiples + sistema estable

### Arquitectura
main()
├─ crisis_handler("lost_archive.txt")
├─ crisis_handler("classified_vault.txt")
├─ crisis_handler("standard_archive.txt")
└─ cierre global


Dentro de `crisis_handler`:
try:
with open():
SUCCESS
except FileNotFoundError:
RESPONSE → not found
except PermissionError:
RESPONSE → access denied
except Exception:
RESPONSE → unexpected
finally:
STATUS → estable


### Idea clave
CRISIS ≠ CAÍDA DEL SISTEMA


### Aprendo
- Cada error tiene respuesta
- El sistema informa, limpia y continúa
- El programa **nunca se rompe**

---

## 🧠 Mapa global del módulo

    ┌──────────┐
    │  Mundo   │
    │ exterior │
    └────┬─────┘
         │
         ▼
  ┌───────────────┐
  │ ex0: leer      │  ← I/O básico
  └───────────────┘
         │
         ▼
  ┌───────────────┐
  │ ex1: escribir  │  ← output controlado
  └───────────────┘
         │
         ▼
  ┌───────────────┐
  │ ex2: streams   │  ← canales separados
  └───────────────┘
         │
         ▼
  ┌───────────────┐
  │ ex3: with      │  ← RAII / seguridad
  └───────────────┘
         │
         ▼
  ┌───────────────┐
  │ ex4: crisis    │  ← resiliencia real
  └───────────────┘

---

## 🎯 Objetivo final del módulo

Ser capaz de explicar con claridad:

- qué puede fallar al interactuar con el mundo exterior
- cómo se protege el programa
- cómo se liberan recursos
- cómo se comunican los errores
- por qué el sistema **sigue vivo pase lo que pase**

Este MAP representa **mi forma de diseñar programas robustos en Python**.
