<div align="center">

<img src="../assets/golem-logo-tagline.png" alt="Golem Network — Create. Compute. Earn." width="520" />

<br /><br />

# Golem Community Builder Programme

**Construa sobre compute descentralizado. Receba bounties em $GLM.**

<br />

[![Bounty](https://img.shields.io/badge/Bounty-500%20USD%20em%20%24GLM-0F1FE3?style=for-the-badge)](#processo-de-participação)
[![Status](https://img.shields.io/badge/Status-Aberto%20%26%20Contínuo-22C55E?style=for-the-badge)](#)
[![License](https://img.shields.io/badge/License-Open%20Source-1E40AF?style=for-the-badge)](#)
[![Discord](https://img.shields.io/badge/Discord-Golem%20Community-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/golem)

<br />

[**Builders Guide**](./docs/guia_builders.md) ·
[**Pitch Template**](./docs/pitch_template.md) ·
[**Submission Guide**](./docs/submission-guide.md) ·
[**FAQ**](./FAQ.md)

</div>

---

## Introdução

O **Golem Community Builder Programme** é uma iniciativa aberta e contínua dirigida a desenvolvedores que desejem construir projetos funcionais sobre a Golem Network, a rede descentralizada de compute open-source operativa desde 2016.

Diferentemente de um hackathon tradicional, o programa não opera sob pressão de prazos finais nem por meio de competições de pitch. Seu objetivo é financiar trabalho técnico genuíno que demonstre, de maneira concreta, as capacidades do protocolo: projetos que vivam no GitHub, gerem conversa na comunidade e contribuam ao ecossistema de compute descentralizado.

> Cada projeto aprovado recebe um bounty de **500 USD pagos em $GLM**, com duração estimada entre duas e quatro semanas de desenvolvimento.

---

## Sobre a Golem Network

A Golem Network é um marketplace descentralizado de recursos computacionais. Os desenvolvedores podem alugar capacidade de processamento proveniente de máquinas reais distribuídas por toda a rede, pagar pelo seu uso em $GLM e executar tarefas paralelizáveis em uma escala que seria impraticável em uma única máquina: transcodificação de vídeo, inferência de modelos de machine learning, simulações científicas, processamento massivo de dados, entre outros casos de uso.

A proposta técnica é direta: se uma tarefa leva dez minutos em uma máquina, a Golem permite distribuí-la entre cem providers e completá-la em uma fração do tempo. A rede é permissionless, o que significa que qualquer pessoa pode consumir compute como requestor ou aportar capacidade como provider, sem intermediários nem autorizações prévias.

#### Recursos oficiais

| Recurso | Link |
|---------|--------|
| Documentação técnica | [docs.golem.network](https://docs.golem.network) |
| Repositórios oficiais | [github.com/golemfactory](https://github.com/golemfactory) |
| Informações do token $GLM | [golem.network/glm](https://golem.network/glm) |
| Comunidade Discord | [discord.gg/golem](https://discord.gg/golem) |

---

## Por que existe este programa

A Golem é um protocolo maduro com um caso técnico sólido, mas boa parte de seu potencial ainda não está adequadamente documentada por meio de projetos concretos. A maneira mais efetiva de mostrar o que o protocolo faz não é por meio de material de marketing, mas sim por meio de código funcional construído por desenvolvedores reais, com repositórios públicos, métricas reproduzíveis e explicações claras.

Este programa existe para encurtar essa distância. Financia builders que estejam dispostos a explorar o protocolo em profundidade e a publicar o resultado de forma transparente, gerando recursos que tanto a comunidade Golem quanto novos desenvolvedores poderão utilizar como referência.

---

## A quem se destina

O programa está aberto a três perfis principais:

#### 🛠️ Builders Web3 com experiência prévia em Golem
Pessoas que já conhecem o protocolo e desejam construir um projeto mais ambicioso com respaldo financeiro e suporte direto da equipe.

#### 🌐 Builders Web3 sem experiência em Golem
Desenvolvedores ativos no ecossistema do Ethereum ou de outras redes descentralizadas que estejam explorando compute descentralizado pela primeira vez. Para esse perfil, o programa também funciona como onboarding pago ao protocolo.

#### 💻 Builders Web2
Desenvolvedores com experiência em backend, sistemas distribuídos, machine learning, processamento de mídias ou outros domínios técnicos relevantes que queiram experimentar um primeiro projeto sobre infraestrutura descentralizada.

> Não é necessário ter experiência prévia com Golem. É necessária capacidade técnica para construir, disposição para documentar o trabalho e disposição para publicar o resultado em aberto.

---

## O que os participantes constroem

O programa propõe cinco tracks orientados a diferentes tipos de demonstrações técnicas. Os tracks não são rígidos: funcionam como pontos de partida e referência para quem prefere um marco definido. Quem tiver uma ideia própria pode propô-la por meio do Track E, sujeita a aprovação prévia da equipe.

<div align="center">

| Track | Foco principal |
|:-----:|:---------------|
| **A** · [Parallel Media Processing](./docs/guia_builders.md#track-a) | Processamento paralelo de arquivos de áudio e vídeo em múltiplos providers |
| **B** · [Compute-Intensive Simulation](./docs/guia_builders.md#track-b) | Simulações numéricas, Monte Carlo e cálculos científicos em escala |
| **C** · [Provider Reputation & Benchmarking](./docs/guia_builders.md#track-c) | Ferramentas de medição, scoring e benchmarking de providers |
| **D** · [Chess Engine / Game AI at Scale](./docs/guia_builders.md#track-d) | Inteligência artificial de jogos como demonstração legível de paralelismo |
| **E** · [Open Track](./docs/guia_builders.md#track-e) | Proposta livre do builder, validada antes do início |

</div>

A descrição completa de cada track, incluindo direções técnicas sugeridas, exemplos de projetos prévios e entregáveis esperados, encontra-se no [**Builders Guide**](./docs/guia_builders.md).

---

## Processo de participação

O programa opera sob um fluxo de cinco etapas projetado para minimizar o atrito tanto para o builder quanto para a equipe da Golem.

```
  ┌───────────┐    ┌──────────┐    ┌──────────┐    ┌─────────────┐    ┌──────────────┐
  │  1. Read  │ →  │ 2. Pitch │ →  │ 3. Review│ →  │  4. Build   │ →  │  5. Deliver  │
  │   Guide   │    │  Submit  │    │ Approval │    │  & Iterate  │    │   & Get Paid │
  └───────────┘    └──────────┘    └──────────┘    └─────────────┘    └──────────────┘
```

### 1. Leitura do Builders Guide

O primeiro passo consiste em revisar o [Builders Guide](./docs/guia_builders.md). Essa leitura permite identificar o track adequado e calibrar o escopo do projeto.

### 2. Envio do pitch

O builder apresenta sua proposta por meio do **formulário oficial de pitch**: *[pendente]*.

A proposta deve seguir a estrutura da [plantilla de pitch](./docs/pitch_template.md) e incluir, no mínimo: track escolhido, descrição do projeto, escopo técnico, plano de trabalho, entregáveis e experiência prévia relevante. Uma página costuma ser suficiente.

### 3. Revisão e aprovação

A equipe da Golem revisa cada pitch internamente e responde com uma de três possibilidades: aprovação direta, solicitação de ajustes no escopo, ou rejeição com justificativa.

Uma vez aprovado o pitch, o escopo do projeto, os entregáveis e o bounty associado são confirmados formalmente.

### 4. Desenvolvimento

O builder desenvolve o projeto em seu próprio repositório público no GitHub. Durante essa etapa, a equipe da Golem está disponível no Discord para resolver dúvidas técnicas, revisar avanços e orientar sobre o uso do protocolo. O prazo típico de desenvolvimento é de **duas a quatro semanas**, ajustável conforme a complexidade acordada no pitch.

### 5. Entrega e pagamento

Ao finalizar o desenvolvimento, o builder entrega seu projeto seguindo o [submission guide](./docs/submission-guide.md). A entrega inclui o repositório público com README claro, métricas reais de execução sobre Golem e um breve write-up explicativo orientado à comunidade. Uma vez validado o entregável, o bounty é transferido diretamente à wallet do builder em **$GLM**.

---

## O que a Golem aporta e o que se espera do builder

O programa funciona como uma colaboração estruturada com compromissos claros de ambas as partes.

<table>
<tr>
<th width="50%">🟦 O que a Golem Network aporta</th>
<th width="50%">🟨 O que se espera do builder</th>
</tr>
<tr>
<td valign="top">

- Financiamento por projeto sem cotas nem limites de participação
- Acesso direto à equipe técnica para consultas, revisões e debugging
- Co-promoção do projeto finalizado pelos canais oficiais e comunidades parceiras
- Flexibilidade de escopo para favorecer a qualidade técnica em vez do cumprimento mecânico de um track

</td>
<td valign="top">

- Compromisso real com a entrega do projeto no escopo acordado
- Código publicado no GitHub sob licença aberta com documentação clara
- Comunicação proativa durante o desenvolvimento, especialmente quando surgirem bloqueios ou ajustes
- Write-up final que permita a outros desenvolvedores entender e reproduzir o trabalho

</td>
</tr>
</table>

---

## Recursos do repositório

| Documento | Propósito |
|-----------|-----------|
| [📘 Builders Guide](./docs/guia_builders.md) | Descrição completa dos cinco tracks, exemplos e entregáveis |
| [📝 Pitch Template](./docs/pitch_template.md) | Plantilla recomendada para estruturar o pitch |
| [📦 Submission Guide](./docs/submission-guide.md) | Requisitos formais para a entrega do projeto |
| [❓ FAQ](./FAQ.md) | Perguntas frequentes sobre o programa |

> 🇬🇧 **English version:** [`/en/README.md`](../en/README.md) · 🇪🇸 **Versión en español:** [`/es/README.md`](../es/README.md)

---

## Projetos anteriores

À medida que projetos forem completados dentro do programa, esta seção será atualizada com links para os repositórios e descrições de cada um.

Como referência prévia ao programa, [**gScribe**](https://gscribe.ai/) é um exemplo de projeto construído sobre Golem que demonstra o caso de uso de transcrição paralela de áudio por meio de Whisper distribuído entre múltiplos providers.

---

## Comunidades parceiras

O programa é desenvolvido em colaboração com comunidades de builders na América Latina e em outras regiões. As comunidades parceiras ajudam a difundir o programa entre seus desenvolvedores, e cada projeto finalizado por um builder de sua comunidade recebe co-promoção em seus canais.

> *Comunidades atualmente envolvidas: a confirmar.*

---

## Contato

Para consultas sobre o programa antes de enviar um pitch, o canal recomendado é o Discord oficial da Golem no canal de builders:

<div align="center">

[![Join Discord](https://img.shields.io/badge/Junte--se%20ao%20canal%20de%20builders-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/golem)

</div>

---

<div align="center">

<img src="../assets/golem-logo.png" alt="Golem" width="60" />

**Powered by $GLM · Built for Ethereum · Open to everyone**

<sub>© Golem Network · Community Builder Programme</sub>

</div>
