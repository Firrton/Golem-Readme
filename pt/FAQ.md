# Perguntas Frequentes

Documento de referência que reúne as perguntas mais habituais sobre o **Golem Community Builder Programme**. É concebido como complemento ao restante da documentação do repositório e como ponto de partida antes de canalizar consultas específicas à equipe do programa ou à comunidade técnica da Golem.

As respostas aqui incluídas refletem a política vigente do programa no momento da última atualização do documento. Para situações particulares não contempladas no FAQ, os canais de comunicação oficiais são detalhados ao final do documento.

---

## Sobre o programa

**O que é exatamente o Golem Community Builder Programme?**

O programa é uma iniciativa aberta e contínua que financia projetos técnicos construídos sobre a Golem Network. Cada projeto aprovado recebe um bounty de 500 USD pagos em $GLM, com duração estimada entre duas e quatro semanas de desenvolvimento. Diferentemente de um hackathon tradicional, o programa não opera sob pressão de prazos finais nem por meio de competições de pitch, mas sim financia trabalho técnico genuíno sobre o protocolo. A descrição completa do programa encontra-se no [README](./README.md).

**Em que se diferencia este programa de um hackathon?**

A diferença principal é estrutural. Um hackathon tem data de início e fim, exige aos participantes completar o trabalho dentro de um prazo comprimido e costuma entregar prêmios apenas aos projetos vencedores após uma competição. Este programa não tem deadline fixo, opera de forma contínua, e paga o bounty completo a todo projeto aprovado que cumpra os entregáveis acordados. A filosofia é financiar trabalho técnico de qualidade em vez de produzir competição entre builders.

**Quem pode participar?**

O programa está aberto a desenvolvedores Web3 com ou sem experiência prévia em Golem, assim como a desenvolvedores Web2 que estejam explorando compute descentralizado pela primeira vez. Não são exigidas credenciais formais nem afiliação a uma organização específica. É exigida capacidade técnica para construir o projeto proposto e disposição para publicar o resultado sob licença aberta.

**É possível formar equipes para participar?**

Sim. O programa aceita tanto builders individuais quanto equipes sem limite explícito de tamanho. As equipes devem designar um único ponto de contato para a comunicação com a equipe da Golem e definir internamente como distribuirão o bounty entre seus membros. O bounty é transferido a um único endereço de wallet, e a distribuição posterior está fora do escopo do programa.

**Posso participar em múltiplos projetos ao longo do tempo?**

A participação em múltiplos projetos é avaliada caso a caso pela equipe do programa. Builders que tenham completado satisfatoriamente um projeto prévio podem ser convidados ou autorizados a apresentar novas propostas, dependendo da qualidade do trabalho prévio, do intervalo transcorrido e da disponibilidade de vagas no programa. A política busca equilibrar o reconhecimento ao trabalho recorrente de builders comprometidos com a abertura do programa a novos participantes.

---

## Sobre os aspectos técnicos

**Preciso ter experiência prévia com Golem para participar?**

Não. O programa está explicitamente desenhado para acolher tanto builders com experiência prévia quanto desenvolvedores que estão se encontrando com Golem pela primeira vez. Para builders novos, o [Builders Guide](./docs/guia_builders.md) oferece direções de projeto com complexidade estimada para facilitar a escolha inicial.

**Que SDK devo usar para construir meu projeto?**

O caminho principal recomendado é `@golem-sdk/task-executor`, uma biblioteca em JavaScript e TypeScript orientada a padrões map-reduce e paralelização de tarefas. Para builders com necessidades mais específicas ou experiência prévia em sistemas distribuídos, `@golem-sdk/golem-js` 3.x oferece acesso direto aos modelos de baixo nível do protocolo. A discussão completa sobre quando escolher cada opção encontra-se na seção de Notas Técnicas Comuns do [Builders Guide](./docs/guia_builders.md).

**Posso trabalhar em testnet ou tenho que usar mainnet?**

Ambas as redes são válidas para entrega do programa. A testnet, que atualmente opera sobre a rede hoodi, é o ambiente recomendado para a maioria dos projetos, dado que permite executar trabalho real sobre a rede sem custo real. A mainnet é apropriada quando o projeto requer demonstrar comportamento econômico real ou integrações com sistemas de produção. A escolha deve ser explicitada no pitch.

**Há suporte para linguagens diferentes de JavaScript e TypeScript?**

O stack da Golem conta com SDKs em outras linguagens, mas a documentação mais atualizada e os exemplos oficiais concentram-se no ecossistema JavaScript. Os builders que prefiram trabalhar em outra linguagem podem fazê-lo, mas devem levar em conta que a curva de aprendizado e o suporte disponível são menores. Recomenda-se discutir essa decisão durante a fase de pitch.

**Posso usar GPU em meu projeto?**

A Golem oferece acesso a providers com GPU, embora a disponibilidade possa ser variável conforme o momento e o tipo de hardware exigido. Os projetos que dependam criticamente de GPU devem mencionar essa dependência no pitch para que a equipe possa confirmar a viabilidade antes da aprovação.

---

## Sobre o processo do programa

**Quanto tempo a equipe leva para revisar um pitch?**

O prazo concreto de resposta depende do volume de pitches recebidos a cada momento. A equipe do programa busca responder com a maior agilidade razoável e notifica o builder assim que a decisão é tomada.

**O que acontece se meu pitch for rejeitado?**

As decisões sobre pitches rejeitados ficam a critério da equipe do programa. Em alguns casos, a rejeição pode ser acompanhada de comentários específicos que permitem ao builder ajustar a proposta e reenviá-la. Em outros casos, pode-se recomendar ao builder explorar uma direção alternativa ou esperar antes de apresentar uma nova proposta. A decisão específica é comunicada diretamente ao builder no momento da rejeição.

**Posso modificar o escopo do projeto durante o desenvolvimento?**

Mudanças menores no escopo, motivadas por descobertas técnicas durante o desenvolvimento, são habituais e aceitáveis sempre que sejam comunicadas à equipe do programa. Mudanças substanciais que alterem a natureza do projeto requerem acordo explícito com a equipe antes de prosseguir. A comunicação proativa durante o desenvolvimento é uma expectativa formal do programa e está documentada no [README](./README.md).

**O que acontece se eu não conseguir completar o projeto?**

As situações de projetos não completados são avaliadas caso a caso pela equipe do programa. Quando o builder manteve comunicação durante o desenvolvimento e existem circunstâncias técnicas genuínas que impediram a finalização, a equipe pode considerar pagamentos parciais proporcionais ao avanço demonstrável ou reorientar o projeto para um escopo reduzido. Em situações de abandono sem comunicação, não procede o pagamento do bounty. A política do programa busca proteger tanto o builder diante de dificuldades genuínas quanto a equipe diante de entregas não completadas.

**Posso apresentar um pitch sem ter lido todos os documentos do repositório?**

É tecnicamente possível, mas não recomendado. A qualidade do pitch e a velocidade de aprovação dependem diretamente de o builder ter compreendido os critérios do programa, as direções de cada track e os requisitos do entregável. Os pitches de builders que evidenciam conhecimento da documentação recebem menor quantidade de pedidos de ajuste e avançam com maior rapidez no processo.

---

## Sobre a propriedade intelectual e a difusão

**Quem é dono do repositório e do código?**

O builder mantém plena propriedade do repositório e do código, publicado sob a licença open source escolhida. O programa não reivindica direitos exclusivos sobre o trabalho financiado e não exige transferência do repositório a uma organização da Golem.

**Posso usar o projeto para meu portfólio ou continuar desenvolvendo-o?**

Sim. O builder está livre para usar o projeto para portfólio profissional, apresentações públicas, candidaturas a empregos, continuação do desenvolvimento, e inclusive evolução do projeto para produtos comerciais. O programa fomenta explicitamente que os projetos financiados continuem crescendo para além do bounty inicial.

**Que difusão a Golem faz do projeto?**

Uma vez validado o entregável, a equipe coordena a difusão do projeto pelos canais oficiais da Golem e pelas comunidades parceiras correspondentes. Isso inclui publicação no Discord oficial, menção em redes sociais do projeto quando aplicável, e inclusão do repositório como referência dentro do ecossistema. A difusão específica varia conforme o tipo de projeto e o momento do programa.

**Posso apresentar o projeto em eventos ou conferências?**

Sim. O builder está livre para apresentar seu trabalho em qualquer evento, hackathon ou conferência, mencionando que foi construído no marco do Golem Community Builder Programme. Quando aplicável, a equipe do programa pode facilitar contatos ou informações adicionais para apoiar esse tipo de apresentações.

---

## Canais de suporte e consultas

Para perguntas não cobertas neste documento, os canais recomendados se diferenciam conforme a natureza da consulta.

Para consultas específicas sobre o programa, a primeira opção é o canal de Discord dedicado ao builder programme dentro do servidor oficial da Golem, onde a equipe do programa atende dúvidas sobre tracks, pitches, escopo, entrega, pagamentos e qualquer aspecto operacional da iniciativa.

Para consultas técnicas sobre o protocolo Golem em si, independentemente do programa, a opção adequada é o canal `❓question-answers` ou equivalente do servidor oficial da Golem, onde a comunidade técnica mais ampla e a equipe de protocolo respondem dúvidas sobre o SDK, yagna, providers, infraestrutura e outros aspectos técnicos gerais.

Para aprofundar em aspectos técnicos antes de levantar uma consulta, a documentação oficial da Golem em [docs.golem.network](https://docs.golem.network) constitui o recurso de referência principal e costuma responder à maioria das dúvidas técnicas habituais sem necessidade de canalizá-las por chat.

O acesso ao servidor oficial do Discord é feito a partir de [discord.gg/golem](https://discord.gg/golem).
