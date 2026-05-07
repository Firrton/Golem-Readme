# Frequently Asked Questions

Reference document gathering the most common questions about the **Golem Community Builder Programme**. It is intended as a complement to the rest of the repository documentation and as a starting point before channelling specific queries to the programme team or the Golem technical community.

The answers included here reflect the policy of the programme in force at the time of the document's last update. For specific situations not covered in the FAQ, official communication channels are detailed at the end of the document.

---

## About the programme

**What exactly is the Golem Community Builder Programme?**

The programme is an open and ongoing initiative that funds technical projects built on top of Golem Network. Each approved project receives a bounty of 500 USD paid in $GLM, with an estimated duration of two to four weeks of development. Unlike a traditional hackathon, the programme does not run under deadline pressure or via pitch competitions; instead, it funds genuine technical work on the protocol. The full description of the programme can be found in the [README](./README.md).

**How is this programme different from a hackathon?**

The main difference is structural. A hackathon has start and end dates, requires participants to complete the work within a compressed timeframe, and usually awards prizes only to winning projects after a competition. This programme has no fixed deadline, runs continuously, and pays the full bounty to every approved project that meets the agreed deliverables. The philosophy is to fund quality technical work rather than to produce competition between builders.

**Who can participate?**

The programme is open to Web3 developers with or without prior Golem experience, as well as Web2 developers exploring decentralized compute for the first time. No formal credentials or affiliation with a specific organization are required. Technical capacity to build the proposed project and willingness to publish the result under an open license are required.

**Can teams be formed for participation?**

Yes. The programme accepts both individual builders and teams without an explicit size limit. Teams must designate a single point of contact for communication with the Golem team and define internally how they will distribute the bounty among their members. The bounty is transferred to a single wallet address, and the subsequent distribution is outside the scope of the programme.

**Can I participate in multiple projects over time?**

Participation in multiple projects is evaluated case by case by the programme team. Builders who have satisfactorily completed a previous project may be invited or authorized to submit new proposals, depending on the quality of the previous work, the time elapsed and the availability of slots in the programme. The policy seeks to balance recognition of the recurring work of committed builders with openness to new participants.

---

## On technical aspects

**Do I need prior experience with Golem to participate?**

No. The programme is explicitly designed to welcome both builders with prior experience and developers who are encountering Golem for the first time. For new builders, the [Builders Guide](./docs/builders_guide.md) offers project directions with estimated complexity to facilitate the initial choice.

**Which SDK should I use to build my project?**

The main recommended path is `@golem-sdk/task-executor`, a JavaScript and TypeScript library oriented towards map-reduce patterns and task parallelization. For builders with more specific needs or prior experience in distributed systems, `@golem-sdk/golem-js` 3.x offers direct access to the protocol's low-level models. The full discussion of when to choose each option can be found in the Common Technical Notes section of the [Builders Guide](./docs/builders_guide.md).

**Can I work on testnet or do I have to use mainnet?**

Both networks are valid for delivery of the programme. The testnet, which currently runs on the hoodi network, is the recommended environment for most projects, as it allows real work to be executed on the network at no real cost. Mainnet is appropriate when the project requires demonstrating real economic behaviour or integrations with production systems. The choice must be made explicit in the pitch.

**Is there support for languages other than JavaScript and TypeScript?**

The Golem stack has SDKs in other languages, but the most up-to-date documentation and the official examples are concentrated in the JavaScript ecosystem. Builders who prefer to work in another language can do so, but should bear in mind that the learning curve and the available support are smaller. It is recommended to discuss this decision during the pitch phase.

**Can I use GPU in my project?**

Golem offers access to GPU providers, although availability may be variable depending on the moment and the type of hardware required. Projects that critically depend on GPU should mention this dependency in the pitch so that the team can confirm viability before approval.

---

## On the programme process

**How long does the team take to review a pitch?**

The concrete response time depends on the volume of pitches received at any given time. The programme team aims to respond with the greatest reasonable agility and notifies the builder as soon as the decision has been made.

**What happens if my pitch is rejected?**

Decisions on rejected pitches are at the discretion of the programme team. In some cases, rejection may be accompanied by specific comments that allow the builder to adjust the proposal and resubmit it. In other cases, the builder may be advised to explore an alternative direction or to wait before submitting a new proposal. The specific decision is communicated directly to the builder at the time of rejection.

**Can I modify the project's scope during development?**

Minor changes in scope, motivated by technical findings during development, are common and acceptable provided they are communicated to the programme team. Substantial changes that alter the nature of the project require explicit agreement with the team before proceeding. Proactive communication during development is a formal expectation of the programme and is documented in the [README](./README.md).

**What happens if I cannot complete the project?**

Situations of uncompleted projects are evaluated case by case by the programme team. When the builder has maintained communication during development and there are genuine technical circumstances that prevented completion, the team may consider partial payments proportional to demonstrable progress or reorient the project towards a reduced scope. In situations of abandonment without communication, payment of the bounty does not proceed. The programme's policy seeks to protect both the builder in the face of genuine difficulties and the team in the face of uncompleted deliveries.

**Can I submit a pitch without having read all the repository documents?**

It is technically possible, but not recommended. The quality of the pitch and the speed of approval depend directly on the builder having understood the programme's criteria, the directions of each track and the deliverable's requirements. Pitches from builders who show familiarity with the documentation receive fewer adjustment requests and advance through the process more quickly.

---

## On intellectual property and dissemination

**Who owns the repository and the code?**

The builder retains full ownership of the repository and the code, published under the chosen open source license. The programme does not claim exclusive rights over the funded work and does not require transfer of the repository to a Golem organization.

**Can I use the project for my portfolio or continue developing it?**

Yes. The builder is free to use the project for professional portfolio, public presentations, job applications, continued development, and even evolution of the project into commercial products. The programme explicitly encourages funded projects to continue growing beyond the initial bounty.

**What dissemination does Golem do of the project?**

Once the deliverable is validated, the team coordinates the dissemination of the project through the official Golem channels and the corresponding partner communities. This includes publication on the official Discord, mention on the project's social networks when applicable, and inclusion of the repository as a reference within the ecosystem. Specific dissemination varies according to the type of project and the moment of the programme.

**Can I present the project at events or conferences?**

Yes. The builder is free to present their work at any event, hackathon or conference, mentioning that it was built within the framework of the Golem Community Builder Programme. When applicable, the programme team can facilitate contacts or additional information to support such presentations.

---

## Support and consultation channels

For questions not covered in this document, the recommended channels differ according to the nature of the query.

For specific queries about the programme, the first option is the Discord channel dedicated to the builder programme within the official Golem server, where the programme team handles questions about tracks, pitches, scope, delivery, payments and any operational aspect of the initiative.

For technical queries about the Golem protocol itself, independent of the programme, the appropriate option is the `❓question-answers` channel or equivalent on the official Golem server, where the wider technical community and the protocol team answer questions about the SDK, yagna, providers, infrastructure and other general technical aspects.

To go deeper into technical aspects before raising a query, the official Golem documentation at [docs.golem.network](https://docs.golem.network) constitutes the main reference resource and usually answers most common technical doubts without the need to channel them through chat.

Access to the official Discord server is via [discord.gg/golem](https://discord.gg/golem).
