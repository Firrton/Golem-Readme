# Builders Guide

Referencia técnica del **Builder Programme**: cinco tracks, stack recomendado y criterios de evaluación. Lectura previa antes del pitch.

---

## Marco general

### Modelo de la red

Golem opera como un mercado descentralizado con dos roles: el **requestor** pide compute y paga en $GLM; el **provider** aporta capacidad y cobra. Ambos lados corren el daemon **yagna** localmente. Cada proyecto del programa tiene que ejecutar trabajo real en la red (testnet o mainnet) y demostrarlo con logs y métricas.

→ Referencia: [Overview de Golem](https://docs.golem.network/docs/golem/overview).

### Stack vigente

| Capa | Componente | Cuándo usarlo |
|---|---|---|
| Daemon | **yagna** ≥ 0.17.4 | Siempre. Punto de entrada a la red. [Instalación](https://docs.golem.network/docs/quickstarts/js-quickstart). |
| Orquestación alta | **@golem-sdk/task-executor** | Por defecto. Patrones map-reduce y paralelización. [Task Model](https://docs.golem.network/docs/creators/javascript/guides/task-model). |
| Orquestación baja | **@golem-sdk/golem-js** 3.x | Control fino del market, selección custom de providers. [API Reference](https://docs.golem.network/docs/golem-js/reference/overview). |
| Frontend | **@golem-sdk/react** | Cuando el proyecto tiene UI (Tracks A y D principalmente). |

Lenguaje primario: **JavaScript / TypeScript sobre Node.js ≥ 20**. Existen SDKs en otros lenguajes, pero la documentación y ejemplos viven en el ecosistema JS.

### Testnet vs mainnet

- **Testnet (`hoodi`)** — Recomendada por defecto. tGLM gratis vía comando CLI `yagna payment fund`, misma API que mainnet, funcionalmente equivalente para fines demostrativos. Alternativas también soportadas: sepolia, rinkeby, amoy. [Quickstart con `payment fund`](https://docs.golem.network/docs/quickstarts/js-quickstart).
- **Mainnet (Polygon)** — Solo si el proyecto requiere comportamiento económico real o integración con producción. Corre sobre **Polygon** (`erc20-polygon-glm`), no Ethereum L1. Costos típicos: unidades a decenas de $GLM por proyecto. Documentar costos en el entregable. [Switching to mainnet](https://docs.golem.network/docs/creators/javascript/examples/switching-to-mainnet) · [Modelo de pagos](https://docs.golem.network/docs/golem/payments).

La elección se declara en el pitch y se mantiene durante el desarrollo. Cualquier cambio se notifica al equipo.

---

## Track A — Parallel Media Processing

**Procesamiento paralelo de audio y video sobre múltiples providers.**

Caso de uso clásico del compute descentralizado y demo más legible para audiencia amplia. Ideal como primer proyecto para builders Web2 con experiencia en backend o procesamiento de medios.

**Direcciones sugeridas:**
- **Transcodificación paralela con FFmpeg** — Dividir video, transcodificar segmentos en paralelo, reensamblar. Métrica clave: tiempo total vs. ejecución secuencial. *Complejidad: básica-intermedia.*
- **Transcripción paralela con Whisper** — Audio largo segmentado en chunks, transcripción distribuida, merge con marcas temporales. Referencia: [gScribe](https://gscribe.ai/). *Intermedia.*
- **Pipeline de imágenes a escala** — Cientos/miles de imágenes con transformaciones paralelas (resize, formato, filtros, metadatos). *Básica-intermedia.*
- **Web app con upload y procesamiento** — UI para subir archivo, elegir procesamiento, mostrar progreso por provider. *Intermedia-avanzada.*

**Stack:** task-executor + FFmpeg/Whisper/ImageMagick en imágenes Golem custom vía Gvmkit-build. Frontend opcional con @golem-sdk/react. Partir de imágenes del [Golem Registry](https://registry.golem.network) o Dockerfile propio.

**Recursos:** [Tutorial parallel tasks](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) · [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image) (FFmpeg, Whisper) · [Transferring data](https://docs.golem.network/docs/creators/javascript/examples/transferring-data) (chunks) · [Running in browser](https://docs.golem.network/docs/creators/javascript/tutorials/running-in-browser) (web app) · [tesseract-ocr-golem](https://github.com/golemfactory/tesseract-ocr-golem) · [Golem Registry](https://registry.golem.network)

**Criterio de éxito:** ¿El proyecto demuestra mejora de tiempo medible y reproducible sobre Golem vs. una sola máquina, con métricas en el README?

---

## Track B — Compute-Intensive Simulation

**Simulaciones numéricas, Monte Carlo y cálculos científicos a escala.**

Cargas paralelizables donde cada unidad de trabajo es independiente. El valor técnico está en el diseño de la paralelización: cómo dividir, cómo agregar resultados, cómo presentar outputs. Adecuado para builders con formación cuantitativa (finanzas, física, estadística, ingeniería).

**Direcciones sugeridas:**
- **Monte Carlo para pricing de opciones** — Decenas/cientos de miles de paths distribuidos. Validar contra Black-Scholes para opciones europeas. *Intermedia.*
- **Análisis de riesgo de portafolio** — VaR o Expected Shortfall por simulación distribuida. *Intermedia-avanzada.*
- **Simulación física o matemática** — Dinámica de partículas, fractales, autómatas celulares, modelos epidemiológicos. Salida visualizable. *Intermedia.*
- **Benchmark de multiplicación de matrices** — Particionamiento por bloques, comparación con hardware local. *Avanzada.*

**Stack:** task-executor para orquestación. Lenguaje libre dentro de los providers (Python+NumPy/SciPy habitual, C++/Rust si el cuello es CPU). Empaquetar con Gvmkit-build. Visualización local: matplotlib, Plotly, D3.js.

**Recursos:** [Running parallel tasks](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) · [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image) (Python+NumPy/SciPy) · [Task API Quickstarts](https://docs.golem.network/docs/creators/javascript/quickstarts) · [Golem Workers](https://github.com/golemfactory/golem-workers) (API alternativa para CPU/GPU directo)

**Criterio de éxito:** ¿Ejecuta cálculos paralelos reales sobre múltiples providers, produce resultados validables contra baseline conocida o análisis de convergencia, y documenta las decisiones de paralelización?

---

## Track C — Provider Reputation & Benchmarking

**Herramientas de medición, observabilidad y análisis sobre el ecosistema de providers.**

Golem ya tiene reputación oficial vía AgreementSelector. Este track no la reemplaza: la complementa con dashboards, suites de benchmarking, auditorías y visualizaciones. A diferencia de los tracks de demo, los entregables acá pueden volverse herramientas de uso continuo.

**Direcciones sugeridas:**
- **Dashboard público de métricas** — Estado de la red, providers activos, precios, latencias, hardware. *Intermedia.*
- **Suite de benchmarking por workload** — Tests estandarizados (rendering, transcodificación, ML, cálculo) con ejecución periódica y rankings. *Intermedia-avanzada.*
- **Herramienta de auditoría independiente** — Validar las métricas oficiales con tests aleatorios sobre providers. *Avanzada.*
- **Bot de Discord / agente de notificaciones** — Alertas o resúmenes periódicos al canal: nuevos providers, caídas, cambios de pricing. *Básica-intermedia.*

**Stack:** **golem-js directo** (preferible a task-executor por el control fino sobre selección de providers) + backend para almacenamiento estructurado (Postgres, SQLite, serverless) + capa de presentación según formato (dashboard, bot, API).

**Recursos:** [Selecting providers](https://docs.golem.network/docs/creators/javascript/examples/selecting-providers) · [golem-js API Reference](https://docs.golem.network/docs/golem-js/reference/overview) · [Golem AgreementSelector](https://blog.golem.network/agreementselector/) · [API de yagna](https://docs.golem.network/docs/golem/yagna)

**Criterio de éxito:** ¿Produce datos reales sobre el estado de la red, los presenta de forma útil, y complementa el sistema oficial sin duplicarlo?

---

## Track D — Chess Engine / Game AI at Scale

**Game AI distribuida como demostración legible de paralelismo.**

Distribuir un motor de IA de juegos (chess, Go, Othello, estrategia) funciona sorprendentemente bien como demo pública: lógica visualmente comprensible, técnicamente no trivial, legible incluso para audiencia no técnica. Alto potencial viral.

**Direcciones sugeridas:**
- **Stockfish distribuido** — Wrapper que distribuye análisis vía Stockfish-MPI o particionamiento del árbol de búsqueda. *Intermedia-avanzada.*
- **Interfaz visual de análisis distribuido** — UI que muestra en tiempo real cómo providers evalúan líneas y los resultados se consolidan. *Avanzada.*
- **Torneo distribuido de motores** — Partidas automáticas entre Stockfish, Komodo y motores propios, una por provider. *Intermedia.*
- **Game AI alternativo** — Go con MCTS distribuido, póker con simulación de manos, juegos de estrategia con búsqueda profunda. *Intermedia-avanzada.*

**Stack:** task-executor para orquestación + motor del juego (Stockfish compilado desde fuentes para integraciones avanzadas). Para UI: @golem-sdk/react + chess.js o equivalente.

**Recursos:** [Running parallel tasks](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) · [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image) (Stockfish compilado desde fuentes) · [Stockfish](https://stockfishchess.org/) · [chess.js](https://github.com/jhlywa/chess.js)

**Criterio de éxito:** ¿Distribuye cómputo real entre múltiples providers, produce un entregable visualmente comprensible, y documenta métricas de rendimiento y costo?

---

## Track E — Open Track

**Propuesta libre del builder, validada antes del inicio.**

Para builders con una idea propia que use Golem de manera interesante y no entre en los tracks A-D. Condiciones: ejecuta sobre Golem real, entregable público, demuestra capacidades del compute descentralizado.

**Admisibles:** integraciones con otros ecosistemas (Ethereum, IPFS, otros Web3), demos exploratorias para audiencia técnica, librerías reutilizables, proyectos artísticos o experimentales.

**No admisibles:** uso marginal o decorativo de Golem, duplicación de trabajo previo del equipo o de builders pasados, scope inejecutable en 4 semanas con 500 USD.

**Proceso:** pitch con mayor detalle que en A-D. Incluir justificación de por qué no encaja en los tracks definidos, descripción explícita del componente paralelizable, y referencias a trabajo previo similar que el builder haya considerado.

**Criterio de éxito:** ¿Demuestra de forma concreta una capacidad de Golem que ningún proyecto previo del programa haya mostrado, y produce un entregable público que la comunidad pueda estudiar, replicar o usar?

---

## Notas técnicas comunes

- **Granularidad de tareas** — La unidad mínima debería ejecutarse en el orden de **segundos a minutos** por provider. Más chica = overhead de negociación que erosiona el beneficio. Más grande = desperdicia capacidad de la red.
- **Errores y reintentos** — Los providers pueden fallar o producir outputs inválidos. task-executor trae lógica de reintentos por defecto; ajustar parámetros y documentar las decisiones.
- **Logging y observabilidad** — Métricas creíbles requieren logs estructurados (timestamps, provider ID, costos, errores). Recomendado: paquete `debug` de Node con namespace `golem-js:*`.
- **task-executor vs golem-js** — task-executor cuando es map-reduce clásico. golem-js cuando hace falta control fino del market, sesiones largas o lógica de selección custom.
- **Costos** — Testnet: despreciable. Mainnet: típicamente unidades a decenas de $GLM para los alcances del programa. Documentar siempre.
- **Limitaciones** — Golem optimiza paralelización embarazosa, no comunicación de baja latencia entre providers. GPUs específicas pueden tener disponibilidad variable. Transferencias muy grandes entre requestor y providers agregan overhead.

---

## Si algo falla

Antes de pedir ayuda en Discord, conviene revisar la documentación oficial de troubleshooting — la mayoría de los problemas frecuentes ya están cubiertos ahí.

- **Errores de yagna, app-key, pagos y file transfer** — [Troubleshooting JS Requestor](https://docs.golem.network/docs/troubleshooting/js-requestor). Cubre `ECONNREFUSED 127.0.0.1:7465` (yagna no corre), `Invalid application key`, `Insufficient funds` (falta `yagna payment fund`), `There is no requestor account...` (falta `yagna payment init`), `Transfer error: send failed because receiver is gone` (falta `VOLUME` en el Dockerfile) y errores de CORS al correr desde browser.
- **Imágenes que no buildean o transferencias rotas** — [Golem Images FAQ](https://docs.golem.network/docs/creators/javascript/guides/golem-images-faq) y [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image). Recordar: cualquier directorio donde se vayan a escribir o subir archivos tiene que estar declarado como `VOLUME` en el Dockerfile.
- **Comportamiento inesperado del task-executor** — [Task Model](https://docs.golem.network/docs/creators/javascript/guides/task-model) para entender el ciclo de vida de Activity, retries y selección de providers.
- **Pagos y allocations** — [Modelo de pagos](https://docs.golem.network/docs/golem/payments) para entender pay-as-you-go, batching y diferencias entre testnet/mainnet.

Si el problema persiste y no aparece en la documentación, abrir consulta en el canal de builders del [Discord de Golem](https://discord.gg/golem) incluyendo: comando que falló, error exacto, versión de yagna (`yagna --version`) y red (testnet hoodi / mainnet polygon).
