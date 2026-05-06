# Submission Guide

Documento de referência para a entrega formal de projetos dentro do **Builder Programme**. Define os critérios mínimos que um entregável deve cumprir, o procedimento de notificação à equipe da Golem, o processo de revisão e os passos para receber o pagamento do bounty.

A leitura deste documento é recomendada no início do desenvolvimento, não apenas no momento de entregar. Conhecer os requisitos da submissão desde o início permite ao builder estruturar o repositório e a documentação de forma incremental, evitando trabalho de última hora e assegurando que o entregável cumpra com os padrões do programa.

---

## Procedimento de entrega

A entrega formal de um projeto finalizado é feita por meio de e-mail dirigido à equipe do programa. Este é o canal oficial pelo qual se inicia o processo de revisão e se dispara o ciclo de validação que conduz ao pagamento do bounty.

O e-mail de entrega deve ser enviado ao endereço oficial do programa [pendente] e incluir, no mínimo, os seguintes elementos: identificação do builder e referência ao pitch aprovado previamente, link público para o repositório do projeto no GitHub, endereço de wallet do builder para a transferência do bounty com indicação explícita da rede sobre a qual o pagamento será feito, e qualquer nota relevante sobre o estado do projeto que a equipe deva conhecer antes de iniciar a revisão (por exemplo, limitações identificadas durante o desenvolvimento, decisões de escopo tomadas em consulta com a equipe, ou resultados particularmente notáveis que convém destacar).

De forma complementar, uma vez confirmada a recepção do e-mail e depois que o processo interno tenha avançado, o projeto será anunciado no Discord oficial da Golem com um resumo breve e os links correspondentes. O builder não precisa iniciar esse anúncio por conta própria: a equipe coordena a publicação nos canais correspondentes uma vez que a entrega tenha sido validada.

---

## Requisitos do repositório

O projeto deve viver em um repositório público no GitHub sob o usuário ou organização pessoal do builder.

O repositório deve estar publicado sob uma licença open source claramente indicada. A licença recomendada é **MIT**, dado que é a mais permissiva, a mais utilizada no ecossistema da Golem e a que melhor facilita a reutilização do trabalho pela comunidade. O arquivo `LICENSE` deve estar presente na raiz do repositório com o texto completo da licença e o nome do titular.

A estrutura do repositório deve permitir que um desenvolvedor externo possa clonar o projeto, instalar as dependências e executá-lo seguindo exclusivamente as instruções do README, sem necessidade de consultas adicionais. Isso implica que o código deve estar acompanhado de um arquivo de configuração de dependências padrão para a linguagem utilizada (`package.json` para Node.js, `requirements.txt` ou `pyproject.toml` para Python, conforme corresponda), dos scripts necessários para reproduzir as corridas documentadas no entregável, e de qualquer arquivo de configuração ou variável de ambiente exigida para a execução, devidamente documentada.

Recomenda-se evitar incluir credenciais, chaves privadas, arquivos de configuração local ou qualquer dado sensível no repositório. As variáveis que o builder deva configurar para rodar o projeto devem estar documentadas no README via um arquivo `.env.example` ou equivalente.

---

## Requisitos do README

O README do repositório constitui o principal documento voltado ao público e deve ser escrito com o cuidado correspondente. Cumpre simultaneamente a função de apresentação do projeto, instruções de uso para desenvolvedores que queiram reproduzi-lo, e write-up técnico que documenta o trabalho realizado.

O README deve abrir com uma descrição concisa do projeto que explique em poucas linhas o que faz, sobre que track do programa foi construído, e por que resulta interessante a partir da perspectiva do compute descentralizado. Esta seção inicial deve ser compreensível para um leitor que não tenha lido o pitch original.

Em seguida, deve ser incluída uma seção de instruções de instalação e execução, suficientemente detalhada para que um desenvolvedor externo possa reproduzir o projeto. Essa seção deve cobrir os requisitos prévios (versão do yagna, versão do Node.js ou outro runtime, dependências do sistema operacional se aplicável), o procedimento passo a passo de instalação e configuração, e os comandos exatos para executar o projeto e reproduzir os resultados documentados.

O corpo principal do README deve conter o write-up técnico do projeto. Esta seção documenta o que se construiu, como se desenhou a paralelização, que decisões técnicas se tomaram e por quê, que desafios se encontraram durante o desenvolvimento e como se resolveram, e que resultados se obtiveram. A extensão esperada é de várias seções bem estruturadas, suficientes para que um leitor técnico possa compreender o trabalho em profundidade sem necessidade de ler o código-fonte.

Uma seção dedicada deve apresentar as métricas e resultados da execução do projeto sobre Golem. Os critérios específicos sobre que métricas reportar e em que formato serão estabelecidos em uma versão posterior deste documento. Até lá, os builders devem reportar as métricas indicadas no track correspondente do [Builders Guide](./guia_builders.md) e qualquer dado adicional que considere relevante para demonstrar o funcionamento do projeto.

Por fim, o README deve fechar com uma breve seção que documente as limitações conhecidas do projeto, as possíveis direções de extensão que outros builders poderiam explorar a partir deste trabalho, e os créditos correspondentes ao builder e ao programa.

---

## Resumo para Discord

De forma complementar ao write-up extenso do README, o projeto deve ser acompanhado de um resumo breve desenhado para publicação no Discord oficial da Golem. Esse resumo não substitui o README, mas funciona como anúncio da entrega e porta de entrada para o repositório.

O resumo deve ser significativamente mais curto que o README, escrito em um registro acessível para uma audiência ampla que pode não ter contexto técnico profundo, e orientado a gerar interesse para consultar o repositório completo. A extensão recomendada é de um ou dois parágrafos que cubram o que se construiu, o que demonstra do protocolo, e onde encontrar o repositório para mais detalhes.

O builder deve enviar esse resumo junto com o e-mail de entrega ou como resposta posterior quando a equipe o solicitar. A publicação efetiva no Discord é coordenada pela equipe do programa seguindo o procedimento interno correspondente.

---

## Processo de revisão e pagamento

Uma vez recebido o e-mail de entrega com a informação completa, a equipe da Golem inicia a revisão do projeto. Essa revisão verifica que o entregável cumpra com os requisitos formais descritos neste documento, que se ajuste ao escopo acordado no pitch aprovado, e que as métricas reportadas sejam coerentes e reproduzíveis a partir do código publicado.

Se a revisão identificar pontos abertos que requeiram ajustes (documentação incompleta, métricas insuficientes, problemas de reprodutibilidade, escopo não coberto), a equipe abrirá um ciclo de iteração com o builder por e-mail, indicando os pontos específicos a resolver. Esse ciclo busca assegurar a qualidade do entregável e, em geral, os ajustes solicitados são menores e se resolvem em poucos dias.

Uma vez validado o entregável, a equipe procede ao pagamento do bounty via transferência de $GLM ao endereço de wallet fornecido pelo builder, na rede indicada no e-mail de entrega. O builder deve assegurar-se de fornecer um endereço de wallet correto e compatível com a rede escolhida, dado que os pagamentos enviados a endereços errôneos não são recuperáveis.

Após a confirmação do pagamento, a equipe procede à coordenação da difusão do projeto pelos canais oficiais e pelas comunidades parceiras correspondentes, completando assim o ciclo do programa.

---

## Recomendações finais

Para além dos requisitos formais, existem algumas boas práticas que elevam significativamente a qualidade percebida de um entregável e favorecem sua difusão posterior.

As capturas de tela, diagramas ou gravações curtas que mostrem o projeto em operação têm um valor demonstrativo desproporcional e recomenda-se incluí-los no README quando o tipo de projeto o permita. Um GIF animado mostrando uma execução real, um diagrama de arquitetura claro ou uma visualização dos resultados obtidos transforma um README correto em um memorável.

A disponibilidade do builder para responder issues razoáveis abertas no repositório durante as semanas posteriores à entrega contribui ao valor do recurso publicado e é considerada boa prática do programa, sem constituir uma condição formal para o pagamento do bounty.

Por fim, os builders cujo entregável for particularmente bem recebido pela comunidade podem ser convidados a participar em futuras iniciativas do ecossistema, apresentar seu trabalho em eventos relacionados com Golem ou colaborar em projetos de maior escopo. A qualidade do entregável inicial é, nesse sentido, também um investimento em oportunidades posteriores.

---

## Próximos passos

Após completar a entrega seguindo este documento, o builder não precisa realizar ações adicionais até receber resposta da equipe. Para consultas durante o processo de revisão ou sobre qualquer aspecto do programa, o canal recomendado continua sendo o Discord oficial da Golem em [discord.gg/golem](https://discord.gg/golem).

Para referência sobre os demais documentos do programa, consultar o [README](../README.md) geral do repositório.
