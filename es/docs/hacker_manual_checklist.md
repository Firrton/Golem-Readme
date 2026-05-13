# Checklist del Hackers Manual — Golem Community Builder Programme

> Versión pragmática para un programa que recién arranca. Lista solo lo **fundamental** para que el manual sea sólido en su etapa inicial, marcando qué está cubierto hoy y qué conviene sumar.

## Convención

- ✅ **Cubierto** — está en el manual de forma clara
- 🟡 **Parcial** — se menciona pero le falta detalle o queda pendiente de definir
- ❌ **Falta** — no está y conviene agregarlo
- ⊘ **N/A** — no aplica al formato del programa

Las referencias entre paréntesis apuntan al archivo donde está cubierto cada item.

---

## 1. Fundamentos del programa

- [✅] Misión y propósito explícitos (README.md → "Introducción", "Por qué existe")
- [✅] Diferencia con hackathon clásico explicada (README.md → "Introducción")
- [✅] Audiencia objetivo definida en 3 perfiles (README.md → "A quién está dirigido")
- [✅] Identidad visual mínima (logo, banner, badges en README.md)
- [✅] Contexto de Golem Network para no iniciados (README.md → "Sobre Golem Network")

---

## 2. Elegibilidad

- [✅] Perfiles aceptados (Web3 con/sin Golem, Web2) en README.md
- [✅] No requiere experiencia previa con Golem (README.md → "A quién está dirigido")
- [✅] Equipos permitidos sin tope de tamaño (FAQ.md)
- [✅] Participación múltiple aclarada (FAQ.md)
- [🟡] Restricciones geográficas no mencionadas — agregar línea si hay alguna, o aclarar "abierto globalmente"

---

## 3. Formato y duración

- [✅] Programa continuo y abierto, sin deadline central (README.md → "Introducción")
- [✅] Duración por proyecto: 2–4 semanas (README.md → "Desarrollo")
- [✅] Proceso de 5 etapas visualizado (README.md → "Proceso de participación")
- [🟡] Tiempo de respuesta al pitch ("a la brevedad" en FAQ, conviene un SLA aproximado, ej: <7 días)

---

## 4. Tracks

- [✅] Cinco tracks descritos con foco claro (guia_builders.md)
- [✅] Criterios de éxito por track (guia_builders.md)
- [✅] Open track con validación previa (Track E)
- [✅] Ejemplo de referencia previa al programa (gScribe en README.md)
- [🟡] Ejemplos de proyectos completados — se completará a medida que existan

---

## 5. Stack técnico y onboarding

- [✅] SDKs y versiones mínimas listadas (guia_builders.md → "Stack vigente")
- [✅] Redes disponibles: testnet hoodi y mainnet con diferencias (guia_builders.md)
- [✅] Faucet y fondos de prueba mencionados
- [✅] Repos oficiales y docs linkeados (README.md → "Recursos oficiales")
- [🟡] Quickstart "hello world" propio del programa — hoy se delega a docs oficiales, podría sumar un repo plantilla mínimo

---

## 6. Formación de equipos

- [✅] Equipos sin límite de tamaño (FAQ.md)
- [✅] Un punto de contacto oficial por equipo (FAQ.md)
- [✅] Split interno del bounty queda en el equipo (FAQ.md)
- [⊘] Cofounder matching formal — overkill para esta etapa, Discord alcanza

---

## 7. Mentoría y soporte

- [✅] Equipo de Golem disponible durante el desarrollo (README.md, FAQ.md)
- [✅] Canal único: Discord oficial (README.md → "Contacto")
- [🟡] Expectativa de tiempo de respuesta no documentada — sugerir cadencia o SLA básico
- [🟡] Reglas de lo que el equipo Golem hace/no hace (revisa código, no lo escribe) — útil para evitar fricción

---

## 8. IP y licencias

- [✅] Builder mantiene la propiedad del código (FAQ.md)
- [✅] Licencia open source requerida (guia_builders.md)
- [✅] Golem puede difundir el proyecto (FAQ.md, README.md → "Co-promoción")
- [✅] Reuso del proyecto por el builder permitido (FAQ.md)

---

## 9. Criterios de evaluación

- [✅] Criterios de éxito declarados por track (guia_builders.md)
- [🟡] Sin rúbrica numérica explícita — para un programa de aprobación binaria (sí/no/ajustar) puede ser suficiente, conviene listar 3-5 criterios transversales (calidad técnica, reproducibilidad, claridad del write-up) que el equipo usa al revisar
- [✅] Tres resultados posibles del review: aprobado, ajustar alcance, rechazado con justificación (README.md)

---

## 10. Entregables y submission

- [✅] Repo público en GitHub requerido (guia_builders.md → "Entregables")
- [✅] README con secciones mínimas definidas (guia_builders.md → "Entregables")
- [✅] Métricas reales de ejecución sobre Golem (guia_builders.md, README.md)
- [✅] Write-up para Discord (guia_builders.md → "Entregables")
- [✅] Wallet para el pago en submission (guia_builders.md)
- [✅] Vídeo demo (2–3 min) requerido para amplificación — definido en [guia_builders.md](../docs/guia_builders.md)
- [🟡] Plantilla de README pre-armada — opcional pero baja fricción

---

## 11. Pitch

- [✅] Aplicación a través del formulario Tally (https://forms.golem.network/golem-builders-programme)
- [✅] Campos mínimos definidos (track, descripción, alcance, plan, entregables)
- [✅] Formulario de aplicación activo: https://forms.golem.network/golem-builders-programme
- [⊘] Pitch en video / demo day — el programa no usa formato pitch público, no aplica

---

## 12. Premio y pago

- [✅] Monto claro: 500 USD en $GLM por proyecto (README.md, badge)
- [✅] Forma de pago: $GLM a la wallet del builder (README.md → "Entrega y pago")
- [🟡] Plazo de pago post-validación — no especificado, conviene una línea (ej: "dentro de X días tras la aprobación de la entrega")
- [🟡] Tipo de cambio: momento del cálculo del equivalente USD↔GLM no aclarado

---

## 13. Comunicación y comunidad

- [✅] Discord como canal único oficial (README.md, FAQ.md)
- [✅] Recursos oficiales (docs, repos, token) listados (README.md)
- [🟡] Cadencia de comunicación durante el proyecto — esperada "proactiva" pero sin frecuencia sugerida

---

## 14. Manejo de excepciones

- [✅] Política de abandono explicada (FAQ.md)
- [✅] Cambios de alcance: requieren reaprobación (FAQ.md)
- [✅] Modificaciones técnicas razonables durante el desarrollo permitidas (FAQ.md)

---

## 15. Conducta y plagio

- [❌] Código de conducta — falta documento corto, alcanza con 1 página linkeada desde README
- [❌] Política sobre código preexistente y forks — aclarar si se permite partir de un fork o si tiene que ser nuevo
- [❌] Política sobre uso de IA generativa para el código — explicitar si se permite, requiere disclosure, etc.

---

## 16. Post-entrega

- [✅] Co-promoción en canales oficiales y comunidades partner (README.md, FAQ.md)
- [✅] El builder puede reutilizar el proyecto en su portfolio (FAQ.md)
- [🟡] Reentry / segundo proyecto del mismo builder — política implícita pero conviene una línea explícita

---

## Resumen rápido

| Estado | Cantidad | Lectura |
|--------|----------|---------|
| ✅ Cubierto | ~40 | Lo operativo del programa está bien |
| 🟡 Parcial | ~14 | Detalles que conviene precisar antes de escalar tracción |
| ❌ Falta | 3 | Código de conducta + política de IA + política de código preexistente |
| ⊘ N/A | 2 | Cofounder matching formal y pitch en video |

**Lo mínimo a sumar antes de promover el programa más fuerte:**

1. **Código de conducta** corto (1 página) linkeado desde README y FAQ.
2. **Política sobre uso de IA generativa** y **código preexistente / forks** — 2 párrafos en FAQ.
3. **SLA aproximado de respuesta a la aplicación** (ej: <7 días hábiles).
4. **Plazo de pago tras la aprobación** (ej: <X días en $GLM).

El resto (rúbrica numérica, quickstart propio, plantilla de README, mentoría estructurada) son mejoras incrementales que tienen sentido cuando el programa crezca, no ahora.

---

**Versión:** 2.0 (simplificada) · **Última actualización:** 2026-05-11
