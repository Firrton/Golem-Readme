<div align="center">

<img src="../assets/golem-logo-tagline.png" alt="Golem Network — Create. Compute. Earn." width="520" />

<br /><br />

# Golem Community Builder Programme

**Construir sobre compute descentralizado. Recibir bounties en $GLM.**

<br />

[![Bounty](https://img.shields.io/badge/Bounty-500%20USD%20en%20%24GLM-0F1FE3?style=for-the-badge)](#proceso-de-participación)
[![Status](https://img.shields.io/badge/Status-Open%20%26%20Ongoing-22C55E?style=for-the-badge)](#)
[![License](https://img.shields.io/badge/License-Open%20Source-1E40AF?style=for-the-badge)](#)
[![Discord](https://img.shields.io/badge/Discord-Golem%20Community-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/golem)

<br />

[**Builders Guide**](./docs/guia_builders.md) ·
[**Pitch Template**](./docs/pitch_template.md) ·
[**Submission Guide**](./docs/submission-guide.md) ·
[**FAQ**](./FAQ.md)

</div>

---

## Introducción

El **Golem Community Builder Programme** es una iniciativa abierta y continua dirigida a desarrolladores que deseen construir proyectos funcionales sobre Golem Network, la red descentralizada de compute open-source operativa desde 2016.

A diferencia de un hackathon tradicional, el programa no opera bajo presión de fechas límite ni mediante competencias de pitch. Su objetivo es financiar trabajo técnico genuino que demuestre, de manera concreta, las capacidades del protocolo: proyectos que vivan en GitHub, generen conversación en la comunidad y contribuyan al ecosistema de compute descentralizado.

> Cada proyecto aprobado recibe un bounty de **500 USD pagados en $GLM**, con una duración estimada de entre dos y cuatro semanas de desarrollo.

---

## Sobre Golem Network

Golem Network es un marketplace descentralizado de recursos computacionales. Los desarrolladores pueden alquilar capacidad de cómputo proveniente de máquinas reales distribuidas en toda la red, pagar por su uso en $GLM y ejecutar tareas paralelizables a una escala que sería impráctica sobre una sola máquina: transcodificación de video, inferencia de modelos de machine learning, simulaciones científicas, procesamiento masivo de datos, entre otros casos de uso.

La propuesta técnica es directa: si una tarea toma diez minutos en una máquina, Golem permite distribuirla a través de cien providers y completarla en una fracción del tiempo. La red es permissionless, lo que significa que cualquier persona puede consumir compute como requestor o aportar capacidad como provider, sin intermediarios ni autorizaciones previas.

#### Recursos oficiales

| Recurso | Enlace |
|---------|--------|
| Documentación técnica | [docs.golem.network](https://docs.golem.network) |
| Repositorios oficiales | [github.com/golemfactory](https://github.com/golemfactory) |
| Información del token $GLM | [golem.network/glm](https://golem.network/glm) |
| Comunidad Discord | [discord.gg/golem](https://discord.gg/golem) |

---

## Por qué existe este programa

Golem es un protocolo maduro con un caso técnico sólido, pero buena parte de su potencial sigue sin estar adecuadamente documentado a través de proyectos concretos. La forma más efectiva de mostrar lo que el protocolo hace no es mediante material de marketing, sino mediante código funcional construido por desarrolladores reales, con repositorios públicos, métricas reproducibles y explicaciones claras.

Este programa existe para acortar esa distancia. Financia builders que estén dispuestos a explorar el protocolo en profundidad y a publicar el resultado de manera transparente, generando recursos que tanto la comunidad de Golem como nuevos desarrolladores podrán utilizar como referencia.

---

## A quién está dirigido

El programa está abierto a tres perfiles principales:

#### 🛠️ Builders de Web3 con experiencia previa en Golem
Personas que ya conocen el protocolo y desean construir un proyecto más ambicioso con respaldo financiero y soporte directo del equipo.

#### 🌐 Builders de Web3 sin experiencia en Golem
Desarrolladores activos en el ecosistema de Ethereum u otras redes descentralizadas que estén explorando compute descentralizado por primera vez. Para este perfil, el programa funciona también como onboarding pago al protocolo.

#### 💻 Builders de Web2
Desarrolladores con experiencia en backend, sistemas distribuidos, machine learning, procesamiento de medios u otros dominios técnicos relevantes que quieran experimentar con un primer proyecto sobre infraestructura descentralizada.

> No se requiere experiencia previa con Golem. Se requiere capacidad técnica para construir, voluntad de documentar el trabajo y disposición para publicar el resultado en abierto.

---

## Qué construyen los participantes

El programa propone cinco tracks orientados a diferentes tipos de demostraciones técnicas. Los tracks no son rígidos: funcionan como puntos de partida y como referencia para quienes prefieren un marco definido. Quienes tengan una idea propia pueden proponerla a través del Track E, sujeta a aprobación previa por parte del equipo.

<div align="center">

| Track | Foco principal |
|:-----:|:---------------|
| **A** · [Parallel Media Processing](./docs/guia_builders.md#track-a) | Procesamiento paralelo de archivos de audio y video sobre múltiples providers |
| **B** · [Compute-Intensive Simulation](./docs/guia_builders.md#track-b) | Simulaciones numéricas, Monte Carlo y cálculos científicos a escala |
| **C** · [Provider Reputation & Benchmarking](./docs/guia_builders.md#track-c) | Herramientas de medición, scoring y benchmarking de providers |
| **D** · [Chess Engine / Game AI at Scale](./docs/guia_builders.md#track-d) | Inteligencia artificial de juegos como demostración legible de paralelismo |
| **E** · [Open Track](./docs/guia_builders.md#track-e) | Propuesta libre del builder, validada antes del inicio |

</div>

La descripción completa de cada track, incluyendo direcciones técnicas sugeridas, ejemplos de proyectos previos y entregables esperados, se encuentra en el [**Builders Guide**](./docs/guia_builders.md).

---

## Proceso de participación

El programa opera bajo un flujo de cinco etapas diseñado para minimizar fricción tanto para el builder como para el equipo de Golem.

```
  ┌───────────┐    ┌──────────┐    ┌──────────┐    ┌─────────────┐    ┌──────────────┐
  │  1. Read  │ →  │ 2. Pitch │ →  │ 3. Review│ →  │  4. Build   │ →  │  5. Deliver  │
  │   Guide   │    │  Submit  │    │ Approval │    │  & Iterate  │    │   & Get Paid │
  └───────────┘    └──────────┘    └──────────┘    └─────────────┘    └──────────────┘
```

### 1. Lectura del Builders Guide

El primer paso consiste en revisar el [Builders Guide](./docs/guia_builders.md). Esta lectura permite identificar el track adecuado y calibrar el alcance del proyecto.

### 2. Envío del pitch

El builder presenta su propuesta a través del **formulario oficial de pitch**: *[pendiente]*.

La propuesta debe seguir la estructura de la [plantilla de pitch](./docs/pitch_template.md) e incluir, como mínimo: track elegido, descripción del proyecto, alcance técnico, plan de trabajo, entregables y experiencia previa relevante. Una página suele ser suficiente.

### 3. Revisión y aprobación

El equipo de Golem revisa cada pitch internamente y responde con una de tres posibilidades: aprobación directa, solicitud de ajustes en el alcance, o rechazo con justificación.

Una vez aprobado el pitch, se confirma formalmente el alcance del proyecto, los entregables y el bounty asociado.

### 4. Desarrollo

El builder desarrolla el proyecto en su propio repositorio público de GitHub. Durante esta etapa, el equipo de Golem está disponible en Discord para resolver dudas técnicas, revisar avances y orientar sobre el uso del protocolo. El plazo típico de desarrollo es de **dos a cuatro semanas**, ajustable según la complejidad acordada en el pitch.

### 5. Entrega y pago

Al finalizar el desarrollo, el builder entrega su proyecto siguiendo el [submission guide](./docs/submission-guide.md). La entrega incluye el repositorio público con README claro, métricas reales de ejecución sobre Golem y un breve write-up explicativo orientado a la comunidad. Una vez validado el entregable, el bounty se transfiere directamente a la wallet del builder en **$GLM**.

---

## Qué aporta Golem y qué se espera del builder

El programa funciona como una colaboración estructurada con compromisos claros por ambas partes.

<table>
<tr>
<th width="50%">🟦 Lo que aporta Golem Network</th>
<th width="50%">🟨 Lo que se espera del builder</th>
</tr>
<tr>
<td valign="top">

- Financiamiento por proyecto sin cuotas ni límites de participación
- Acceso directo al equipo técnico para consultas, revisiones y debugging
- Co-promoción del proyecto finalizado a través de canales oficiales y comunidades partner
- Flexibilidad de alcance para favorecer la calidad técnica por encima del cumplimiento mecánico de un track

</td>
<td valign="top">

- Compromiso real con la entrega del proyecto en el alcance acordado
- Código publicado en GitHub bajo licencia abierta con documentación clara
- Comunicación proactiva durante el desarrollo, especialmente si surgen bloqueos o ajustes
- Write-up final que permita a otros desarrolladores entender y reproducir el trabajo

</td>
</tr>
</table>

---

## Recursos del repositorio

| Documento | Propósito |
|-----------|-----------|
| [📘 Builders Guide](./docs/guia_builders.md) | Descripción completa de los cinco tracks, ejemplos y entregables |
| [📝 Pitch Template](./docs/pitch_template.md) | Plantilla recomendada para estructurar el pitch |
| [📦 Submission Guide](./docs/submission-guide.md) | Requisitos formales para la entrega del proyecto |
| [❓ FAQ](./FAQ.md) | Preguntas frecuentes sobre el programa |

> 🇬🇧 **English version:** [`/en/README.md`](../en/README.md) · 🇧🇷 **Versão em português:** [`/pt/README.md`](../pt/README.md)

---

## Proyectos anteriores

A medida que se completen proyectos dentro del programa, esta sección se actualizará con enlaces a los repositorios y descripciones de cada uno.

Como referencia previa al programa, [**gScribe**](https://gscribe.ai/) es un ejemplo de proyecto construido sobre Golem que demuestra el caso de uso de transcripción paralela de audio mediante Whisper distribuido entre múltiples providers.

---

## Comunidades partner

El programa se desarrolla en colaboración con comunidades de builders en América Latina y otras regiones. Las comunidades partner ayudan a difundir el programa entre sus desarrolladores, y cada proyecto finalizado por un builder de su comunidad recibe co-promoción en sus canales.

> *Comunidades actualmente involucradas: por confirmar.*

---

## Contacto

Para consultas sobre el programa antes de enviar un pitch, el canal recomendado es el Discord oficial de Golem en el canal de builders:

<div align="center">

[![Join Discord](https://img.shields.io/badge/Join%20the%20Builders%20Channel-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/golem)

</div>

---

<div align="center">

<img src="../assets/golem-logo.png" alt="Golem" width="60" />

**Powered by $GLM · Built for Ethereum · Open to everyone**

<sub>© Golem Network · Community Builder Programme</sub>

</div>
