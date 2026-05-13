# Perguntas Frequentes

Documento de referência que reúne as perguntas mais habituais sobre o **Golem Community Builder Programme**. É concebido como complemento ao restante da documentação do repositório e como ponto de partida antes de canalizar consultas específicas à equipe do programa ou à comunidade técnica da Golem.

As respostas aqui incluídas refletem a política vigente do programa no momento da última atualização do documento. Para situações particulares não contempladas no FAQ, os canais de comunicação oficiais são detalhados ao final do documento.

---

## Sobre o programa

**O que é exatamente o Golem Community Builder Programme?**

O programa é uma iniciativa aberta e contínua que financia projetos técnicos construídos sobre a Golem Network. Cada projeto aprovado recebe um bounty de 500 USD pagos em $GLM, com duração estimada entre duas e quatro semanas de desenvolvimento. Diferentemente de um hackathon tradicional, o programa não opera sob pressão de prazos finais nem por meio de competições de pitch, mas sim financia trabalho técnico genuíno sobre o protocolo. A descrição completa do programa encontra-se no [README](./README.md).

**Em que se diferencia este programa de um hackathon?**

O programa é contínuo, sem prazos nem julgamento competitivo. A equipe da Golem financia projetos com escopo claramente definido que demonstrem o protocolo, e todo projeto aprovado recebe o bounty — não há finalistas.

**Quem pode participar?**

Qualquer desenvolvedor com capacidade técnica para entregar um projeto real: perfil Web2 ou Web3, com ou sem experiência prévia em Golem. Não são exigidas credenciais nem afiliações.

**É possível formar equipes para participar?**

Sim. O programa aceita tanto builders individuais quanto equipes sem limite explícito de tamanho. As equipes devem designar um único ponto de contato para a comunicação com a equipe da Golem e definir internamente como distribuirão o bounty entre seus membros. O bounty é transferido a um único endereço de wallet, e a distribuição posterior está fora do escopo do programa.

**Posso participar em múltiplos projetos ao longo do tempo?**

Um projeto por equipe de cada vez. Após a validação da entrega e o pagamento do bounty, a mesma equipe pode candidatar-se novamente com uma nova ideia. Fazemos isso para que a atenção da equipe permaneça num projeto bem definido, não em vários em paralelo.

---

## Sobre os aspectos técnicos

**Preciso ter experiência prévia com Golem para participar?**

Não é necessária experiência prévia com Golem. A equipe está disponível no Discord para orientar sobre o protocolo durante o desenvolvimento.

**Que SDK devo usar para construir meu projeto?**

O caminho principal recomendado é `@golem-sdk/task-executor`, uma biblioteca em JavaScript e TypeScript orientada a padrões map-reduce e paralelização de tarefas. Para builders com necessidades mais específicas ou experiência prévia em sistemas distribuídos, `@golem-sdk/golem-js` 3.x oferece acesso direto aos modelos de baixo nível do protocolo. A discussão completa sobre quando escolher cada opção encontra-se na seção de Notas Técnicas Comuns do [Builders Guide](./docs/guia_builders.md).

**Posso trabalhar em testnet ou tenho que usar mainnet?**

Ambas as redes são válidas para entrega do programa. A testnet, que atualmente opera sobre a rede hoodi, é o ambiente recomendado para a maioria dos projetos, dado que permite executar trabalho real sobre a rede sem custo real. A mainnet é apropriada quando o projeto requer demonstrar comportamento econômico real ou integrações com sistemas de produção. A escolha deve ser explicitada no formulário de candidatura.

**Há suporte para linguagens diferentes de JavaScript e TypeScript?**

O stack da Golem conta com SDKs em outras linguagens, mas a documentação mais atualizada e os exemplos oficiais concentram-se no ecossistema JavaScript. Os builders que prefiram trabalhar em outra linguagem podem fazê-lo, mas devem levar em conta que a curva de aprendizado e o suporte disponível são menores. Recomenda-se discutir essa decisão durante a fase de candidatura.

**Posso usar GPU em meu projeto?**

A Golem oferece acesso a providers com GPU, embora a disponibilidade possa ser variável conforme o momento e o tipo de hardware exigido. Os projetos que dependam criticamente de GPU devem mencionar essa dependência no formulário de candidatura para que a equipe possa confirmar a viabilidade antes da aprovação.

---

## Sobre o processo do programa

**Quanto tempo a equipe leva para revisar uma candidatura?**

O nosso objetivo é responder dentro de 7 dias úteis. Se, num caso particular, esperarmos demorar mais (por exemplo, durante lançamentos do programa com alto volume de candidaturas), informaremos o builder no e-mail de confirmação de receção.

**O que acontece se minha candidatura for rejeitada?**

As decisões sobre candidaturas rejeitadas ficam a critério da equipe do programa. Em alguns casos, a rejeição pode ser acompanhada de comentários específicos que permitem ao builder ajustar a proposta e reenviá-la. Em outros casos, pode-se recomendar ao builder explorar uma direção alternativa ou esperar antes de apresentar uma nova proposta. A decisão específica é comunicada diretamente ao builder no momento da rejeição.

**Posso modificar o escopo do projeto durante o desenvolvimento?**

Mudanças menores no escopo, motivadas por descobertas técnicas durante o desenvolvimento, são habituais e aceitáveis sempre que sejam comunicadas à equipe do programa. Mudanças substanciais que alterem a natureza do projeto requerem acordo explícito com a equipe antes de prosseguir. A comunicação proativa durante o desenvolvimento é uma expectativa formal do programa e está documentada no [README](./README.md).

**O que acontece se eu não conseguir completar o projeto?**

As situações de projetos não completados são avaliadas caso a caso pela equipe do programa. Quando o builder manteve comunicação durante o desenvolvimento e existem circunstâncias técnicas genuínas que impediram a finalização, a equipe pode considerar pagamentos parciais proporcionais ao avanço demonstrável ou reorientar o projeto para um escopo reduzido. Em situações de abandono sem comunicação, não procede o pagamento do bounty. A política do programa busca proteger tanto o builder diante de dificuldades genuínas quanto a equipe diante de entregas não completadas.

---

## Sobre a propriedade intelectual e a difusão

**Quem é dono do repositório e do código?**

O builder mantém plena propriedade do repositório e do código, publicado sob a licença open source escolhida. O programa não reivindica direitos exclusivos sobre o trabalho financiado e não exige transferência do repositório a uma organização da Golem.

**Posso usar o projeto para meu portfólio ou continuar desenvolvendo-o?**

Sim. O builder está livre para usar o projeto para portfólio profissional, apresentações públicas, candidaturas a empregos, continuação do desenvolvimento, e inclusive evolução do projeto para produtos comerciais. O programa fomenta explicitamente que os projetos financiados continuem crescendo para além do bounty inicial.

**Que difusão a Golem faz do projeto?**

Uma vez validado o entregável, a equipe coordena a difusão do projeto pelos canais oficiais da Golem. Isso inclui publicação no Discord oficial, menção em redes sociais do projeto quando aplicável, e inclusão do repositório como referência dentro do ecossistema. A difusão específica varia conforme o tipo de projeto e o momento do programa.

**Posso apresentar o projeto em eventos ou conferências?**

Sim. O builder está livre para apresentar seu trabalho em qualquer evento, hackathon ou conferência, mencionando que foi construído no marco do Golem Community Builder Programme. Quando aplicável, a equipe do programa pode facilitar contatos ou informações adicionais para apoiar esse tipo de apresentações.

---

## Canais de suporte e consultas

Para perguntas não cobertas neste documento, os canais recomendados se diferenciam conforme a natureza da consulta.

Para consultas específicas sobre o programa, a primeira opção é o canal de builders no Discord oficial da Golem (discord.gg/golem), onde a equipe do programa atende dúvidas sobre tracks, candidaturas, escopo, entrega, pagamentos e qualquer aspecto operacional da iniciativa.

Para consultas técnicas sobre o protocolo Golem em si, independentemente do programa, a opção adequada é o canal `❓question-answers` ou equivalente do servidor oficial da Golem, onde a comunidade técnica mais ampla e a equipe de protocolo respondem dúvidas sobre o SDK, yagna, providers, infraestrutura e outros aspectos técnicos gerais.

Para aprofundar em aspectos técnicos antes de levantar uma consulta, a documentação oficial da Golem em [docs.golem.network](https://docs.golem.network) constitui o recurso de referência principal e costuma responder à maioria das dúvidas técnicas habituais sem necessidade de canalizá-las por chat.

O acesso ao servidor oficial do Discord é feito a partir de [discord.gg/golem](https://discord.gg/golem).

---

## Perguntas adicionais

**Preciso preparar um documento de pitch ou um template para me candidatar?**

Não. As candidaturas são feitas através do formulário oficial em https://forms.golem.network/golem-builders-programme. O formulário recolhe o track, a ideia, a abordagem técnica e a experiência relevante. Não há nenhum documento de pitch separado para redigir ou enviar.

**Quanto tempo demora a receber resposta após a candidatura?**

O nosso objetivo é responder dentro de 7 dias úteis. Se a ideia se enquadra no programa, a equipe entra em contacto para discutir os detalhes e os marcos antes de o desenvolvimento começar.

**O que deve mostrar o vídeo demo de 2–3 minutos?**

Uma gravação breve do projeto a funcionar na prática — suficiente para que alguém sem conhecimento prévio do trabalho compreenda o que faz e como usa a Golem. O vídeo é um entregável obrigatório e é utilizado para amplificação nos canais oficiais da Golem.

**Quando o bounty é pago em $GLM, como é feita a conversão do valor em USD?**

O bounty é denominado em 500 USD e pago em $GLM. O valor em $GLM é fixado pela cotação no dia do pagamento, de modo que o equivalente em USD nesse momento corresponde ao bounty acordado. Os builders fornecem um endereço de wallet e a rede em que desejam receber (Polygon ou Ethereum mainnet); o $GLM é transferido diretamente.

**Posso usar ferramentas de IA ou assistentes de código enquanto construo?**

Sim. O entregável é o projeto a funcionar, a documentação e o vídeo demo. A forma como o constróis é decisão tua — assistentes de código com IA, ferramentas de pair programming ou qualquer outro recurso. O que importa é que o código seja teu para publicar sob licença aberta, que o relatório técnico reflita a tua compreensão do trabalho e que o projeto realmente execute na Golem.

**Posso fazer um fork de um projeto Golem existente para a minha candidatura?**

Forks são aceites apenas como ponto de partida e somente com trabalho novo substancial acrescentado. Um fork puro com alterações menores não qualifica. Se tiveres dúvidas sobre se a tua proposta conta como trabalho substancial, menciona-o no formulário de candidatura — a equipe dirá de antemão.
