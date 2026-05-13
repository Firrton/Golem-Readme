# Frequently Asked Questions

## About the programme

**What exactly is the Golem Community Builder Programme?**

The programme is an open and ongoing initiative that funds technical projects built on top of Golem Network. Each approved project receives a bounty of 500 USD paid in $GLM, with an estimated duration of two to four weeks of development. The full description of the programme can be found in the [README](./README.md).

**How is this programme different from a hackathon?**

The programme is open-ended: no deadlines, no pitch competition, no runners-up. Builders submit their own ideas through the application form. The Golem team reviews submissions on a rolling basis and picks the strongest ones. For selected projects, the builder and the team agree the scope together — and only then does development start.

**Who can participate?**

Any developer with the technical capacity to ship a real project: Web2 or Web3 background, with or without prior Golem experience.

**Can teams be formed for participation?**

Yes. The programme accepts both individual builders and teams without a size limit.

**Can I participate in multiple projects over time?**

One project per team at a time. After delivery is validated and the bounty paid, the same team may apply again with a new idea. 

---

## On technical aspects

**Do I need prior experience with Golem to participate?**

No prior Golem experience required. The team is available on Discord to onboard you to the protocol during development.

**Which SDK should I use to build my project?**

The main recommended path is `@golem-sdk/task-executor`, a JavaScript and TypeScript library oriented towards map-reduce patterns and task parallelization. For builders with more specific needs or prior experience in distributed systems, `@golem-sdk/golem-js` 3.x offers direct access to the protocol's low-level models. The full discussion of when to choose each option can be found in the Common Technical Notes section of the [Builders Guide](./docs/builders_guide.md).

**Can I work on testnet or do I have to use mainnet?**

We expect builders to iterate on testnet (currently `hoodi`). There is no mainnet expectation by default. If mainnet is genuinely needed for a project, that's agreed between the selected team and the Golem team at scoping time.

**Is there support for languages other than JavaScript and TypeScript?**

The Golem stack has SDKs in other languages, but the most up-to-date documentation and the official examples are concentrated in the JavaScript ecosystem. Builders who prefer to work in another language can do so, but should bear in mind that the learning curve and the available support are smaller. It is recommended to discuss this decision during the application phase.

**Can I use GPU in my project?**

Golem offers access to GPU providers, although availability may be variable depending on the moment and the type of hardware required. Projects that critically depend on GPU should mention this dependency in the application form so that the team can confirm viability before approval.

---

## On the programme process

**How long does it take to hear back after applying?**

The Golem team reviews applications on a rolling basis, so there is no fixed response window. You'll be notified as soon as a decision is made. If your idea fits the programme, the team reaches out to discuss scope and milestones before any development starts.

**What happens if my application is rejected?**

Decisions on rejected applications are at the discretion of the programme team. We aim to share feedback when we can, but given application volume we cannot guarantee it.

**Can I modify the project's scope during development?**

Minor changes in scope, motivated by technical findings during development, are common and acceptable provided they are communicated to the programme team. Substantial changes that alter the nature of the project require explicit agreement with the team before proceeding.

**What happens if I cannot complete the project?**

Situations of uncompleted projects are evaluated case by case by the programme team.

---

## On intellectual property and dissemination

**Who owns the repository and the code?**

The builder retains full ownership of the repository and the code, published under the chosen open source licence. The programme does not claim exclusive rights over the funded work and does not require transfer of the repository to a Golem organisation.

By submitting a project to the programme, you authorise Golem to mention, share, and feature the project across its channels for marketing and ecosystem-promotion purposes.

**Can I use the project for my portfolio or continue developing it?**

Yes. The builder is free to use the project for professional portfolio, public presentations, job applications, continued development, and even evolution of the project into commercial products. The programme explicitly encourages funded projects to continue growing beyond the initial bounty.

**How does Golem promote the project?**

Once your deliverable is validated, the team shares the project across Golem's official channels: a post on Discord, a mention on Golem's social media when it fits, and adding the repository to our list of ecosystem references. What we do exactly depends on the project.

**Can I present the project at events or conferences?**

Yes. The builder is free to present their work at any event, hackathon or conference. When applicable, the programme team can facilitate contacts or additional information to support such presentations.

---

## Support and channels

For anything not covered here, use the channel that fits the question:

- **Programme questions** (tracks, applications, scope, delivery, payments): the `builders` channel on the official Golem Discord.
- **Technical questions about Golem itself** (SDK, yagna, providers, infrastructure): the `❓question-answers` channel on the same Discord.
- **Before asking, check the docs**: [docs.golem.network](https://docs.golem.network) covers most technical questions.

Join the Discord at [discord.gg/golem](https://discord.gg/golem).

---

## Additional questions

**Do I need to prepare a pitch document or template to apply?**

No. Applications are made through the official form at https://forms.golem.network/golem-builders-programme. The form captures the track, idea, technical approach and relevant experience. There is no separate pitch document to write or upload.

**What should the 2–3 minute demo video show?**

A short recording of the project running in practice — enough for someone unfamiliar with the work to grasp what it does and how it uses Golem. The video is a required deliverable and is used for amplification on official Golem channels.

**When the bounty is paid in $GLM, how is the USD amount converted?**

The bounty is denominated in 500 USD and paid in $GLM. The $GLM amount is fixed at the rate on the day of payment, so the equivalent USD value at that moment matches the agreed bounty. Builders provide a wallet address and the network they want to receive on (Polygon or Ethereum mainnet); $GLM is transferred directly.

**Can I use AI tools or code assistants while building?**

Yes. The deliverable is the working project, the documentation and the demo video. How you build it is up to you — AI code assistants, pair-programming tools, or anything else. What matters is that the code is yours to publish under an open licence, the technical write-up reflects your understanding of the work, and the project actually runs on Golem.

**Can I fork an existing Golem project for my submission?**

Forks are accepted only as a starting point and only with substantial new work on top. A pure fork with minor changes does not qualify. If you're in doubt about whether your direction counts as substantial, mention it in the application form — the team will tell you up front.
