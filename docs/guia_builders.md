# Builders Guide

Documento técnico de referencia del **Builder Programme**. Este guide describe los cinco tracks disponibles, el stack técnico recomendado, las consideraciones comunes a todos los proyectos y los criterios que el equipo de Golem utiliza para evaluar el alcance técnico de cada propuesta.

La lectura de este documento es el paso previo recomendado antes de redactar un pitch. Permite identificar el track adecuado, calibrar el alcance del proyecto y comprender qué nivel de profundidad técnica se espera del entregable.

---

## Marco general

### Cómo funciona una aplicación sobre Golem

Una aplicación construida sobre Golem Network opera bajo un modelo de mercado descentralizado en el que coexisten dos roles principales. El **requestor** es quien solicita compute, define las características de la carga de trabajo y paga por su ejecución en $GLM. El **provider** es quien aporta capacidad computacional desde una máquina conectada a la red y recibe el pago correspondiente al servicio prestado.

La interacción entre ambos roles se gestiona a través de un mercado en el que los requestors publican órdenes con sus requerimientos técnicos y de presupuesto, los providers responden con propuestas, y la negociación se cierra mediante un acuerdo formal que dispara la ejecución de la tarea. Todo el ciclo de vida, desde la negociación hasta el pago final, está mediado por el daemon **yagna**, que cada participante corre localmente.

Para los builders del programa, este modelo significa que cada proyecto debe necesariamente ejecutar trabajo real sobre la red, ya sea testnet o mainnet, y debe poder demostrar mediante logs y métricas que la ejecución efectivamente ocurrió de forma distribuida.

### Stack técnico vigente

Golem Network ofrece actualmente un stack de desarrollo organizado en capas, diseñado para permitir distintos niveles de abstracción según la complejidad del caso de uso. El programa recomienda a los builders trabajar con el stack vigente y evitar versiones deprecadas.

El daemon central es **yagna**, en su versión 0.17.4 o superior, que es el componente que cada builder corre localmente para conectarse a la red. La instalación de yagna es el primer paso técnico de cualquier proyecto y se documenta en detalle en el [Getting Started](./getting-started.md).

Sobre yagna, el programa recomienda como camino principal el uso de **@golem-sdk/task-executor**, una librería en JavaScript y TypeScript orientada específicamente a patrones map-reduce y paralelización de tareas. Dado que los cinco tracks del programa giran alrededor de cargas paralelizables, esta librería ofrece la abstracción más adecuada para la mayoría de los proyectos: el builder define qué tarea quiere ejecutar, la librería se encarga de orquestar providers, gestionar reintentos y coordinar resultados.

Para builders con necesidades más específicas o experiencia previa en sistemas distribuidos, está disponible **@golem-sdk/golem-js** en su versión 3.x, que ofrece acceso directo a los modelos de bajo nivel del protocolo (`ResourceRental`, `ExeUnit`, control fino del market y de la negociación). Esta opción es apropiada para proyectos que requieran lógica de orquestación no estándar, integración con frameworks complejos o control granular sobre la selección de providers.

Adicionalmente, **@golem-sdk/react** está disponible para builders que deseen incorporar un frontend a su proyecto, lo cual es particularmente relevante para los Tracks A y D, donde la dimensión visual aporta valor demostrativo.

Como referencia rápida, los builders deben asumir que el lenguaje primario del programa es JavaScript o TypeScript ejecutado sobre Node.js 20 o superior. Existen SDKs alternativos en otros lenguajes, pero la documentación más actualizada y los ejemplos oficiales se concentran en el ecosistema JavaScript.

### Testnet y mainnet

El programa acepta entregables ejecutados tanto en la testnet de Golem como en mainnet. Cada opción tiene implicaciones distintas que conviene considerar al planificar el proyecto.

La testnet, que actualmente opera sobre la red **hoodi**, es el entorno recomendado para la mayoría de los proyectos del programa. Permite ejecutar trabajo real sobre la red sin necesidad de adquirir $GLM en mainnet, utiliza tokens de prueba (tGLM) que se pueden obtener gratuitamente desde un faucet, y ofrece la misma superficie de API que mainnet. Para fines demostrativos, la testnet es funcionalmente equivalente a mainnet y suficiente para satisfacer los requisitos del programa.

La mainnet, por su parte, opera con $GLM real y debe utilizarse cuando el proyecto requiera demostrar comportamiento económico real, integraciones con sistemas de producción o casos de uso que dependan específicamente del marketplace en condiciones reales. Los builders que opten por mainnet deben prever en su pitch los costos asociados al uso de compute, que en general son modestos pero deben quedar documentados en el entregable final.

La elección entre testnet y mainnet debe explicitarse en el pitch y mantenerse consistente durante el desarrollo. Cualquier cambio entre redes durante la ejecución del proyecto requiere notificación al equipo de Golem.

---

## Track A — Parallel Media Processing

**Procesamiento paralelo de archivos de audio y video sobre múltiples providers.**

### Descripción

El procesamiento de medios constituye el caso de uso clásico del compute descentralizado y la demostración técnica más legible para una audiencia amplia. La lógica es directa: un archivo de gran tamaño se divide en fragmentos, cada fragmento se procesa de forma independiente sobre un provider distinto, y los resultados se reensamblan en un único archivo de salida. Lo que tomaría veinte minutos en una sola máquina puede completarse en una fracción del tiempo si la carga se distribuye correctamente.

Este track resulta especialmente adecuado como primer proyecto sobre Golem para builders Web2 con experiencia en backend o procesamiento de medios. La lógica de chunking y merge es relativamente intuitiva, las herramientas auxiliares (FFmpeg, Whisper) son ampliamente conocidas, y el entregable final permite demostrar visualmente el beneficio de la paralelización.

### Direcciones de proyecto sugeridas

**Transcodificación paralela de video con FFmpeg.** Construir una herramienta que tome un archivo de video como input, lo divida en segmentos de duración fija, ejecute FFmpeg sobre cada segmento en un provider distinto para transcodificarlo a uno o varios formatos de salida (por ejemplo, H.264 a distintas resoluciones para streaming adaptativo), y reensamble los segmentos en un archivo final coherente. La métrica clave a documentar es el tiempo total de procesamiento comparado con la ejecución secuencial sobre una sola máquina. Complejidad estimada: básica a intermedia.

**Transcripción paralela de audio con Whisper.** Tomar un archivo de audio extenso (una conferencia, un podcast, una entrevista), segmentarlo en chunks con superposición mínima para preservar continuidad, ejecutar Whisper sobre cada chunk en paralelo a través de múltiples providers, y combinar las transcripciones resultantes en un único texto con marcas temporales correctas. El proyecto de referencia [gScribe](https://gscribe.ai/) implementa esta dirección y puede consultarse como ejemplo. Complejidad estimada: intermedia.

**Pipeline de procesamiento de imágenes a escala.** Construir una herramienta que reciba un conjunto grande de imágenes (por ejemplo, varios cientos o miles) y aplique transformaciones en paralelo: redimensionado, conversión de formato, aplicación de filtros, extracción de metadatos, generación de thumbnails. El interés técnico está en diseñar la unidad mínima de trabajo y en gestionar eficientemente la transferencia de archivos entre el requestor y los providers. Complejidad estimada: básica a intermedia.

**Aplicación web con upload y procesamiento sobre Golem.** Construir una interfaz web simple en la que un usuario pueda subir un archivo, elegir un tipo de procesamiento, y obtener el resultado procesado de vuelta. La aplicación debería demostrar de manera transparente que el procesamiento ocurre sobre Golem, idealmente mostrando en la UI el progreso de los providers individuales. Esta dirección combina backend distribuido con frontend, y es particularmente adecuada para builders con experiencia full-stack. Complejidad estimada: intermedia a avanzada.

### Stack técnico recomendado

El camino más directo es @golem-sdk/task-executor para la orquestación de tareas paralelas, en combinación con FFmpeg, Whisper, ImageMagick u otras herramientas open-source instaladas dentro de imágenes Golem personalizadas mediante Gvmkit-build. Los builders pueden partir de imágenes existentes en el [Golem Registry](https://registry.golem.network) o construir las suyas a partir de un Dockerfile. Para proyectos con frontend, @golem-sdk/react ofrece hooks que simplifican la integración entre la interfaz y la ejecución sobre la red.

### Entregables

El entregable consiste en un repositorio público en GitHub con código funcional, README detallado que incluya instrucciones de instalación y ejecución reproducibles, al menos una corrida documentada con métricas reales que comparen el tiempo de ejecución sobre Golem contra una baseline de una sola máquina, y un breve write-up publicado en el Discord de Golem que explique en lenguaje accesible qué se construyó y qué se aprendió.

### Recursos relevantes

- [Tutorial: Running tasks in parallel](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) en la documentación oficial.
- [Tesseract OCR on Golem](https://github.com/golemfactory/tesseract-ocr-golem) como ejemplo de librería que paraleliza una herramienta CLI sobre la red.
- [Golem Registry](https://registry.golem.network) para imágenes preexistentes utilizables en el proyecto.

### Criterio de éxito

¿El proyecto demuestra una mejora de tiempo de procesamiento medible y reproducible al ejecutarse sobre Golem en comparación con una sola máquina, con métricas documentadas en el README?

---

## Track B — Compute-Intensive Simulation

**Simulaciones numéricas, Monte Carlo y cálculos científicos a escala.**

### Descripción

Golem es particularmente adecuado para cargas de trabajo que se benefician de paralelismo a gran escala: simulaciones Monte Carlo, experimentos numéricos, análisis combinatorios y cualquier cálculo en el que cada unidad de trabajo sea independiente de las demás. El interés técnico de este track está menos en la herramienta utilizada y más en el diseño de la paralelización: cómo dividir el problema en unidades de trabajo, cómo agregar los resultados parciales, y cómo presentar los outputs de manera comprensible.

Este track es adecuado para builders con formación técnica o académica en disciplinas cuantitativas (finanzas, física, matemática aplicada, estadística, ingeniería) que quieran usar Golem como infraestructura de cómputo para un experimento concreto. También es atractivo para developers Web2 con interés en computación de alto rendimiento que busquen una alternativa descentralizada a clusters tradicionales.

### Direcciones de proyecto sugeridas

**Simulación Monte Carlo para pricing de opciones financieras.** Implementar un modelo de pricing de opciones europeas o asiáticas mediante simulación Monte Carlo, distribuyendo decenas o cientos de miles de paths de simulación a través de múltiples providers. El entregable debería incluir comparación de resultados contra fórmulas analíticas conocidas (Black-Scholes para opciones europeas) como validación de correctitud, y métricas de convergencia que muestren cómo el error disminuye al aumentar el número de simulaciones. Complejidad estimada: intermedia.

**Análisis de riesgo de portafolio.** Construir una herramienta que reciba la composición de un portafolio de activos y ejecute un análisis de Value at Risk (VaR) o Expected Shortfall mediante simulación distribuida. El interés del proyecto está en demostrar cómo Golem permite correr análisis de mayor granularidad o sobre mayor número de escenarios de los que serían factibles en una máquina individual. Complejidad estimada: intermedia a avanzada.

**Simulación física o matemática paralelizable.** Implementar una simulación clásica en la que cada unidad de trabajo es independiente: dinámica de partículas con condiciones iniciales aleatorias, generación distribuida de fractales con parámetros variables, búsqueda de patrones en autómatas celulares, exploración de espacios de parámetros en modelos epidemiológicos. La elección del problema es libre siempre que el componente de paralelización sea genuino y la salida sea visualizable o presentable de manera clara. Complejidad estimada: intermedia.

**Benchmark de multiplicación de matrices a escala.** Implementar multiplicación distribuida de matrices grandes mediante particionamiento por bloques, comparando la performance de Golem contra hardware local en distintos tamaños de input. Este proyecto es más técnico que aplicado, pero produce datos cuantitativos útiles sobre las características de la red y puede convertirse en una referencia para futuros builders. Complejidad estimada: avanzada.

### Stack técnico recomendado

@golem-sdk/task-executor es nuevamente la opción principal para la orquestación. La elección del lenguaje de cómputo dentro de los providers es libre y depende del problema: Python con NumPy y SciPy es habitual para problemas científicos, mientras que C++ o Rust son preferibles cuando el cuello de botella es CPU puro. Los builders pueden empaquetar sus dependencias en imágenes Golem personalizadas mediante Gvmkit-build. Para visualización de resultados, librerías estándar como matplotlib, Plotly o D3.js son adecuadas y no requieren ejecutarse sobre Golem.

### Entregables

El repositorio debe incluir código funcional con instrucciones reproducibles, los resultados de al menos una corrida real con visualización o tabla de resultados, una sección en el README que documente qué se paralelizó, qué se mantuvo secuencial y por qué, y notas sobre los desafíos técnicos encontrados durante la paralelización (granularidad de las tareas, manejo de errores, agregación de resultados).

### Recursos relevantes

- [Task API Quickstarts](https://docs.golem.network/docs/creators/javascript/quickstarts) para patrones básicos de paralelización.
- [Golem Workers](https://github.com/golemfactory/golem-workers) como API alternativa de alto nivel para acceso directo a CPU y GPU.

### Criterio de éxito

¿El proyecto ejecuta efectivamente cálculos en paralelo sobre múltiples providers, produce resultados validables contra una baseline conocida o un análisis de convergencia, y documenta de forma comprensible las decisiones de diseño de la paralelización?

---

## Track C — Provider Reputation & Benchmarking

**Herramientas de medición, observabilidad y análisis sobre el ecosistema de providers.**

### Descripción

A medida que crece el número de providers conectados a la red, la pregunta de cuáles son rápidos, confiables, económicos o adecuados para cargas específicas se vuelve cada vez más relevante. Golem ya cuenta con un sistema de reputación oficial implementado en el componente AgreementSelector, lo cual significa que este track no apunta a reemplazar esa infraestructura, sino a construir herramientas complementarias que la enriquezcan: dashboards públicos, suites de benchmarking especializadas, herramientas de auditoría y visualizaciones que hagan los datos del ecosistema más accesibles.

Este track es adecuado para builders con experiencia en data engineering, observabilidad, dashboards o sistemas distribuidos. Produce entregables con un valor diferencial claro: a diferencia de los tracks orientados a demos, los proyectos de este track pueden convertirse en herramientas de uso continuo dentro del ecosistema.

### Direcciones de proyecto sugeridas

**Dashboard público de métricas de la red.** Construir una aplicación web que consulte el estado de la red Golem, recopile datos sobre providers activos, distribución de precios, latencias, capacidades de hardware ofrecidas, y los presente en un dashboard accesible y actualizado. El proyecto puede consumir datos del AgreementSelector existente y enriquecerlos con métricas propias. Complejidad estimada: intermedia.

**Suite de benchmarking para cargas específicas.** Diseñar e implementar una batería de tests estandarizados que midan la performance de los providers en categorías concretas de workload: rendering, transcodificación, inferencia de ML, cálculo numérico. La suite debería ejecutarse periódicamente, almacenar resultados de manera estructurada, y publicar rankings o comparativas que permitan a otros builders elegir providers adecuados a sus casos de uso. Complejidad estimada: intermedia a avanzada.

**Herramienta de auditoría independiente.** Construir una herramienta que valide de manera externa las métricas reportadas por el sistema oficial de reputación, ejecutando tests aleatorios sobre providers seleccionados y comparando los resultados observados contra los esperados según el AgreementSelector. El valor del proyecto está en aportar transparencia adicional al ecosistema. Complejidad estimada: avanzada.

**Bot de Discord o agente de notificaciones.** Construir un bot que monitoree el estado de la red de manera continua y publique en el Discord de Golem alertas o resúmenes periódicos: nuevos providers, caídas detectadas, cambios significativos en pricing, top performers de la semana. El proyecto combina infraestructura de monitoreo con presentación accesible para la comunidad. Complejidad estimada: básica a intermedia.

### Stack técnico recomendado

El proyecto requiere uso del SDK de Golem para la ejecución de tests sobre providers (@golem-sdk/golem-js es preferible a task-executor en este track porque los proyectos suelen necesitar control fino sobre selección de providers y filtros de mercado), un backend para el almacenamiento estructurado de resultados (PostgreSQL, SQLite, o una base de datos serverless según el alcance), y un frontend o capa de presentación adecuada al formato del entregable (dashboard web, bot de Discord, API pública).

### Entregables

El repositorio debe incluir código funcional, al menos una ejecución completa con datos reales recopilados de la red, una visualización o resumen de los datos obtenidos, y documentación que permita a otros builders ejecutar la herramienta o consumir sus outputs.

### Recursos relevantes

- [Golem AgreementSelector](https://blog.golem.network/agreementselector/) como referencia del sistema oficial de reputación.
- [API de yagna](https://docs.golem.network/docs/golem/yagna) para acceso programático al estado de la red.

### Criterio de éxito

¿El proyecto produce datos reales sobre el estado de la red Golem, los presenta de manera comprensible y útil, y aporta valor que complemente al sistema oficial de reputación sin duplicarlo?

---

## Track D — Chess Engine / Game AI at Scale

**Inteligencia artificial de juegos como demostración legible de paralelismo.**

### Descripción

Distribuir un motor de inteligencia artificial de juegos (chess, Go, Othello, juegos de estrategia) a través de múltiples providers resulta sorprendentemente efectivo como demostración pública de Golem. La lógica es visualmente comprensible, técnicamente no trivial, y el resultado es legible incluso para audiencias no técnicas. Este track utiliza game AI como vehículo de demostración del paralelismo, no como objetivo en sí mismo.

Es adecuado para builders con interés en juegos, IA, búsqueda en árboles de decisión o sistemas distribuidos, y produce entregables con alto potencial viral en redes sociales y comunidad. Un demo bien construido en este track puede convertirse en uno de los recursos de marketing más efectivos del programa.

### Direcciones de proyecto sugeridas

**Stockfish distribuido sobre Golem.** Implementar un wrapper que distribuya el análisis de Stockfish (el motor de chess open-source más fuerte) a través de múltiples providers, permitiendo analizar varias posiciones simultáneamente o profundizar el análisis de una sola posición mediante particionamiento del árbol de búsqueda. La variante con Stockfish-MPI es particularmente adecuada para paralelización distribuida. Complejidad estimada: intermedia a avanzada.

**Interfaz visual de análisis distribuido.** Construir una aplicación web que muestre en tiempo real cómo el análisis se distribuye entre providers: una posición de chess en pantalla, providers individuales evaluando distintas líneas, y los resultados consolidándose en una recomendación final. La dimensión visual hace al proyecto particularmente demostrativo. Complejidad estimada: avanzada.

**Torneo distribuido de motores.** Implementar un sistema que ejecute torneos automáticos entre distintos motores de chess (Stockfish, Komodo, motores propios) sobre Golem, con cada partida ejecutándose en un provider diferente. El entregable incluye los resultados del torneo, métricas de tiempo y costo, y una interfaz para visualizar las partidas. Complejidad estimada: intermedia.

**Game AI alternativo distribuido.** En lugar de chess, implementar paralelización para otro juego: Go con Monte Carlo Tree Search distribuido, póker con simulación de manos a escala, o un juego de estrategia con búsqueda profunda. La elección del juego es libre siempre que el componente paralelizable sea genuino. Complejidad estimada: intermedia a avanzada.

### Stack técnico recomendado

@golem-sdk/task-executor para la orquestación de evaluaciones paralelas, junto con el motor de juego elegido (Stockfish suele compilarse desde fuentes para integraciones avanzadas). Para la interfaz visual, @golem-sdk/react permite vincular el estado del juego con la ejecución sobre la red de manera natural. Librerías como chess.js o equivalentes facilitan la representación del estado del juego en el frontend.

### Entregables

El repositorio debe incluir código funcional con instrucciones de ejecución, una grabación o capturas que muestren el sistema en operación, métricas que documenten el costo en $GLM y los tiempos de ejecución observados, y un write-up para Discord que explique de manera accesible qué se construyó.

### Recursos relevantes

- [Stockfish](https://stockfishchess.org/) como motor de chess de referencia.
- [chess.js](https://github.com/jhlywa/chess.js) para manipulación de estado de partidas en JavaScript.

### Criterio de éxito

¿El proyecto distribuye genuinamente cómputo entre múltiples providers, produce un entregable visualmente comprensible para una audiencia amplia, y documenta métricas concretas de rendimiento y costo?

---

## Track E — Open Track

**Propuesta libre del builder, validada antes del inicio.**

### Descripción

El Track E está reservado para builders que tengan una idea propia que utilice el compute de Golem de manera interesante y no encaje naturalmente en los cuatro tracks anteriores. La flexibilidad es deliberada: el equipo de Golem prefiere financiar trabajo bien orientado por iniciativa propia del builder antes que forzar proyectos a ajustarse a tracks predefinidos.

Las únicas condiciones sustantivas son que el proyecto se ejecute efectivamente sobre Golem, produzca un entregable público y compartible, y demuestre lo que el compute descentralizado permite hacer. La condición procedural es que el pitch debe ser revisado y aprobado antes del inicio del desarrollo, lo cual es válido para todos los tracks pero adquiere particular importancia en este caso.

### Direcciones admisibles

Cualquier proyecto que requiera compute distribuido paralelizable de manera no trivial califica para este track. Esto incluye herramientas e integraciones que conecten Golem con otros ecosistemas (Ethereum mainnet, IPFS, otros protocolos de Web3), demos exploratorias que muestren capacidades del protocolo a una audiencia técnica especializada, librerías reutilizables que faciliten el uso de Golem para casos de uso específicos, o proyectos artísticos y experimentales que utilicen la red de manera creativa.

No califican para este track propuestas que utilicen Golem solo de manera marginal o decorativa, proyectos que dupliquen trabajo ya realizado por el equipo de Golem o por participantes anteriores del programa, ni proyectos de scope tan amplio que no sean realizables en cuatro semanas con un bounty de 500 USD.

### Proceso específico

Dado que el track no tiene direcciones predefinidas, el equipo de Golem requiere mayor detalle en el pitch para evaluar la viabilidad. Se recomienda incluir, además de los elementos estándar de la [pitch-template](./pitch-template.md), una sección breve que justifique por qué el proyecto no encaja en los tracks A a D, una descripción explícita del componente paralelizable, y cualquier referencia a trabajo previo similar que el builder haya considerado.

### Entregables

Los entregables son los mismos que para los tracks específicos: repositorio público con código funcional, README claro, métricas de ejecución sobre Golem, y write-up para Discord. La forma específica del entregable se acuerda durante la aprobación del pitch.

### Criterio de éxito

¿El proyecto demuestra de manera concreta una capacidad de Golem que ningún proyecto previo del programa había mostrado, y produce un entregable público que la comunidad pueda estudiar, replicar o utilizar?

---

## Notas técnicas comunes

Más allá de las particularidades de cada track, existen consideraciones transversales que aplican a cualquier proyecto del programa y que conviene tener presentes desde la fase de diseño.

### Granularidad de las tareas

El diseño correcto de la unidad mínima de trabajo es probablemente la decisión técnica más importante de cualquier proyecto. Tareas demasiado pequeñas generan overhead de negociación y comunicación que erosiona el beneficio de la paralelización. Tareas demasiado grandes desperdician la capacidad de la red al concentrar trabajo en pocos providers. Como heurística inicial, una unidad de trabajo razonable se ejecuta en el orden de segundos a minutos en un provider individual, no milisegundos ni horas.

### Manejo de errores y reintentos

Los providers en una red descentralizada pueden fallar, desconectarse o producir resultados inválidos. Cualquier proyecto serio sobre Golem debe contemplar mecanismos de reintento, validación de outputs, y eventualmente exclusión de providers problemáticos. @golem-sdk/task-executor incluye lógica de reintentos por defecto, pero los builders deben verificar que los parámetros sean adecuados a su caso de uso y documentar las decisiones tomadas.

### Logging y observabilidad

Las métricas del entregable final deben ser creíbles y reproducibles. Esto requiere logging estructurado durante la ejecución del proyecto: timestamps de cada tarea, identificadores de provider, costos individuales, errores capturados. Los entregables que reportan métricas sin logs de soporte tienen menor valor demostrativo. Se recomienda utilizar el paquete `debug` de Node.js o equivalente, configurando los namespaces `golem-js:*` para capturar la actividad relevante del SDK.

### Selección entre task-executor y golem-js

Como regla general, task-executor es la opción correcta cuando el problema se ajusta a un patrón map-reduce: tareas independientes, mismo tipo de cómputo, agregación simple de resultados. golem-js directo es preferible cuando el proyecto requiere control fino sobre la selección de providers, lógica de mercado personalizada, gestión de sesiones de larga duración, o integración con frameworks que no sean compatibles con el modelo task-based.

### Costos y presupuesto

Un proyecto típico del programa, ejecutado mayoritariamente en testnet, tiene costos despreciables en compute. Para proyectos en mainnet, los costos varían según el volumen de trabajo y los providers seleccionados, pero generalmente se mantienen en el orden de unidades a decenas de $GLM para los alcances esperados. Los builders que ejecuten en mainnet deben prever este costo y documentarlo en el entregable.

### Limitaciones a tener presentes

Golem es una red de propósito general, pero existen ciertos casos de uso donde su rendimiento puede ser subóptimo. Cargas que requieren comunicación de muy baja latencia entre providers durante la ejecución no son ideales para Golem, dado que la red optimiza paralelización embarazosa antes que sincronización fina. Workloads que requieren GPU específicas pueden encontrar disponibilidad limitada o variable. Transferencias de archivos muy grandes entre requestor y providers introducen overhead que debe ser considerado en la arquitectura.

Estas limitaciones no descartan ningún track del programa, pero conviene tenerlas en cuenta al definir el alcance del proyecto durante la fase de pitch.

