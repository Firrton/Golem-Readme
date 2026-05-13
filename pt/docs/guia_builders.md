# Builders Guide

Referência técnica do **Builder Programme**: cinco tracks, stack recomendado e critérios de avaliação. Leitura prévia antes de aplicar.

> Quando você tiver sua ideia, candidate-se através do [formulário oficial de candidatura](https://forms.golem.network/golem-builders-programme).

---

## Marco geral

### Modelo da rede

Golem opera como um mercado descentralizado com dois papéis: o **requestor** solicita compute e paga em $GLM; o **provider** aporta capacidade e recebe. Ambos os lados rodam o daemon **yagna** localmente. Cada projeto do programa precisa executar trabalho real na rede (testnet ou mainnet) e demonstrá-lo com logs e métricas.

→ Referência: [Overview da Golem](https://docs.golem.network/docs/golem/overview).

### Stack vigente

| Camada | Componente | Quando usar |
|---|---|---|
| Daemon | **yagna** ≥ 0.17.4 | Sempre. Ponto de entrada à rede. [Instalação](https://docs.golem.network/docs/quickstarts/js-quickstart). |
| Orquestração alta | **@golem-sdk/task-executor** | Por padrão. Padrões map-reduce e paralelização. [Task Model](https://docs.golem.network/docs/creators/javascript/guides/task-model). |
| Orquestração baixa | **@golem-sdk/golem-js** 3.x | Controle fino do market, seleção custom de providers. [API Reference](https://docs.golem.network/docs/golem-js/reference/overview). |
| Frontend | **@golem-sdk/react** | Quando o projeto tem UI (Tracks A e D principalmente). |

Linguagem primária: **JavaScript / TypeScript sobre Node.js ≥ 20**. Existem SDKs em outras linguagens, mas a documentação e os exemplos vivem no ecossistema JS.

### Testnet vs mainnet

- **Testnet (`hoodi`)** — Recomendada por padrão. tGLM grátis via comando CLI `yagna payment fund`, mesma API que mainnet, funcionalmente equivalente para fins demonstrativos. Alternativas também suportadas: sepolia, rinkeby, amoy. [Quickstart com `payment fund`](https://docs.golem.network/docs/quickstarts/js-quickstart).
- **Mainnet (Polygon)** — Apenas se o projeto exigir comportamento econômico real ou integração com produção. Roda sobre **Polygon** (`erc20-polygon-glm`), não Ethereum L1. Custos típicos: unidades a dezenas de $GLM por projeto. Documentar custos no entregável. [Switching to mainnet](https://docs.golem.network/docs/creators/javascript/examples/switching-to-mainnet) · [Modelo de pagamentos](https://docs.golem.network/docs/golem/payments).

A escolha é declarada no formulário de candidatura e mantida durante o desenvolvimento. Qualquer mudança é notificada à equipe.

---

## Track A — Parallel Media Processing

**Processamento paralelo de áudio e vídeo sobre múltiplos providers.**

Caso de uso clássico do compute descentralizado e demo mais legível para audiência ampla. Ideal como primeiro projeto para builders Web2 com experiência em backend ou processamento de mídia.

**Direções sugeridas:**
- **Transcodificação paralela com FFmpeg** — Dividir vídeo, transcodificar segmentos em paralelo, remontar. Métrica-chave: tempo total vs. execução sequencial. *Complexidade: básica-intermediária.*
- **Transcrição paralela com Whisper** — Áudio longo segmentado em chunks, transcrição distribuída, merge com marcações temporais. Referência: [gScribe](https://gscribe.ai/). *Intermediária.*
- **Pipeline de imagens em escala** — Centenas/milhares de imagens com transformações paralelas (resize, formato, filtros, metadados). *Básica-intermediária.*
- **Web app com upload e processamento** — UI para subir arquivo, escolher processamento, mostrar progresso por provider. *Intermediária-avançada.*

**Stack:** task-executor + FFmpeg/Whisper/ImageMagick em imagens Golem custom via Gvmkit-build. Frontend opcional com @golem-sdk/react. Partir de imagens do [Golem Registry](https://registry.golem.network) ou Dockerfile próprio.

**Recursos:** [Tutorial parallel tasks](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) · [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image) (FFmpeg, Whisper) · [Transferring data](https://docs.golem.network/docs/creators/javascript/examples/transferring-data) (chunks) · [Running in browser](https://docs.golem.network/docs/creators/javascript/tutorials/running-in-browser) (web app) · [tesseract-ocr-golem](https://github.com/golemfactory/tesseract-ocr-golem) · [Golem Registry](https://registry.golem.network)

**Critério de sucesso:** O projeto demonstra melhora de tempo mensurável e reproduzível sobre Golem vs. uma única máquina, com métricas no README?

---

## Track B — Compute-Intensive Simulation

**Simulações numéricas, Monte Carlo e cálculos científicos em escala.**

Cargas paralelizáveis onde cada unidade de trabalho é independente. O valor técnico está no desenho da paralelização: como dividir, como agregar resultados, como apresentar outputs. Adequado para builders com formação quantitativa (finanças, física, estatística, engenharia).

**Direções sugeridas:**
- **Monte Carlo para pricing de opções** — Dezenas/centenas de milhares de paths distribuídos. Validar contra Black-Scholes para opções europeias. *Intermediária.*
- **Análise de risco de portfólio** — VaR ou Expected Shortfall por simulação distribuída. *Intermediária-avançada.*
- **Simulação física ou matemática** — Dinâmica de partículas, fractais, autômatos celulares, modelos epidemiológicos. Saída visualizável. *Intermediária.*
- **Benchmark de multiplicação de matrizes** — Particionamento por blocos, comparação com hardware local. *Avançada.*

**Stack:** task-executor para orquestração. Linguagem livre dentro dos providers (Python+NumPy/SciPy habitual, C++/Rust se o gargalo for CPU). Empacotar com Gvmkit-build. Visualização local: matplotlib, Plotly, D3.js.

**Recursos:** [Running parallel tasks](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) · [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image) (Python+NumPy/SciPy) · [Task API Quickstarts](https://docs.golem.network/docs/creators/javascript/quickstarts) · [Golem Workers](https://github.com/golemfactory/golem-workers) (API alternativa para CPU/GPU direto)

**Critério de sucesso:** Executa cálculos paralelos reais sobre múltiplos providers, produz resultados validáveis contra baseline conhecida ou análise de convergência, e documenta as decisões de paralelização?

---

## Track C — Provider Reputation & Benchmarking

**Ferramentas de medição, observabilidade e análise sobre o ecossistema de providers.**

Golem já tem reputação oficial via AgreementSelector. Este track não a substitui: complementa com dashboards, suites de benchmarking, auditorias e visualizações. Diferentemente dos tracks de demo, os entregáveis aqui podem virar ferramentas de uso contínuo.

**Direções sugeridas:**
- **Dashboard público de métricas** — Estado da rede, providers ativos, preços, latências, hardware. *Intermediária.*
- **Suite de benchmarking por workload** — Testes padronizados (rendering, transcodificação, ML, cálculo) com execução periódica e rankings. *Intermediária-avançada.*
- **Ferramenta de auditoria independente** — Validar as métricas oficiais com testes aleatórios sobre providers. *Avançada.*
- **Bot de Discord / agente de notificações** — Alertas ou resumos periódicos: novos providers, quedas, mudanças de pricing. *Básica-intermediária.*

**Stack:** **golem-js direto** (preferível a task-executor pelo controle fino sobre seleção de providers) + backend para armazenamento estruturado (Postgres, SQLite, serverless) + camada de apresentação conforme o formato (dashboard, bot, API).

**Recursos:** [Selecting providers](https://docs.golem.network/docs/creators/javascript/examples/selecting-providers) · [golem-js API Reference](https://docs.golem.network/docs/golem-js/reference/overview) · [Golem AgreementSelector](https://blog.golem.network/agreementselector/) · [API do yagna](https://docs.golem.network/docs/golem/yagna)

**Critério de sucesso:** Produz dados reais sobre o estado da rede, apresenta-os de forma útil, e complementa o sistema oficial sem duplicá-lo?

---

## Track D — Chess Engine / Game AI at Scale

**Game AI distribuída como demonstração legível de paralelismo.**

Distribuir um motor de IA de jogos (chess, Go, Othello, estratégia) funciona surpreendentemente bem como demo público: lógica visualmente compreensível, tecnicamente não trivial, legível inclusive para audiência não técnica. Alto potencial viral.

**Direções sugeridas:**
- **Stockfish distribuído** — Wrapper que distribui análise via Stockfish-MPI ou particionamento da árvore de busca. *Intermediária-avançada.*
- **Interface visual de análise distribuída** — UI que mostra em tempo real como providers avaliam linhas e os resultados consolidam. *Avançada.*
- **Torneio distribuído de motores** — Partidas automáticas entre Stockfish, Komodo e motores próprios, uma por provider. *Intermediária.*
- **Game AI alternativo** — Go com MCTS distribuído, poker com simulação de mãos, jogos de estratégia com busca profunda. *Intermediária-avançada.*

**Stack:** task-executor para orquestração + motor do jogo (Stockfish compilado a partir das fontes para integrações avançadas). Para UI: @golem-sdk/react + chess.js ou equivalente.

**Recursos:** [Running parallel tasks](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) · [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image) (Stockfish compilado a partir das fontes) · [Stockfish](https://stockfishchess.org/) · [chess.js](https://github.com/jhlywa/chess.js)

**Critério de sucesso:** Distribui compute real entre múltiplos providers, produz um entregável visualmente compreensível, e documenta métricas de desempenho e custo?

---

## Track E — Open Track

**Proposta livre do builder, validada antes do início.**

Para builders com uma ideia própria que use Golem de forma interessante e não se encaixe nos tracks A-D. Condições: executa sobre Golem real, entregável público, demonstra capacidades do compute descentralizado.

**Admissíveis:** integrações com outros ecossistemas (Ethereum, IPFS, outros Web3), demos exploratórias para audiência técnica, bibliotecas reutilizáveis, projetos artísticos ou experimentais.

**Não admissíveis:** uso marginal ou decorativo de Golem, duplicação de trabalho prévio da equipe ou de builders passados, escopo inexecutável em 4 semanas com 500 USD.

**Processo:** as respostas do formulário de candidatura devem incluir mais detalhe do que nos tracks A-D: justificativa de por que a ideia não se encaixa nos tracks definidos, descrição explícita do componente paralelizável, e referências a trabalho prévio similar que o builder tenha considerado.

**Critério de sucesso:** Demonstra de forma concreta uma capacidade da Golem que nenhum projeto prévio do programa tenha mostrado, e produz um entregável público que a comunidade possa estudar, replicar ou usar?

---

## Entregáveis

A lista abaixo é orientativa. Os entregáveis concretos são acordados com a equipa da Golem quando o projecto é seleccionado.

- **Repositório público no GitHub** — sob o utilizador ou org do builder, com um README de configuração claro que um terceiro possa clonar e executar.
- **Licença de código aberto** — MIT recomendada; o ficheiro `LICENSE` deve estar presente na raiz do repositório.
- **Documentação técnica** — no README do repositório: o que foi construído, como a paralelização funciona, decisões técnicas, resultados e métricas sobre Golem Network.
- **Vídeo demo (2–3 minutos)** — uma gravação curta mostrando o projecto em funcionamento, usada para amplificação nos canais da Golem.

---

## Notas técnicas comuns

- **Granularidade das tarefas** — A unidade mínima deveria executar na ordem de **segundos a minutos** por provider. Menor = overhead de negociação que erode o benefício. Maior = desperdiça capacidade da rede.
- **Erros e retentativas** — Os providers podem falhar ou produzir outputs inválidos. task-executor traz lógica de retentativas por padrão; ajustar parâmetros e documentar as decisões.
- **Logging e observabilidade** — Métricas críveis exigem logs estruturados (timestamps, provider ID, custos, erros). Recomendado: pacote `debug` do Node com namespace `golem-js:*`.
- **task-executor vs golem-js** — task-executor quando é map-reduce clássico. golem-js quando há necessidade de controle fino do market, sessões longas ou lógica de seleção custom.
- **Custos** — Testnet: desprezível. Mainnet: tipicamente unidades a dezenas de $GLM para os escopos do programa. Documentar sempre.
- **Limitações** — Golem otimiza paralelização embaraçosa, não comunicação de baixa latência entre providers. GPUs específicas podem ter disponibilidade variável. Transferências muito grandes entre requestor e providers agregam overhead.

---

## Se algo falhar

Antes de pedir ajuda no Discord, vale revisar a documentação oficial de troubleshooting — a maioria dos problemas frequentes já está coberta lá.

- **Erros de yagna, app-key, pagamentos e file transfer** — [Troubleshooting JS Requestor](https://docs.golem.network/docs/troubleshooting/js-requestor). Cobre `ECONNREFUSED 127.0.0.1:7465` (yagna não roda), `Invalid application key`, `Insufficient funds` (falta `yagna payment fund`), `There is no requestor account...` (falta `yagna payment init`), `Transfer error: send failed because receiver is gone` (falta `VOLUME` no Dockerfile) e erros de CORS ao rodar a partir do browser.
- **Imagens que não buildam ou transferências quebradas** — [Golem Images FAQ](https://docs.golem.network/docs/creators/javascript/guides/golem-images-faq) e [Building custom image](https://docs.golem.network/docs/creators/javascript/tutorials/building-custom-image). Lembrar: qualquer diretório onde forem ser escritos ou enviados arquivos tem que estar declarado como `VOLUME` no Dockerfile.
- **Comportamento inesperado do task-executor** — [Task Model](https://docs.golem.network/docs/creators/javascript/guides/task-model) para entender o ciclo de vida de Activity, retries e seleção de providers.
- **Pagamentos e allocations** — [Modelo de pagamentos](https://docs.golem.network/docs/golem/payments) para entender pay-as-you-go, batching e diferenças entre testnet/mainnet.

Se o problema persistir e não aparecer na documentação, abrir consulta no canal de builders do [Discord da Golem](https://discord.gg/golem) incluindo: comando que falhou, erro exato, versão do yagna (`yagna --version`) e rede (testnet hoodi / mainnet polygon).
