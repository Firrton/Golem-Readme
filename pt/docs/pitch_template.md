# Pitch Template

## Descrição dos campos

### 1. Informações de contato

O pitch deve abrir com as informações básicas que permitam à equipe do programa identificar o builder e estabelecer comunicação durante o processo de revisão e desenvolvimento.

Para builders individuais, os campos exigidos são nome completo, endereço de e-mail, identificador do Discord e link para o perfil do GitHub ou portfólio profissional. O endereço de wallet não é solicitado no pitch, mas sim no momento da entrega final do projeto.

Para equipes, deve ser designado um único ponto de contato responsável pela comunicação com a equipe do programa. O pitch também deve listar os demais membros da equipe com nome completo, papel previsto no projeto e link para perfil profissional ou GitHub. A distribuição interna do bounty está fora do escopo do programa e deve ser acordada internamente entre os membros da equipe.

### 2. Track e título do projeto

O builder deve indicar de forma explícita qual dos cinco tracks corresponde à sua proposta: Track A (Parallel Media Processing), Track B (Compute-Intensive Simulation), Track C (Provider Reputation & Benchmarking), Track D (Chess Engine / Game AI at Scale) ou Track E (Open Track). Essa classificação facilita a avaliação interna e permite à equipe identificar rapidamente o contexto técnico da proposta.

O título tentativo do projeto pode ser ajustado durante o desenvolvimento, mas convém propor um desde o pitch para facilitar a comunicação posterior.

### 3. Descrição do projeto

Esse campo é o coração do pitch. Em um ou dois parágrafos, o builder deve explicar o que será construído, que problema ou caso de uso aborda, e o que torna o projeto interessante a partir da perspectiva do compute descentralizado.

A descrição deve ser compreensível para um leitor que conheça a Golem mas não tenha lido outra documentação prévia sobre o projeto. Deve responder com clareza a três perguntas básicas: o que será construído, como a Golem será usada dentro do projeto, e que tipo de demonstração técnica produz o resultado final.

### 4. Escopo técnico

Esta seção detalha as decisões técnicas concretas que o builder tomou ao planejar o projeto. Deve cobrir quatro elementos.

O primeiro é o SDK que será utilizado: `@golem-sdk/task-executor` como caminho principal recomendado para a maioria dos projetos, ou `@golem-sdk/golem-js` 3.x quando o projeto requeira controle fino sobre a lógica de mercado ou seleção de providers. Se o builder propuser trabalhar com um SDK distinto do ecossistema JavaScript, deve justificá-lo explicitamente.

O segundo é a rede sobre a qual o projeto será executado: testnet hoodi para a maioria dos casos, ou mainnet quando o projeto requeira demonstrar comportamento econômico real.

O terceiro é o stack auxiliar relevante: linguagens de programação, bibliotecas externas, ferramentas de paralelização ou qualquer dependência técnica significativa que a equipe deva conhecer para avaliar a viabilidade.

O quarto são as decisões de arquitetura específicas, particularmente aquelas relacionadas com a paralelização do trabalho: como a tarefa será dividida em unidades distribuíveis, como os resultados serão agregados, e como serão tratados erros ou providers não responsivos.

### 5. Plano de trabalho

O builder deve propor uma divisão do projeto em fases ou marcos, com tempos estimados para cada um. Não é exigido um cronograma detalhado: uma divisão aproximada que demonstre que o builder pensou em como distribuir o trabalho ao longo das duas a quatro semanas previstas é suficiente.

Uma divisão típica para um projeto de três semanas poderia incluir uma primeira semana de configuração do ambiente, exploração do SDK e construção da primeira prova de conceito; uma segunda semana de desenvolvimento do componente paralelizado e validação de resultados; e uma terceira semana de polimento, documentação, geração de métricas finais e preparação do entregável.

### 6. Entregáveis previstos

O builder deve especificar o que o repositório terá ao final do projeto, que métricas serão documentadas, e que tipo de demonstração ou evidência será produzida. Esses entregáveis devem alinhar-se com os descritos no track correspondente do [Builders Guide](./guia_builders.md), embora possam incluir elementos adicionais próprios da proposta.

Para projetos com componente visual, convém antecipar se será incluída demo ao vivo, capturas de tela, GIFs animados ou vídeo explicativo. Para projetos com componente quantitativo, convém antecipar que tipo de visualizações ou tabelas de resultados acompanharão o entregável.

### 7. Experiência prévia relevante

Esta seção permite à equipe avaliar a capacidade de execução do builder. Deve descrever brevemente o background técnico relevante para o projeto, sem necessidade de um currículo exaustivo.

Os elementos úteis a mencionar incluem experiência no domínio do projeto (por exemplo, processamento de mídias para Track A, finanças computacionais para Track B), experiência prévia com Golem se houver, projetos similares construídos previamente, e links para repositórios ou demos que demonstrem a capacidade técnica do builder ou equipe.

Para builders sem experiência prévia com Golem, esta seção não é um obstáculo: o programa está explicitamente aberto a desenvolvedores novos no protocolo. O que se avalia é a capacidade técnica geral para executar o projeto proposto, não a familiaridade prévia com Golem.

### 8. Notas adicionais

Seção aberta onde o builder pode incluir qualquer informação que ajude a equipe a avaliar a proposta e que não se encaixe naturalmente nos campos anteriores. Os usos típicos incluem riscos identificados que o builder antecipa, decisões de escopo que o builder quer validar antes de começar, dependências externas que podem afetar a viabilidade do projeto, perguntas específicas dirigidas à equipe, ou qualquer contexto adicional relevante.

Esta seção é opcional. Pitches sem notas adicionais são perfeitamente válidos quando o restante do conteúdo é suficientemente claro.

---

## Plantilla limpa

A seguir é apresentada a plantilla em formato pronto para copiar e completar. Os campos entre colchetes devem ser substituídos pela informação correspondente.

```
GOLEM COMMUNITY BUILDER PROGRAMME — PITCH

1. INFORMAÇÕES DE CONTATO

Nome completo: [nome do builder ou ponto de contato da equipe]
E-mail: [endereço de e-mail]
Discord: [identificador do Discord]
GitHub ou portfólio: [link para perfil profissional]

Tipo de candidatura:
[ ] Builder individual
[ ] Equipe

Se aplica como equipe, listar membros adicionais:
- [Nome]: [papel no projeto] — [link para perfil]
- [Nome]: [papel no projeto] — [link para perfil]

2. TRACK E TÍTULO DO PROJETO

Track escolhido:
[ ] Track A — Parallel Media Processing
[ ] Track B — Compute-Intensive Simulation
[ ] Track C — Provider Reputation & Benchmarking
[ ] Track D — Chess Engine / Game AI at Scale
[ ] Track E — Open Track

Título tentativo do projeto: [título]

3. DESCRIÇÃO DO PROJETO

[Um ou dois parágrafos que expliquem o que será construído, que
problema ou caso de uso aborda, e o que torna o projeto interessante
a partir da perspectiva do compute descentralizado.]

4. ESCOPO TÉCNICO

SDK a utilizar:
[ ] @golem-sdk/task-executor
[ ] @golem-sdk/golem-js 3.x
[ ] Outro: [especificar e justificar]

Rede de execução:
[ ] Testnet (hoodi)
[ ] Mainnet

Stack auxiliar relevante:
[Linguagens, bibliotecas, ferramentas externas e dependências
técnicas significativas.]

Decisões de arquitetura:
[Como o trabalho será dividido em unidades paralelizáveis, como
serão agregados os resultados, e como serão tratados erros ou
providers não responsivos.]

5. PLANO DE TRABALHO

Duração estimada: [número de semanas]

Marcos previstos:
- Semana 1: [atividades principais]
- Semana 2: [atividades principais]
- Semana 3: [atividades principais]
- Semana 4 (se aplicável): [atividades principais]

6. ENTREGÁVEIS PREVISTOS

Repositório:
[O que o repositório terá ao final do projeto.]

Métricas a documentar:
[Que métricas serão reportadas e como serão obtidas.]

Demonstração ou evidência:
[Tipo de demo, capturas, GIFs, vídeo ou visualizações que
acompanharão o entregável.]

7. EXPERIÊNCIA PRÉVIA RELEVANTE

[Breve descrição do background técnico relevante para o projeto.
Mencionar experiência no domínio, experiência prévia com Golem
se houver, e links para projetos prévios se aplicável.]


8. NOTAS ADICIONAIS (OPCIONAL)

[Riscos identificados, decisões de escopo a validar, dependências
externas, perguntas para a equipe, ou qualquer contexto adicional
relevante. Esta seção é opcional.]
```

---

## Próximos passos

Uma vez completada a plantilla, o pitch deve ser enviado por meio do **formulário oficial do programa**: [pendente]. O formulário está estruturado de maneira coerente com esta plantilla, portanto a transferência da informação é direta.

A equipe do programa revisa cada pitch e responde com uma de três possibilidades: aprovação direta, solicitação de ajustes no escopo, ou rejeição com justificativa. A política completa de revisão está descrita no [README](../README.md) geral do repositório.

Para consultas prévias ao envio do pitch, o canal recomendado é o Discord oficial da Golem em [discord.gg/golem](https://discord.gg/golem).
