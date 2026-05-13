# Perguntas Frequentes

## Sobre o programa

**O que é exatamente o Golem Community Builder Programme?**

O programa é uma iniciativa aberta e contínua que financia projectos técnicos construídos sobre a Golem Network. Cada projecto aprovado recebe um bounty de 500 USD pagos em $GLM, com duração estimada entre duas e quatro semanas de desenvolvimento. A descrição completa do programa encontra-se no [README](./README.md).

**Em que se diferencia este programa de um hackathon?**

O programa é aberto e sem prazo: não há competição de pitch nem runners-up. Os builders submetem as suas próprias ideias através do formulário de candidatura. A equipa da Golem revê as candidaturas de forma contínua e selecciona as mais sólidas. Para os projectos seleccionados, o builder e a equipa acordam juntos o âmbito — e só depois começa o desenvolvimento.

**Quem pode participar?**

Qualquer programador com capacidade técnica para entregar um projecto real: perfil Web2 ou Web3, com ou sem experiência prévia em Golem.

**É possível formar equipes para participar?**

Sim. O programa aceita tanto builders individuais como equipas sem limite de tamanho. As equipas devem designar um único ponto de contacto para a comunicação com a equipa da Golem e definir internamente como distribuirão o bounty entre os seus membros. O bounty é transferido para um único endereço de wallet, e a distribuição posterior está fora do âmbito do programa.

**Posso participar em múltiplos projetos ao longo do tempo?**

Um projecto por equipa de cada vez. Após a validação da entrega e o pagamento do bounty, a mesma equipa pode candidatar-se novamente com uma nova ideia.

---

## Sobre os aspectos técnicos

**Preciso ter experiência prévia com Golem para participar?**

Não é necessária experiência prévia com Golem. A equipe está disponível no Discord para orientar sobre o protocolo durante o desenvolvimento.

**Que SDK devo usar para construir meu projeto?**

O caminho principal recomendado é `@golem-sdk/task-executor`, uma biblioteca em JavaScript e TypeScript orientada a padrões map-reduce e paralelização de tarefas. Para builders com necessidades mais específicas ou experiência prévia em sistemas distribuídos, `@golem-sdk/golem-js` 3.x oferece acesso direto aos modelos de baixo nível do protocolo. A discussão completa sobre quando escolher cada opção encontra-se na seção de Notas Técnicas Comuns do [Builders Guide](./docs/guia_builders.md).

**Posso trabalhar em testnet ou tenho que usar mainnet?**

O esperado por defeito é que os builders iterem em testnet (actualmente `hoodi`). Não há qualquer expectativa de mainnet. Se a mainnet for genuinamente necessária para um projecto, isso é acordado entre a equipa seleccionada e a equipa da Golem no momento do scoping.

**Há suporte para linguagens diferentes de JavaScript e TypeScript?**

O stack da Golem conta com SDKs em outras linguagens, mas a documentação mais atualizada e os exemplos oficiais concentram-se no ecossistema JavaScript. Os builders que prefiram trabalhar em outra linguagem podem fazê-lo, mas devem levar em conta que a curva de aprendizado e o suporte disponível são menores. Recomenda-se discutir essa decisão durante a fase de candidatura.

**Posso usar GPU em meu projeto?**

A Golem oferece acesso a providers com GPU, embora a disponibilidade possa ser variável conforme o momento e o tipo de hardware exigido. Os projetos que dependam criticamente de GPU devem mencionar essa dependência no formulário de candidatura para que a equipe possa confirmar a viabilidade antes da aprovação.

---

## Sobre o processo do programa

**Quanto tempo demora a equipa a responder após a candidatura?**

A equipa da Golem revê as candidaturas de forma contínua, pelo que não há uma janela de resposta fixa. Serás notificado assim que for tomada uma decisão. Se a ideia se enquadrar no programa, a equipa entra em contacto para discutir o âmbito e os marcos antes de o desenvolvimento começar.

**O que acontece se a minha candidatura for rejeitada?**

As decisões sobre candidaturas rejeitadas ficam ao critério da equipa do programa. Procuramos partilhar feedback quando possível, mas dado o volume de candidaturas não podemos garantir que isso aconteça em todos os casos.

**Posso modificar o escopo do projeto durante o desenvolvimento?**

Alterações menores no âmbito, motivadas por descobertas técnicas durante o desenvolvimento, são habituais e aceitáveis desde que sejam comunicadas à equipa do programa. Alterações substanciais que alterem a natureza do projecto requerem acordo explícito com a equipa antes de prosseguir.

**O que acontece se eu não conseguir completar o projeto?**

As situações de projectos não concluídos são avaliadas caso a caso pela equipa do programa.

---

## Sobre a propriedade intelectual e a difusão

**Quem é dono do repositório e do código?**

O builder mantém plena propriedade do repositório e do código, publicado sob a licença open source escolhida. O programa não reivindica direitos exclusivos sobre o trabalho financiado e não exige a transferência do repositório para uma organização da Golem.

Ao submeter um projecto ao programa, o builder autoriza a Golem a mencionar, partilhar e dar destaque ao projecto nos seus canais para fins de marketing e promoção do ecossistema.

**Posso usar o projeto para meu portfólio ou continuar desenvolvendo-o?**

Sim. O builder está livre para usar o projeto para portfólio profissional, apresentações públicas, candidaturas a empregos, continuação do desenvolvimento, e inclusive evolução do projeto para produtos comerciais. O programa fomenta explicitamente que os projetos financiados continuem crescendo para além do bounty inicial.

**Como é que a Golem divulga o projecto?**

Assim que o entregável é validado, a equipa partilha o projecto pelos canais oficiais da Golem: uma publicação no Discord, uma menção nas redes sociais quando se justificar, e a adição do repositório à lista de referências do ecossistema. O que fazemos concretamente depende do projecto.

**Posso apresentar o projeto em eventos ou conferências?**

Sim. O builder está livre para apresentar o seu trabalho em qualquer evento, hackathon ou conferência. Quando aplicável, a equipa do programa pode facilitar contactos ou informações adicionais para apoiar esse tipo de apresentações.

---

## Suporte e canais

- **Perguntas sobre o programa** (tracks, candidaturas, âmbito, entrega, pagamentos): canal `builders` no Discord oficial da Golem.
- **Questões técnicas sobre a Golem** (SDK, yagna, providers, infraestrutura): canal `❓question-answers` no mesmo Discord.
- **Antes de perguntar, consulta a documentação**: [docs.golem.network](https://docs.golem.network) cobre a maioria das questões técnicas habituais.

Junta-te ao Discord em [discord.gg/golem](https://discord.gg/golem).

---

## Perguntas adicionais

**Preciso preparar um documento de pitch ou um template para me candidatar?**

Não. As candidaturas são feitas através do formulário oficial em https://forms.golem.network/golem-builders-programme. O formulário recolhe o track, a ideia, a abordagem técnica e a experiência relevante. Não há nenhum documento de pitch separado para redigir ou enviar.

**O que deve mostrar o vídeo demo de 2–3 minutos?**

Uma gravação breve do projeto a funcionar na prática — suficiente para que alguém sem conhecimento prévio do trabalho compreenda o que faz e como usa a Golem. O vídeo é um entregável obrigatório e é utilizado para amplificação nos canais oficiais da Golem.

**Quando o bounty é pago em $GLM, como é feita a conversão do valor em USD?**

O bounty é denominado em 500 USD e pago em $GLM. O valor em $GLM é fixado pela cotação no dia do pagamento, de modo que o equivalente em USD nesse momento corresponde ao bounty acordado. Os builders fornecem um endereço de wallet e a rede em que desejam receber (Polygon ou Ethereum mainnet); o $GLM é transferido diretamente.

**Posso usar ferramentas de IA ou assistentes de código enquanto construo?**

Sim. O entregável é o projeto a funcionar, a documentação e o vídeo demo. A forma como o constróis é decisão tua — assistentes de código com IA, ferramentas de pair programming ou qualquer outro recurso. O que importa é que o código seja teu para publicar sob licença aberta, que o relatório técnico reflita a tua compreensão do trabalho e que o projeto realmente execute na Golem.

**Posso fazer um fork de um projeto Golem existente para a minha candidatura?**

Forks são aceites apenas como ponto de partida e somente com trabalho novo substancial acrescentado. Um fork puro com alterações menores não qualifica. Se tiveres dúvidas sobre se a tua proposta conta como trabalho substancial, menciona-o no formulário de candidatura — a equipe dirá de antemão.
