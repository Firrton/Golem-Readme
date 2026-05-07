# Submission Guide

Reference document for the formal delivery of projects within the **Builder Programme**. It defines the minimum criteria that a deliverable must meet, the procedure for notifying the Golem team, the review process, and the steps to receive payment of the bounty.

Reading this document is recommended at the start of development, not only at the time of delivery. Knowing the submission requirements from the start allows the builder to structure the repository and documentation incrementally, avoiding last-minute work and ensuring that the deliverable meets the standards of the programme.

---

## Delivery procedure

The formal delivery of a finished project is made via email addressed to the programme team. This is the official channel through which the review process begins and the validation cycle leading to payment of the bounty is triggered.

The delivery email must be sent to the official programme address [pending] and include at minimum the following elements: identification of the builder and reference to the previously approved pitch, public link to the project's GitHub repository, builder's wallet address for the transfer of the bounty with explicit indication of the network on which payment will be made, and any relevant note on the state of the project that the team should know before starting the review (for example, limitations identified during development, scope decisions taken in consultation with the team, or particularly noteworthy results worth highlighting).

Complementarily, once receipt of the email has been confirmed and after the internal process has progressed, the project will be announced on the official Golem Discord with a brief summary and the corresponding links. The builder does not need to initiate this announcement on their own: the team coordinates publication on the corresponding channels once the delivery has been validated.

---

## Repository requirements

The project must live in a public GitHub repository under the builder's personal user or organization.

The repository must be published under a clearly indicated open source license. The recommended license is **MIT**, given that it is the most permissive, the most widely used in the Golem ecosystem and the one that best facilitates reuse of the work by the community. The `LICENSE` file must be present at the root of the repository with the full text of the license and the name of the holder.

The structure of the repository must allow an external developer to clone the project, install dependencies and run it following exclusively the instructions of the README, with no need for additional consultation. This implies that the code must be accompanied by a standard dependency configuration file for the language used (`package.json` for Node.js, `requirements.txt` or `pyproject.toml` for Python, as appropriate), the scripts necessary to reproduce the runs documented in the deliverable, and any configuration file or environment variable required for execution, properly documented.

It is recommended to avoid including credentials, private keys, local configuration files or any sensitive data in the repository. Variables that the builder must configure to run the project should be documented in the README via a `.env.example` file or equivalent.

---

## README requirements

The README of the repository constitutes the main public-facing document and must be written with corresponding care. It simultaneously fulfils the role of project presentation, usage instructions for developers who want to reproduce it, and technical write-up documenting the work done.

The README should open with a concise description of the project explaining in a few lines what it does, on which programme track it was built, and why it is interesting from the perspective of decentralized compute. This initial section must be comprehensible to a reader who has not read the original pitch.

Next, an installation and execution instructions section should be included, detailed enough for an external developer to reproduce the project. This section must cover the prerequisites (yagna version, Node.js or other runtime version, operating system dependencies if applicable), the step-by-step installation and configuration procedure, and the exact commands to run the project and reproduce the documented results.

The main body of the README should contain the technical write-up of the project. This section documents what was built, how the parallelization was designed, what technical decisions were made and why, what challenges were encountered during development and how they were resolved, and what results were obtained. The expected length is several well-structured sections, sufficient for a technical reader to understand the work in depth without needing to read the source code.

A dedicated section should present the metrics and results of the project's execution on Golem. Specific criteria on which metrics to report and in what format will be established in a later version of this document. Until then, builders should report the metrics indicated in the corresponding track of the [Builders Guide](./builders_guide.md) and any additional data they consider relevant to demonstrate the functioning of the project.

Finally, the README should close with a brief section documenting known limitations of the project, possible directions of extension that other builders could explore from this work, and the corresponding credits to the builder and the programme.

---

## Discord summary

Complementary to the extensive write-up of the README, the project should be accompanied by a brief summary designed for publication on the official Golem Discord. This summary does not replace the README but works as an announcement of the delivery and a gateway to the repository.

The summary should be significantly shorter than the README, written in a register accessible to a wide audience that may not have deep technical context, and oriented towards generating interest in consulting the full repository. The recommended length is one or two paragraphs covering what was built, what it demonstrates of the protocol, and where to find the repository for further detail.

The builder should send this summary together with the delivery email or as a subsequent reply when the team requests it. The actual publication on Discord is coordinated by the programme team following the corresponding internal procedure.

---

## Review and payment process

Once the delivery email has been received with the complete information, the Golem team begins review of the project. This review verifies that the deliverable meets the formal requirements described in this document, that it conforms to the scope agreed in the approved pitch, and that the reported metrics are coherent and reproducible from the published code.

If the review identifies open points requiring adjustments (incomplete documentation, insufficient metrics, reproducibility problems, scope not covered), the team will open an iteration cycle with the builder by email, indicating the specific points to resolve. This cycle aims to ensure the quality of the deliverable and, in general, the requested adjustments are minor and resolved in a few days.

Once the deliverable has been validated, the team proceeds to payment of the bounty via transfer of $GLM to the wallet address provided by the builder, on the network indicated in the delivery email. The builder must ensure that they provide a correct wallet address compatible with the chosen network, given that payments sent to wrong addresses are not recoverable.

After confirmation of payment, the team proceeds to coordinate the dissemination of the project through the official channels and the corresponding partner communities, thereby completing the cycle of the programme.

---

## Final recommendations

Beyond the formal requirements, there are some good practices that significantly elevate the perceived quality of a deliverable and favour its subsequent dissemination.

Screenshots, diagrams or short recordings showing the project in operation have disproportionate demonstrative value and are recommended to include in the README when the type of project allows. An animated GIF showing a real execution, a clear architecture diagram or a visualization of the obtained results transforms a correct README into a memorable one.

The availability of the builder to respond to reasonable issues opened in the repository during the weeks following delivery contributes to the value of the published resource and is considered good practice of the programme, without constituting a formal condition for payment of the bounty.

Finally, builders whose deliverable is particularly well received by the community may be invited to participate in future ecosystem initiatives, present their work at events related to Golem or collaborate on projects of greater scope. The quality of the initial deliverable is, in this sense, also an investment in subsequent opportunities.

---

## Next steps

After completing the delivery following this document, the builder does not need to take additional actions until receiving a response from the team. For queries during the review process or about any aspect of the programme, the recommended channel continues to be the official Golem Discord at [discord.gg/golem](https://discord.gg/golem).

For reference on the other documents of the programme, consult the general [README](../README.md) of the repository.
