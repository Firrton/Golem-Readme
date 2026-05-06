# Builders Guide

Documento técnico de referência do **Builder Programme**. Este guide descreve os cinco tracks disponíveis, o stack técnico recomendado, as considerações comuns a todos os projetos e os critérios que a equipe da Golem utiliza para avaliar o escopo técnico de cada proposta.

A leitura deste documento é o passo prévio recomendado antes de redigir um pitch. Permite identificar o track adequado, calibrar o escopo do projeto e compreender que nível de profundidade técnica é esperado do entregável.

---

## Marco geral

### Como funciona uma aplicação sobre Golem

Uma aplicação construída sobre a Golem Network opera sob um modelo de mercado descentralizado em que coexistem dois papéis principais. O **requestor** é quem solicita compute, define as características da carga de trabalho e paga por sua execução em $GLM. O **provider** é quem aporta capacidade computacional a partir de uma máquina conectada à rede e recebe o pagamento correspondente ao serviço prestado.

A interação entre ambos os papéis é gerida por meio de um mercado em que os requestors publicam ordens com seus requerimentos técnicos e de orçamento, os providers respondem com propostas, e a negociação se fecha por meio de um acordo formal que dispara a execução da tarefa. Todo o ciclo de vida, desde a negociação até o pagamento final, é mediado pelo daemon **yagna**, que cada participante roda localmente.

Para os builders do programa, esse modelo significa que cada projeto deve necessariamente executar trabalho real sobre a rede, seja testnet ou mainnet, e deve poder demonstrar por meio de logs e métricas que a execução efetivamente ocorreu de forma distribuída.

### Stack técnico vigente

A Golem Network oferece atualmente um stack de desenvolvimento organizado em camadas, projetado para permitir distintos níveis de abstração conforme a complexidade do caso de uso. O programa recomenda aos builders trabalhar com o stack vigente e evitar versões depreciadas.

O daemon central é **yagna**, em sua versão 0.17.4 ou superior, que é o componente que cada builder roda localmente para conectar-se à rede. A instalação do yagna é o primeiro passo técnico de qualquer projeto e está documentada em detalhe na documentação oficial da Golem.

Sobre yagna, o programa recomenda como caminho principal o uso de **@golem-sdk/task-executor**, uma biblioteca em JavaScript e TypeScript orientada especificamente a padrões map-reduce e paralelização de tarefas. Dado que os cinco tracks do programa giram em torno de cargas paralelizáveis, essa biblioteca oferece a abstração mais adequada para a maioria dos projetos: o builder define que tarefa deseja executar, e a biblioteca se encarrega de orquestrar providers, gerir reintentos e coordenar resultados.

Para builders com necessidades mais específicas ou experiência prévia em sistemas distribuídos, está disponível **@golem-sdk/golem-js** em sua versão 3.x, que oferece acesso direto aos modelos de baixo nível do protocolo (`ResourceRental`, `ExeUnit`, controle fino do market e da negociação). Essa opção é apropriada para projetos que requeiram lógica de orquestração não padrão, integração com frameworks complexos ou controle granular sobre a seleção de providers.

Adicionalmente, **@golem-sdk/react** está disponível para builders que desejem incorporar um frontend ao seu projeto, o que é particularmente relevante para os Tracks A e D, onde a dimensão visual aporta valor demonstrativo.

Como referência rápida, os builders devem assumir que a linguagem primária do programa é JavaScript ou TypeScript executado sobre Node.js 20 ou superior. Existem SDKs alternativos em outras linguagens, mas a documentação mais atualizada e os exemplos oficiais concentram-se no ecossistema JavaScript.

### Testnet e mainnet

O programa aceita entregáveis executados tanto na testnet da Golem quanto na mainnet. Cada opção tem implicações distintas que convém considerar ao planejar o projeto.

A testnet, que atualmente opera sobre a rede **hoodi**, é o ambiente recomendado para a maioria dos projetos do programa. Permite executar trabalho real sobre a rede sem necessidade de adquirir $GLM em mainnet, utiliza tokens de teste (tGLM) que podem ser obtidos gratuitamente a partir de um faucet, e oferece a mesma superfície de API que a mainnet. Para fins demonstrativos, a testnet é funcionalmente equivalente à mainnet e suficiente para satisfazer os requisitos do programa.

A mainnet, por sua vez, opera com $GLM real e deve ser utilizada quando o projeto requeira demonstrar comportamento econômico real, integrações com sistemas de produção ou casos de uso que dependam especificamente do marketplace em condições reais. Os builders que optem por mainnet devem prever em seu pitch os custos associados ao uso de compute, que em geral são modestos mas devem ficar documentados no entregável final.

A escolha entre testnet e mainnet deve ser explicitada no pitch e mantida consistente durante o desenvolvimento. Qualquer mudança entre redes durante a execução do projeto requer notificação à equipe da Golem.

---

## Track A — Parallel Media Processing

**Processamento paralelo de arquivos de áudio e vídeo em múltiplos providers.**

### Descrição

O processamento de mídias constitui o caso de uso clássico do compute descentralizado e a demonstração técnica mais legível para uma audiência ampla. A lógica é direta: um arquivo de grande tamanho é dividido em fragmentos, cada fragmento é processado de forma independente em um provider distinto, e os resultados são reagrupados em um único arquivo de saída. O que levaria vinte minutos em uma única máquina pode ser completado em uma fração do tempo se a carga for distribuída corretamente.

Esse track é especialmente adequado como primeiro projeto sobre Golem para builders Web2 com experiência em backend ou processamento de mídias. A lógica de chunking e merge é relativamente intuitiva, as ferramentas auxiliares (FFmpeg, Whisper) são amplamente conhecidas, e o entregável final permite demonstrar visualmente o benefício da paralelização.

### Direções de projeto sugeridas

**Transcodificação paralela de vídeo com FFmpeg.** Construir uma ferramenta que receba um arquivo de vídeo como input, divida-o em segmentos de duração fixa, execute FFmpeg sobre cada segmento em um provider distinto para transcodificá-lo a um ou vários formatos de saída (por exemplo, H.264 em distintas resoluções para streaming adaptativo), e reagrupe os segmentos em um arquivo final coerente. A métrica chave a documentar é o tempo total de processamento comparado com a execução sequencial em uma única máquina. Complexidade estimada: básica a intermediária.

**Transcrição paralela de áudio com Whisper.** Pegar um arquivo de áudio extenso (uma conferência, um podcast, uma entrevista), segmentá-lo em chunks com sobreposição mínima para preservar a continuidade, executar Whisper sobre cada chunk em paralelo por meio de múltiplos providers, e combinar as transcrições resultantes em um único texto com marcas temporais corretas. O projeto de referência [gScribe](https://gscribe.ai/) implementa essa direção e pode ser consultado como exemplo. Complexidade estimada: intermediária.

**Pipeline de processamento de imagens em escala.** Construir uma ferramenta que receba um conjunto grande de imagens (por exemplo, várias centenas ou milhares) e aplique transformações em paralelo: redimensionamento, conversão de formato, aplicação de filtros, extração de metadados, geração de thumbnails. O interesse técnico está em desenhar a unidade mínima de trabalho e em gerir eficientemente a transferência de arquivos entre o requestor e os providers. Complexidade estimada: básica a intermediária.

**Aplicação web com upload e processamento sobre Golem.** Construir uma interface web simples na qual um usuário possa subir um arquivo, escolher um tipo de processamento, e obter o resultado processado de volta. A aplicação deveria demonstrar de maneira transparente que o processamento ocorre sobre Golem, idealmente mostrando na UI o progresso dos providers individuais. Essa direção combina backend distribuído com frontend, e é particularmente adequada para builders com experiência full-stack. Complexidade estimada: intermediária a avançada.

### Stack técnico recomendado

O caminho mais direto é @golem-sdk/task-executor para a orquestração de tarefas paralelas, em combinação com FFmpeg, Whisper, ImageMagick ou outras ferramentas open-source instaladas dentro de imagens Golem personalizadas via Gvmkit-build. Os builders podem partir de imagens existentes no [Golem Registry](https://registry.golem.network) ou construir as suas a partir de um Dockerfile. Para projetos com frontend, @golem-sdk/react oferece hooks que simplificam a integração entre a interface e a execução sobre a rede.

### Entregáveis

O entregável consiste em um repositório público no GitHub com código funcional, README detalhado que inclua instruções de instalação e execução reproduzíveis, ao menos uma corrida documentada com métricas reais que comparem o tempo de execução sobre Golem contra uma baseline de uma única máquina, e um breve write-up publicado no Discord da Golem que explique em linguagem acessível o que se construiu e o que se aprendeu.

### Recursos relevantes

- [Tutorial: Running tasks in parallel](https://docs.golem.network/docs/creators/javascript/tutorials/running-parallel-tasks) na documentação oficial.
- [Tesseract OCR on Golem](https://github.com/golemfactory/tesseract-ocr-golem) como exemplo de biblioteca que paraleliza uma ferramenta CLI sobre a rede.
- [Golem Registry](https://registry.golem.network) para imagens preexistentes utilizáveis no projeto.

### Critério de sucesso

O projeto demonstra uma melhoria de tempo de processamento mensurável e reproduzível ao executar-se sobre Golem em comparação com uma única máquina, com métricas documentadas no README?

---

## Track B — Compute-Intensive Simulation

**Simulações numéricas, Monte Carlo e cálculos científicos em escala.**

### Descrição

A Golem é particularmente adequada para cargas de trabalho que se beneficiam de paralelismo em grande escala: simulações Monte Carlo, experimentos numéricos, análises combinatórias e qualquer cálculo no qual cada unidade de trabalho seja independente das demais. O interesse técnico desse track está menos na ferramenta utilizada e mais no desenho da paralelização: como dividir o problema em unidades de trabalho, como agregar os resultados parciais, e como apresentar as saídas de forma compreensível.

Esse track é adequado para builders com formação técnica ou acadêmica em disciplinas quantitativas (finanças, física, matemática aplicada, estatística, engenharia) que queiram usar a Golem como infraestrutura de computação para um experimento concreto. Também é atrativo para developers Web2 com interesse em computação de alto desempenho que busquem uma alternativa descentralizada a clusters tradicionais.

### Direções de projeto sugeridas

**Simulação Monte Carlo para pricing de opções financeiras.** Implementar um modelo de pricing de opções europeias ou asiáticas via simulação Monte Carlo, distribuindo dezenas ou centenas de milhares de paths de simulação por meio de múltiplos providers. O entregável deveria incluir comparação de resultados contra fórmulas analíticas conhecidas (Black-Scholes para opções europeias) como validação de correção, e métricas de convergência que mostrem como o erro diminui ao aumentar o número de simulações. Complexidade estimada: intermediária.

**Análise de risco de portfólio.** Construir uma ferramenta que receba a composição de um portfólio de ativos e execute uma análise de Value at Risk (VaR) ou Expected Shortfall por meio de simulação distribuída. O interesse do projeto está em demonstrar como a Golem permite rodar análises de maior granularidade ou sobre maior número de cenários do que seriam factíveis em uma máquina individual. Complexidade estimada: intermediária a avançada.

**Simulação física ou matemática paralelizável.** Implementar uma simulação clássica na qual cada unidade de trabalho é independente: dinâmica de partículas com condições iniciais aleatórias, geração distribuída de fractais com parâmetros variáveis, busca de padrões em autômatos celulares, exploração de espaços de parâmetros em modelos epidemiológicos. A escolha do problema é livre desde que o componente de paralelização seja genuíno e a saída seja visualizável ou apresentável de forma clara. Complexidade estimada: intermediária.

**Benchmark de multiplicação de matrizes em escala.** Implementar multiplicação distribuída de matrizes grandes via particionamento por blocos, comparando o desempenho da Golem contra hardware local em distintos tamanhos de input. Esse projeto é mais técnico do que aplicado, mas produz dados quantitativos úteis sobre as características da rede e pode tornar-se uma referência para futuros builders. Complexidade estimada: avançada.

### Stack técnico recomendado

@golem-sdk/task-executor é novamente a opção principal para a orquestração. A escolha da linguagem de cálculo dentro dos providers é livre e depende do problema: Python com NumPy e SciPy é habitual para problemas científicos, enquanto C++ ou Rust são preferíveis quando o gargalo é CPU puro. Os builders podem empacotar suas dependências em imagens Golem personalizadas via Gvmkit-build. Para visualização de resultados, bibliotecas padrão como matplotlib, Plotly ou D3.js são adequadas e não requerem ser executadas sobre Golem.

### Entregáveis

O repositório deve incluir código funcional com instruções reproduzíveis, os resultados de ao menos uma corrida real com visualização ou tabela de resultados, uma seção no README que documente o que foi paralelizado, o que se manteve sequencial e por quê, e notas sobre os desafios técnicos encontrados durante a paralelização (granularidade das tarefas, manejo de erros, agregação de resultados).

### Recursos relevantes

- [Task API Quickstarts](https://docs.golem.network/docs/creators/javascript/quickstarts) para padrões básicos de paralelização.
- [Golem Workers](https://github.com/golemfactory/golem-workers) como API alternativa de alto nível para acesso direto a CPU e GPU.

### Critério de sucesso

O projeto executa efetivamente cálculos em paralelo em múltiplos providers, produz resultados validáveis contra uma baseline conhecida ou uma análise de convergência, e documenta de forma compreensível as decisões de design da paralelização?

---

## Track C — Provider Reputation & Benchmarking

**Ferramentas de medição, observabilidade e análise sobre o ecossistema de providers.**

### Descrição

À medida que cresce o número de providers conectados à rede, a pergunta de quais são rápidos, confiáveis, econômicos ou adequados para cargas específicas torna-se cada vez mais relevante. A Golem já conta com um sistema de reputação oficial implementado no componente AgreementSelector, o que significa que esse track não busca substituir essa infraestrutura, mas sim construir ferramentas complementares que a enriqueçam: dashboards públicos, suítes de benchmarking especializadas, ferramentas de auditoria e visualizações que tornem os dados do ecossistema mais acessíveis.

Esse track é adequado para builders com experiência em data engineering, observabilidade, dashboards ou sistemas distribuídos. Produz entregáveis com um valor diferencial claro: diferentemente dos tracks orientados a demos, os projetos desse track podem se tornar ferramentas de uso contínuo dentro do ecossistema.

### Direções de projeto sugeridas

**Dashboard público de métricas da rede.** Construir uma aplicação web que consulte o estado da rede Golem, recolha dados sobre providers ativos, distribuição de preços, latências, capacidades de hardware oferecidas, e os apresente em um dashboard acessível e atualizado. O projeto pode consumir dados do AgreementSelector existente e enriquecê-los com métricas próprias. Complexidade estimada: intermediária.

**Suíte de benchmarking para cargas específicas.** Desenhar e implementar uma bateria de testes padronizados que meçam o desempenho dos providers em categorias concretas de workload: rendering, transcodificação, inferência de ML, cálculo numérico. A suíte deveria executar-se periodicamente, armazenar resultados de forma estruturada, e publicar rankings ou comparativas que permitam a outros builders escolher providers adequados a seus casos de uso. Complexidade estimada: intermediária a avançada.

**Ferramenta de auditoria independente.** Construir uma ferramenta que valide de forma externa as métricas reportadas pelo sistema oficial de reputação, executando testes aleatórios sobre providers selecionados e comparando os resultados observados contra os esperados segundo o AgreementSelector. O valor do projeto está em aportar transparência adicional ao ecossistema. Complexidade estimada: avançada.

**Bot do Discord ou agente de notificações.** Construir um bot que monitore o estado da rede de forma contínua e publique no Discord da Golem alertas ou resumos periódicos: novos providers, quedas detectadas, mudanças significativas em pricing, top performers da semana. O projeto combina infraestrutura de monitoramento com apresentação acessível para a comunidade. Complexidade estimada: básica a intermediária.

### Stack técnico recomendado

O projeto requer uso do SDK da Golem para a execução de testes sobre providers (@golem-sdk/golem-js é preferível a task-executor nesse track porque os projetos costumam precisar de controle fino sobre seleção de providers e filtros de mercado), um backend para o armazenamento estruturado de resultados (PostgreSQL, SQLite ou um banco de dados serverless conforme o escopo), e um frontend ou camada de apresentação adequada ao formato do entregável (dashboard web, bot do Discord, API pública).

### Entregáveis

O repositório deve incluir código funcional, ao menos uma execução completa com dados reais coletados da rede, uma visualização ou resumo dos dados obtidos, e documentação que permita a outros builders executar a ferramenta ou consumir suas saídas.

### Recursos relevantes

- [Golem AgreementSelector](https://blog.golem.network/agreementselector/) como referência do sistema oficial de reputação.
- [API do yagna](https://docs.golem.network/docs/golem/yagna) para acesso programático ao estado da rede.

### Critério de sucesso

O projeto produz dados reais sobre o estado da rede Golem, apresenta-os de forma compreensível e útil, e aporta valor que complemente o sistema oficial de reputação sem duplicá-lo?

---

## Track D — Chess Engine / Game AI at Scale

**Inteligência artificial de jogos como demonstração legível de paralelismo.**

### Descrição

Distribuir um motor de inteligência artificial de jogos (chess, Go, Othello, jogos de estratégia) por meio de múltiplos providers resulta surpreendentemente efetivo como demonstração pública da Golem. A lógica é visualmente compreensível, tecnicamente não trivial, e o resultado é legível inclusive para audiências não técnicas. Esse track utiliza game AI como veículo de demonstração do paralelismo, não como objetivo em si mesmo.

É adequado para builders com interesse em jogos, IA, busca em árvores de decisão ou sistemas distribuídos, e produz entregáveis com alto potencial viral em redes sociais e comunidade. Um demo bem construído nesse track pode tornar-se um dos recursos de marketing mais efetivos do programa.

### Direções de projeto sugeridas

**Stockfish distribuído sobre Golem.** Implementar um wrapper que distribua a análise do Stockfish (o motor de chess open-source mais forte) por meio de múltiplos providers, permitindo analisar várias posições simultaneamente ou aprofundar a análise de uma única posição via particionamento da árvore de busca. A variante com Stockfish-MPI é particularmente adequada para paralelização distribuída. Complexidade estimada: intermediária a avançada.

**Interface visual de análise distribuída.** Construir uma aplicação web que mostre em tempo real como a análise se distribui entre providers: uma posição de chess na tela, providers individuais avaliando distintas linhas, e os resultados consolidando-se em uma recomendação final. A dimensão visual torna o projeto particularmente demonstrativo. Complexidade estimada: avançada.

**Torneio distribuído de motores.** Implementar um sistema que execute torneios automáticos entre distintos motores de chess (Stockfish, Komodo, motores próprios) sobre Golem, com cada partida executando-se em um provider diferente. O entregável inclui os resultados do torneio, métricas de tempo e custo, e uma interface para visualizar as partidas. Complexidade estimada: intermediária.

**Game AI alternativo distribuído.** Em vez de chess, implementar paralelização para outro jogo: Go com Monte Carlo Tree Search distribuído, pôquer com simulação de mãos em escala, ou um jogo de estratégia com busca profunda. A escolha do jogo é livre desde que o componente paralelizável seja genuíno. Complexidade estimada: intermediária a avançada.

### Stack técnico recomendado

@golem-sdk/task-executor para a orquestração de avaliações paralelas, junto com o motor de jogo escolhido (Stockfish costuma compilar-se a partir das fontes para integrações avançadas). Para a interface visual, @golem-sdk/react permite vincular o estado do jogo com a execução sobre a rede de forma natural. Bibliotecas como chess.js ou equivalentes facilitam a representação do estado do jogo no frontend.

### Entregáveis

O repositório deve incluir código funcional com instruções de execução, uma gravação ou capturas que mostrem o sistema em operação, métricas que documentem o custo em $GLM e os tempos de execução observados, e um write-up para Discord que explique de forma acessível o que se construiu.

### Recursos relevantes

- [Stockfish](https://stockfishchess.org/) como motor de chess de referência.
- [chess.js](https://github.com/jhlywa/chess.js) para manipulação de estado de partidas em JavaScript.

### Critério de sucesso

O projeto distribui genuinamente computação entre múltiplos providers, produz um entregável visualmente compreensível para uma audiência ampla, e documenta métricas concretas de desempenho e custo?

---

## Track E — Open Track

**Proposta livre do builder, validada antes do início.**

### Descrição

O Track E está reservado para builders que tenham uma ideia própria que utilize o compute da Golem de forma interessante e que não se encaixe naturalmente nos quatro tracks anteriores. A flexibilidade é deliberada: a equipe da Golem prefere financiar trabalho bem orientado por iniciativa própria do builder em vez de forçar projetos a se ajustarem a tracks predefinidos.

As únicas condições substantivas são que o projeto execute efetivamente sobre Golem, produza um entregável público e compartilhável, e demonstre o que o compute descentralizado permite fazer. A condição procedural é que o pitch deve ser revisado e aprovado antes do início do desenvolvimento, o que é válido para todos os tracks mas adquire particular importância nesse caso.

### Direções admissíveis

Qualquer projeto que requeira compute distribuído paralelizável de maneira não trivial qualifica-se para esse track. Isso inclui ferramentas e integrações que conectem a Golem com outros ecossistemas (Ethereum mainnet, IPFS, outros protocolos de Web3), demos exploratórias que mostrem capacidades do protocolo a uma audiência técnica especializada, bibliotecas reutilizáveis que facilitem o uso da Golem para casos de uso específicos, ou projetos artísticos e experimentais que utilizem a rede de forma criativa.

Não se qualificam para esse track propostas que utilizem a Golem apenas de forma marginal ou decorativa, projetos que dupliquem trabalho já realizado pela equipe da Golem ou por participantes anteriores do programa, nem projetos de escopo tão amplo que não sejam realizáveis em quatro semanas com um bounty de 500 USD.

### Processo específico

Dado que o track não tem direções predefinidas, a equipe da Golem requer maior detalhe no pitch para avaliar a viabilidade. Recomenda-se incluir, além dos elementos padrão da [pitch-template](./pitch_template.md), uma seção breve que justifique por que o projeto não se encaixa nos tracks A a D, uma descrição explícita do componente paralelizável, e qualquer referência a trabalho prévio similar que o builder tenha considerado.

### Entregáveis

Os entregáveis são os mesmos que para os tracks específicos: repositório público com código funcional, README claro, métricas de execução sobre Golem, e write-up para Discord. A forma específica do entregável é acordada durante a aprovação do pitch.

### Critério de sucesso

O projeto demonstra de forma concreta uma capacidade da Golem que nenhum projeto prévio do programa havia mostrado, e produz um entregável público que a comunidade possa estudar, replicar ou utilizar?

---

## Notas técnicas comuns

Para além das particularidades de cada track, existem considerações transversais que se aplicam a qualquer projeto do programa e que convém ter presentes desde a fase de design.

### Granularidade das tarefas

O design correto da unidade mínima de trabalho é provavelmente a decisão técnica mais importante de qualquer projeto. Tarefas demasiadamente pequenas geram overhead de negociação e comunicação que erode o benefício da paralelização. Tarefas demasiadamente grandes desperdiçam a capacidade da rede ao concentrar trabalho em poucos providers. Como heurística inicial, uma unidade de trabalho razoável é executada na ordem de segundos a minutos em um provider individual, não milissegundos nem horas.

### Manejo de erros e reintentos

Os providers em uma rede descentralizada podem falhar, desconectar-se ou produzir resultados inválidos. Qualquer projeto sério sobre Golem deve contemplar mecanismos de reintentos, validação de saídas, e eventualmente exclusão de providers problemáticos. @golem-sdk/task-executor inclui lógica de reintentos por padrão, mas os builders devem verificar que os parâmetros sejam adequados ao seu caso de uso e documentar as decisões tomadas.

### Logging e observabilidade

As métricas do entregável final devem ser críveis e reproduzíveis. Isso requer logging estruturado durante a execução do projeto: timestamps de cada tarefa, identificadores de provider, custos individuais, erros capturados. Os entregáveis que reportam métricas sem logs de suporte têm menor valor demonstrativo. Recomenda-se utilizar o pacote `debug` do Node.js ou equivalente, configurando os namespaces `golem-js:*` para capturar a atividade relevante do SDK.

### Seleção entre task-executor e golem-js

Como regra geral, task-executor é a opção correta quando o problema se ajusta a um padrão map-reduce: tarefas independentes, mesmo tipo de cálculo, agregação simples de resultados. golem-js direto é preferível quando o projeto requer controle fino sobre a seleção de providers, lógica de mercado personalizada, gestão de sessões de longa duração, ou integração com frameworks que não sejam compatíveis com o modelo task-based.

### Custos e orçamento

Um projeto típico do programa, executado majoritariamente em testnet, tem custos desprezíveis em compute. Para projetos em mainnet, os custos variam conforme o volume de trabalho e os providers selecionados, mas geralmente mantêm-se na ordem de unidades a dezenas de $GLM para os escopos esperados. Os builders que executem em mainnet devem prever esse custo e documentá-lo no entregável.

### Limitações a considerar

A Golem é uma rede de propósito geral, mas existem certos casos de uso onde seu desempenho pode ser subótimo. Cargas que requerem comunicação de muito baixa latência entre providers durante a execução não são ideais para Golem, dado que a rede otimiza paralelização embaraçosa em vez de sincronização fina. Workloads que requerem GPUs específicas podem encontrar disponibilidade limitada ou variável. Transferências de arquivos muito grandes entre requestor e providers introduzem overhead que deve ser considerado na arquitetura.

Essas limitações não descartam nenhum track do programa, mas convém tê-las em conta ao definir o escopo do projeto durante a fase de pitch.
