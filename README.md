# Golem Community Builder Programme

**Construir sobre compute descentralizado. Recibir bounties en $GLM.**

---

## Introducción

El **Golem Community Builder Programme** es una iniciativa abierta y continua dirigida a desarrolladores que deseen construir proyectos funcionales sobre Golem Network, la red descentralizada de compute open-source operativa desde 2016.

A diferencia de un hackathon tradicional, el programa no opera bajo presión de fechas límite ni mediante competencias de pitch. Su objetivo es financiar trabajo técnico genuino que demuestre, de manera concreta, las capacidades del protocolo: proyectos que vivan en GitHub, generen conversación en la comunidad y contribuyan al ecosistema de compute descentralizado.

Cada proyecto aprobado recibe un bounty de **500 USD pagados en $GLM**, con una duración estimada de entre dos y cuatro semanas de desarrollo.

---

## Sobre Golem Network

Golem Network es un marketplace descentralizado de recursos computacionales. Los desarrolladores pueden alquilar capacidad de cómputo proveniente de máquinas reales distribuidas en toda la red, pagar por su uso en $GLM y ejecutar tareas paralelizables a una escala que sería impráctica sobre una sola máquina: transcodificación de video, inferencia de modelos de machine learning, simulaciones científicas, procesamiento masivo de datos, entre otros casos de uso.

La propuesta técnica es directa: si una tarea toma diez minutos en una máquina, Golem permite distribuirla a través de cien providers y completarla en una fracción del tiempo. La red es permissionless, lo que significa que cualquier persona puede consumir compute como requestor o aportar capacidad como provider, sin intermediarios ni autorizaciones previas.

Recursos oficiales:

- **Documentación:** [docs.golem.network](https://docs.golem.network)
- **Repositorios:** [github.com/golemfactory](https://github.com/golemfactory)
- **Información del token $GLM:** [golem.network/glm](https://golem.network/glm)
- **Comunidad en Discord:** [discord.gg/golem](https://discord.gg/golem)

---

## Por qué existe este programa

Golem es un protocolo maduro con un caso técnico sólido, pero buena parte de su potencial sigue sin estar adecuadamente documentado a través de proyectos concretos. La forma más efectiva de mostrar lo que el protocolo hace no es mediante material de marketing, sino mediante código funcional construido por desarrolladores reales, con repositorios públicos, métricas reproducibles y explicaciones claras.

Este programa existe para acortar esa distancia. Financia builders que estén dispuestos a explorar el protocolo en profundidad y a publicar el resultado de manera transparente, generando recursos que tanto la comunidad de Golem como nuevos desarrolladores podrán utilizar como referencia.

---

## A quién está dirigido

El programa está abierto a tres perfiles principales.

**Builders de Web3 con experiencia previa en Golem.** Personas que ya conocen el protocolo y desean construir un proyecto más ambicioso con respaldo financiero y soporte directo del equipo.

**Builders de Web3 sin experiencia en Golem.** Desarrolladores activos en el ecosistema de Ethereum u otras redes descentralizadas que estén explorando compute descentralizado por primera vez. Para este perfil, el programa funciona también como onboarding pago al protocolo.

**Builders de Web2.** Desarrolladores con experiencia en backend, sistemas distribuidos, machine learning, procesamiento de medios u otros dominios técnicos relevantes que quieran experimentar con un primer proyecto sobre infraestructura descentralizada.

No se requiere experiencia previa con Golem. Se requiere capacidad técnica para construir, voluntad de documentar el trabajo y disposición para publicar el resultado en abierto.

---

## Qué construyen los participantes

El programa propone cinco tracks orientados a diferentes tipos de demostraciones técnicas. Los tracks no son rígidos: funcionan como puntos de partida y como referencia para quienes prefieren un marco definido. Quienes tengan una idea propia pueden proponerla a través del Track E, sujeta a aprobación previa por parte del equipo.

| Track | Foco principal |
|-------|---------------|
| **A — [Parallel Media Processing](./docs/guia_builders.md#track-a)** | Procesamiento paralelo de archivos de audio y video sobre múltiples providers |
| **B — [Compute-Intensive Simulation](./docs/guia_builders.md#track-b)** | Simulaciones numéricas, Monte Carlo y cálculos científicos a escala |
| **C — [Provider Reputation & Benchmarking](./docs/guia_builders.md#track-c)** | Herramientas de medición, scoring y benchmarking de providers |
| **D — [Chess Engine / Game AI at Scale](./docs/guia_builders.md#track-d)** | Inteligencia artificial de juegos como demostración legible de paralelismo |
| **E — [Open Track](./docs/guia_builders.md#track-e)** | Propuesta libre del builder, validada antes del inicio |

La descripción completa de cada track, incluyendo direcciones técnicas sugeridas, ejemplos de proyectos previos y entregables esperados, se encuentra en el [Builders Guide](./docs/guia_builders).

---

## Proceso de participación

El programa opera bajo un flujo de cinco etapas diseñado para minimizar fricción tanto para el builder como para el equipo de Golem.

### 1. Lectura del Builders Guide

El primer paso consiste en revisar el [Builders Guide](./docs/builders-guide.md). Esta lectura permite identificar el track adecuado y calibrar el alcance del proyecto

### 2. Envío del pitch

El builder presenta su propuesta a través del **formulario oficial de pitch**: [pendiente].

La propuesta debe seguir la estructura de la [plantilla de pitch](./docs/pitch-template.md) e incluir, como mínimo: track elegido, descripción del proyecto, alcance técnico, plan de trabajo, entregables y experiencia previa relevante. Una página suele ser suficiente.

### 3. Revisión y aprobación

El equipo de Golem revisa cada pitch internamente y responde con una de tres posibilidades: aprobación directa, solicitud de ajustes en el alcance, o rechazo con justificación. Los criterios completos de evaluación se detallan en el documento de [approval criteria](./docs/approval-criteria.md).

Una vez aprobado el pitch, se confirma formalmente el alcance del proyecto, los entregables y el bounty asociado. <!-- PLACEHOLDER: tiempo estimado de respuesta -->

### 4. Desarrollo

El builder desarrolla el proyecto en su propio repositorio público de GitHub. Durante esta etapa, el equipo de Golem está disponible en Discord para resolver dudas técnicas, revisar avances y orientar sobre el uso del protocolo. El plazo típico de desarrollo es de dos a cuatro semanas, ajustable según la complejidad acordada en el pitch.

### 5. Entrega y pago

Al finalizar el desarrollo, el builder entrega su proyecto siguiendo el [submission guide](./docs/submission-guide.md). La entrega incluye el repositorio público con README claro, métricas reales de ejecución sobre Golem y un breve write-up explicativo orientado a la comunidad. Una vez validado el entregable, el bounty se transfiere directamente a la wallet del builder en $GLM.

---

## Qué aporta Golem y qué se espera del builder

El programa funciona como una colaboración estructurada con compromisos claros por ambas partes.

**Lo que aporta Golem Network:**

Financiamiento por proyecto sin cuotas ni límites de participación, acceso directo al equipo técnico para consultas, revisiones y debugging, co-promoción del proyecto finalizado a través de los canales oficiales de Golem y de las comunidades partner, y flexibilidad de alcance para favorecer la calidad técnica por encima del cumplimiento mecánico de un track.

**Lo que se espera del builder:**

Compromiso real con la entrega del proyecto en el alcance acordado, código publicado en GitHub bajo licencia abierta con documentación clara, comunicación proactiva durante el desarrollo (especialmente si surgen bloqueos o ajustes de alcance), y un write-up final que permita a otros desarrolladores entender el trabajo realizado y reproducirlo.

---

## Recursos del repositorio

| Documento | Propósito |
|-----------|-----------|
| [Builders Guide](./docs/builders-guide.md) | Descripción completa de los cinco tracks, ejemplos y entregables |
| [Pitch Template](./docs/pitch-template.md) | Plantilla recomendada para estructurar el pitch |
| [Approval Criteria](./docs/approval-criteria.md) | Criterios que utiliza el equipo de Golem para evaluar cada propuesta |
| [Getting Started](./docs/getting-started.md) | Guía técnica de configuración inicial sobre Golem |
| [Submission Guide](./docs/submission-guide.md) | Requisitos formales para la entrega del proyecto |
| [FAQ](./FAQ.md) | Preguntas frecuentes sobre el programa |
| [Rules](./RULES.md) | Términos, condiciones y elegibilidad |

---

## Proyectos anteriores

A medida que se completen proyectos dentro del programa, esta sección se actualizará con enlaces a los repositorios y descripciones de cada uno.

Como referencia previa al programa, [gScribe](https://gscribe.ai/) es un ejemplo de proyecto construido sobre Golem que demuestra el caso de uso de transcripción paralela de audio mediante Whisper distribuido entre múltiples providers.

---

## Comunidades partner

El programa se desarrolla en colaboración con comunidades de builders en América Latina y otras regiones. Las comunidades partner ayudan a difundir el programa entre sus desarrolladores, y cada proyecto finalizado por un builder de su comunidad recibe co-promoción en sus canales.

Comunidades actualmente involucradas: <!-- PLACEHOLDER: confirmar y agregar logos cuando estén disponibles -->
-
-
-

---

## Contacto

Para consultas sobre el programa antes de enviar un pitch, el canal recomendado es el Discord oficial de Golem en el canal de builders: [discord.gg/golem](https://discord.gg/golem).

---

*Powered by $GLM · Built for Ethereum · Open to everyone*