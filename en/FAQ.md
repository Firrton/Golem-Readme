# Frequently Asked Questions

Reference document gathering the most common questions about the **Golem Community Builder Programme**. It is intended as a complement to the rest of the repository documentation and as a starting point before channelling specific queries to the programme team or the Golem technical community.

The answers included here reflect the policy of the programme in force at the time of the document's last update. For specific situations not covered in the FAQ, official communication channels are detailed at the end of the document.

---

## About the programme

**What exactly is the Golem Community Builder Programme?**

The programme is an open and ongoing initiative that funds technical projects built on top of Golem Network. Each approved project receives a bounty of 500 USD paid in $GLM, with an estimated duration of two to four weeks of development. Unlike a traditional hackathon, the programme does not run under deadline pressure or via pitch competitions; instead, it funds genuine technical work on the protocol. The full description of the programme can be found in the [README](./README.md).

**How is this programme different from a hackathon?**

The programme is open-ended with no deadlines or competitive judging. The Golem team funds clearly-scoped projects that demonstrate the protocol, and every approved project receives the bounty — there are no runners-up.

**Who can participate?**

Any developer with the technical capacity to ship a real project: Web2 or Web3 background, with or without prior Golem experience. No credentials or affiliations required.

**Can teams be formed for participation?**

Yes. The programme accepts both individual builders and teams without an explicit size limit.

**Can I participate in multiple projects over time?**

One project per team at a time. After delivery is validated and the bounty paid, the same team may apply again with a new idea. We do this so the team's attention stays on one well-scoped project, not several in parallel.

---

## On technical aspects

**Do I need prior experience with Golem to participate?**

No prior Golem experience required. The team is available on Discord to onboard you to the protocol during development.

**Which SDK should I use to build my project?**

The main recommended path is `@golem-sdk/task-executor`, a JavaScript and TypeScript library oriented towards map-reduce patterns and task parallelization. For builders with more specific needs or prior experience in distributed systems, `@golem-sdk/golem-js` 3.x offers direct access to the protocol's low-level models. The full discussion of when to choose each option can be found in the Common Technical Notes section of the [Builders Guide](./docs/builders_guide.md).

**Can I work on testnet or do I have to use mainnet?**

Both networks are valid for delivery of the programme. The testnet, which currently runs on the hoodi network, is the recommended environment for most projects, as it allows real work to be executed on the network at no real cost. Mainnet is appropriate when the project requires demonstrating real economic behaviour or integrations with production systems. The choice must be made explicit in the application form.

**Is there support for languages other than JavaScript and TypeScript?**

The Golem stack has SDKs in other languages, but the most up-to-date documentation and the official examples are concentrated in the JavaScript ecosystem. Builders who prefer to work in another language can do so, but should bear in mind that the learning curve and the available support are smaller. It is recommended to discuss this decision during the application phase.

**Can I use GPU in my project?**

Golem offers access to GPU providers, although availability may be variable depending on the moment and the type of hardware required. Projects that critically depend on GPU should mention this dependency in the application form so that the team can confirm viability before approval.

---

## On the programme process

**How long does the team take to review an application?**

We aim to respond within 7 business days. If we expect to take longer in a particular case (for example during programme launches with high volume), we'll let you know when you receive the acknowledgement email.

**What happens if my application is rejected?**

Decisions on rejected applications are at the discretion of the programme team. In some cases, rejection may be accompanied by specific comments that allow the builder to adjust the proposal and resubmit it. In other cases, the builder may be advised to explore an alternative direction or to wait before submitting a new proposal. The specific decision is communicated directly to the builder at the time of rejection.

**Can I modify the project's scope during development?**

Minor changes in scope, motivated by technical findings during development, are common and acceptable provided they are communicated to the programme team. Substantial changes that alter the nature of the project require explicit agreement with the team before proceeding. Proactive communication during development is a formal expectation of the programme and is documented in the [README](./README.md).

**What happens if I cannot complete the project?**

Situations of uncompleted projects are evaluated case by case by the programme team. When the builder has maintained communication during development and there are genuine technical circumstances that prevented completion, the team may consider partial payments proportional to demonstrable progress or reorient the project towards a reduced scope. In situations of abandonment without communication, payment of the bounty does not proceed. The programme's policy seeks to protect both the builder in the face of genuine difficulties and the team in the face of uncompleted deliveries.

---

## On intellectual property and dissemination

**Who owns the repository and the code?**

The builder retains full ownership of the repository and the code, published under the chosen open source licence. The programme does not claim exclusive rights over the funded work and does not require transfer of the repository to a Golem organisation.

**Can I use the project for my portfolio or continue developing it?**

Yes. The builder is free to use the project for professional portfolio, public presentations, job applications, continued development, and even evolution of the project into commercial products. The programme explicitly encourages funded projects to continue growing beyond the initial bounty.

**What dissemination does Golem do of the project?**

Once the deliverable is validated, the team coordinates the dissemination of the project through the official Golem channels. This includes publication on the official Discord, mention on the project's social networks when applicable, and inclusion of the repository as a reference within the ecosystem. Specific dissemination varies according to the type of project and the moment of the programme.

**Can I present the project at events or conferences?**

Yes. The builder is free to present their work at any event, hackathon or conference, mentioning that it was built within the framework of the Golem Community Builder Programme. When applicable, the programme team can facilitate contacts or additional information to support such presentations.

---

## Support and consultation channels

For questions not covered in this document, the recommended channels differ according to the nature of the query.

For specific queries about the programme, the first option is the builders channel on the official Golem Discord (discord.gg/golem), where the programme team handles questions about tracks, applications, scope, delivery, payments and any operational aspect of the initiative.

For technical queries about the Golem protocol itself, independent of the programme, the appropriate option is the `❓question-answers` channel or equivalent on the official Golem server, where the wider technical community and the protocol team answer questions about the SDK, yagna, providers, infrastructure and other general technical aspects.

To go deeper into technical aspects before raising a query, the official Golem documentation at [docs.golem.network](https://docs.golem.network) constitutes the main reference resource and usually answers most common technical doubts without the need to channel them through chat.

Access to the official Discord server is via [discord.gg/golem](https://discord.gg/golem).

---

## Additional questions

**Do I need to prepare a pitch document or template to apply?**

No. Applications are made through the official form at https://forms.golem.network/golem-builders-programme. The form captures the track, idea, technical approach and relevant experience. There is no separate pitch document to write or upload.

**How long does it take to hear back after applying?**

The Golem team reviews applications on a rolling basis. There is no fixed response window, but you will be notified as soon as a decision is made. If your idea fits the programme, the team reaches out to discuss specifics and milestones before any development starts.

**What should the 2–3 minute demo video show?**

A short recording of the project running in practice — enough for someone unfamiliar with the work to grasp what it does and how it uses Golem. The video is a required deliverable and is used for amplification on official Golem channels.

**When the bounty is paid in $GLM, how is the USD amount converted?**

The bounty is denominated in 500 USD and paid in $GLM. The $GLM amount is fixed at the rate on the day of payment, so the equivalent USD value at that moment matches the agreed bounty. Builders provide a wallet address and the network they want to receive on (Polygon or Ethereum mainnet); $GLM is transferred directly.

**Can I use AI tools or code assistants while building?**

Yes. The deliverable is the working project, the documentation and the demo video. How you build it is up to you — AI code assistants, pair-programming tools, or anything else. What matters is that the code is yours to publish under an open licence, the technical write-up reflects your understanding of the work, and the project actually runs on Golem.

**Can I fork an existing Golem project for my submission?**

Forks are accepted only as a starting point and only with substantial new work on top. A pure fork with minor changes does not qualify. If you're in doubt about whether your direction counts as substantial, mention it in the application form — the team will tell you up front.
