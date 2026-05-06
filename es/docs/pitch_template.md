# Pitch Template

## Descripción de los campos

### 1. Información de contacto

El pitch debe abrir con la información básica que permita al equipo del programa identificar al builder y establecer comunicación durante el proceso de revisión y desarrollo.

Para builders individuales, los campos requeridos son nombre completo, dirección de correo electrónico, identificador de Discord y enlace al perfil de GitHub o portfolio profesional. La dirección de wallet no se solicita en el pitch, sino al momento de la entrega final del proyecto.

Para equipos, debe designarse un punto de contacto único responsable de la comunicación con el equipo del programa. El pitch debe listar también a los demás miembros del equipo con nombre completo, rol previsto en el proyecto y enlace a perfil profesional o GitHub. La distribución interna del bounty queda fuera del alcance del programa y debe acordarse internamente entre los miembros del equipo.

### 2. Track y título del proyecto

El builder debe indicar de manera explícita cuál de los cinco tracks corresponde a su propuesta: Track A (Parallel Media Processing), Track B (Compute-Intensive Simulation), Track C (Provider Reputation & Benchmarking), Track D (Chess Engine / Game AI at Scale) o Track E (Open Track). Esta clasificación facilita la evaluación interna y permite al equipo identificar rápidamente el contexto técnico de la propuesta.

El título tentativo del proyecto puede ajustarse durante el desarrollo, pero conviene proponer uno desde el pitch para facilitar la comunicación posterior.

### 3. Descripción del proyecto

Este campo es el corazón del pitch. En uno o dos párrafos, el builder debe explicar qué se construirá, qué problema o caso de uso aborda, y qué hace que el proyecto resulte interesante desde la perspectiva del compute descentralizado.

La descripción debe ser comprensible para un lector que conozca Golem pero no haya leído otra documentación previa sobre el proyecto. Debe responder con claridad a tres preguntas básicas: qué se va a construir, cómo se va a usar Golem dentro del proyecto, y qué tipo de demostración técnica produce el resultado final.

### 4. Alcance técnico

Esta sección detalla las decisiones técnicas concretas que el builder ha tomado al planificar el proyecto. Debe cubrir cuatro elementos.

El primero es el SDK que se utilizará: `@golem-sdk/task-executor` como camino principal recomendado para la mayoría de los proyectos, o `@golem-sdk/golem-js` 3.x cuando el proyecto requiera control fino sobre la lógica de mercado o selección de providers. Si el builder propone trabajar con un SDK distinto al ecosistema JavaScript, debe justificarlo explícitamente.

El segundo es la red sobre la que se ejecutará el proyecto: testnet hoodi para la mayoría de los casos, o mainnet cuando el proyecto requiera demostrar comportamiento económico real.

El tercero es el stack auxiliar relevante: lenguajes de programación, librerías externas, herramientas de paralelización o cualquier dependencia técnica significativa que el equipo deba conocer para evaluar la viabilidad.

El cuarto son las decisiones de arquitectura específicas, particularmente aquellas relacionadas con la paralelización del trabajo: cómo se dividirá la tarea en unidades distribuibles, cómo se agregarán los resultados, y cómo se manejarán errores o providers no responsivos.

### 5. Plan de trabajo

El builder debe proponer una división del proyecto en fases o hitos, con tiempos estimados para cada uno. No se requiere un cronograma detallado: una división aproximada que demuestre que el builder ha pensado en cómo distribuir el trabajo a lo largo de las dos a cuatro semanas previstas es suficiente.

Una división típica para un proyecto de tres semanas podría incluir una primera semana de configuración del entorno, exploración del SDK y construcción de la primera prueba de concepto; una segunda semana de desarrollo del componente paralelizado y validación de resultados; y una tercera semana de pulido, documentación, generación de métricas finales y preparación del entregable.

### 6. Entregables previstos

El builder debe especificar qué tendrá el repositorio al cierre del proyecto, qué métricas se documentarán, y qué tipo de demostración o evidencia se producirá. Estos entregables deben alinearse con los descritos en el track correspondiente del [Builders Guide](./guia_builders.md), aunque pueden incluir elementos adicionales propios de la propuesta.

Para proyectos con componente visual, conviene anticipar si se incluirá demo en vivo, capturas de pantalla, GIF animados o video explicativo. Para proyectos con componente cuantitativo, conviene anticipar qué tipo de visualizaciones o tablas de resultados acompañarán al entregable.

### 7. Experiencia previa relevante

Esta sección permite al equipo evaluar la capacidad de ejecución del builder. Debe describir brevemente el background técnico relevante para el proyecto, sin necesidad de un currículum exhaustivo.

Los elementos útiles a mencionar incluyen experiencia en el dominio del proyecto (por ejemplo, procesamiento de medios para Track A, finanzas computacionales para Track B), experiencia previa con Golem si la hay, proyectos similares construidos previamente, y enlaces a repositorios o demos que demuestren la capacidad técnica del builder o equipo.

Para builders sin experiencia previa con Golem, esta sección no es un obstáculo: el programa está explícitamente abierto a desarrolladores nuevos en el protocolo. Lo que se evalúa es la capacidad técnica general para ejecutar el proyecto propuesto, no la familiaridad previa con Golem.

### 8. Notas adicionales

Sección abierta donde el builder puede incluir cualquier información que ayude al equipo a evaluar la propuesta y que no encaje naturalmente en los campos anteriores. Los usos típicos incluyen riesgos identificados que el builder anticipa, decisiones de alcance que el builder quiere validar antes de comenzar, dependencias externas que pueden afectar la viabilidad del proyecto, preguntas específicas dirigidas al equipo, o cualquier contexto adicional relevante.

Esta sección es opcional. Pitches sin notas adicionales son perfectamente válidos cuando el resto del contenido es suficientemente claro.

---

## Plantilla limpia

A continuación se presenta la plantilla en formato listo para copiar y completar. Los campos entre corchetes deben reemplazarse por la información correspondiente.

```
GOLEM COMMUNITY BUILDER PROGRAMME — PITCH

1. INFORMACIÓN DE CONTACTO

Nombre completo: [nombre del builder o punto de contacto del equipo]
Correo electrónico: [dirección de email]
Discord: [identificador de Discord]
GitHub o portfolio: [enlace a perfil profesional]

Tipo de aplicación:
[ ] Builder individual
[ ] Equipo

Si aplica como equipo, listar miembros adicionales:
- [Nombre]: [rol en el proyecto] — [enlace a perfil]
- [Nombre]: [rol en el proyecto] — [enlace a perfil]

2. TRACK Y TÍTULO DEL PROYECTO

Track elegido:
[ ] Track A — Parallel Media Processing
[ ] Track B — Compute-Intensive Simulation
[ ] Track C — Provider Reputation & Benchmarking
[ ] Track D — Chess Engine / Game AI at Scale
[ ] Track E — Open Track

Título tentativo del proyecto: [título]

3. DESCRIPCIÓN DEL PROYECTO

[Uno o dos párrafos que expliquen qué se construirá, qué problema
o caso de uso aborda, y qué hace que el proyecto resulte interesante
desde la perspectiva del compute descentralizado.]

4. ALCANCE TÉCNICO

SDK a utilizar:
[ ] @golem-sdk/task-executor
[ ] @golem-sdk/golem-js 3.x
[ ] Otro: [especificar y justificar]

Red de ejecución:
[ ] Testnet (hoodi)
[ ] Mainnet

Stack auxiliar relevante:
[Lenguajes, librerías, herramientas externas y dependencias
técnicas significativas.]

Decisiones de arquitectura:
[Cómo se dividirá el trabajo en unidades paralelizables, cómo se
agregarán los resultados, y cómo se manejarán errores o providers
no responsivos.]

5. PLAN DE TRABAJO

Duración estimada: [número de semanas]

Hitos previstos:
- Semana 1: [actividades principales]
- Semana 2: [actividades principales]
- Semana 3: [actividades principales]
- Semana 4 (si aplica): [actividades principales]

6. ENTREGABLES PREVISTOS

Repositorio:
[Qué tendrá el repositorio al cierre del proyecto.]

Métricas a documentar:
[Qué métricas se reportarán y cómo se obtendrán.]

Demostración o evidencia:
[Tipo de demo, capturas, GIFs, video o visualizaciones que
acompañarán al entregable.]

7. EXPERIENCIA PREVIA RELEVANTE

[Breve descripción del background técnico relevante para el
proyecto. Mencionar experiencia en el dominio, experiencia previa
con Golem si la hay, y enlaces a proyectos previos si aplica.]


8. NOTAS ADICIONALES (OPCIONAL)

[Riesgos identificados, decisiones de alcance a validar,
dependencias externas, preguntas para el equipo, o cualquier
contexto adicional relevante. Esta sección es opcional.]
```

---

## Próximos pasos

Una vez completada la plantilla, el pitch debe enviarse a través del **formulario oficial del programa**:  [pendiente]. El formulario está estructurado de manera coherente con esta plantilla, por lo que la transferencia de la información es directa.

El equipo del programa revisa cada pitch y responde con una de tres posibilidades: aprobación directa, solicitud de ajustes en el alcance, o rechazo con justificación. La política completa de revisión se describe en el [README](../README.md) general del repositorio.

Para consultas previas al envío del pitch, el canal recomendado es el Discord oficial de Golem en [discord.gg/golem](https://discord.gg/golem).