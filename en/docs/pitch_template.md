# Pitch Template

## Description of the fields

### 1. Contact information

The pitch should open with the basic information that allows the programme team to identify the builder and establish communication during the review and development process.

For individual builders, the required fields are full name, email address, Discord identifier and link to GitHub profile or professional portfolio. The wallet address is not requested in the pitch, but at the time of final delivery of the project.

For teams, a single point of contact responsible for communication with the programme team must be designated. The pitch must also list the rest of the team members with full name, expected role in the project and link to professional profile or GitHub. The internal distribution of the bounty is outside the scope of the programme and should be agreed internally among the team members.

### 2. Track and project title

The builder must explicitly indicate which of the five tracks corresponds to their proposal: Track A (Parallel Media Processing), Track B (Compute-Intensive Simulation), Track C (Provider Reputation & Benchmarking), Track D (Chess Engine / Game AI at Scale) or Track E (Open Track). This classification facilitates internal evaluation and allows the team to quickly identify the technical context of the proposal.

The tentative title of the project may be adjusted during development, but it is convenient to propose one from the pitch to facilitate subsequent communication.

### 3. Project description

This field is the heart of the pitch. In one or two paragraphs, the builder must explain what will be built, what problem or use case it addresses, and what makes the project interesting from the perspective of decentralized compute.

The description must be comprehensible to a reader who knows Golem but has not read other documentation about the project. It should clearly answer three basic questions: what will be built, how Golem will be used within the project, and what kind of technical demonstration the final result produces.

### 4. Technical scope

This section details the concrete technical decisions that the builder has made when planning the project. It should cover four elements.

The first is the SDK to be used: `@golem-sdk/task-executor` as the main recommended path for most projects, or `@golem-sdk/golem-js` 3.x when the project requires fine control over the market logic or selection of providers. If the builder proposes to work with an SDK other than the JavaScript ecosystem, they must justify it explicitly.

The second is the network on which the project will be executed: testnet hoodi for most cases, or mainnet when the project requires demonstrating real economic behaviour.

The third is the relevant auxiliary stack: programming languages, external libraries, parallelization tools or any significant technical dependency that the team should know in order to evaluate viability.

The fourth is the specific architecture decisions, particularly those related to parallelization of the work: how the task will be divided into distributable units, how the results will be aggregated, and how errors or non-responsive providers will be handled.

### 5. Work plan

The builder must propose a division of the project into phases or milestones, with estimated times for each. A detailed schedule is not required: an approximate division demonstrating that the builder has thought about how to distribute the work over the planned two to four weeks is sufficient.

A typical division for a three-week project might include a first week of environment setup, SDK exploration and construction of the first proof of concept; a second week of development of the parallelized component and validation of results; and a third week of polishing, documentation, generation of final metrics and preparation of the deliverable.

### 6. Expected deliverables

The builder must specify what the repository will contain at the end of the project, what metrics will be documented, and what kind of demonstration or evidence will be produced. These deliverables should align with those described in the corresponding track of the [Builders Guide](./builders_guide.md), although they may include additional elements specific to the proposal.

For projects with a visual component, it is convenient to anticipate whether a live demo, screenshots, animated GIFs or explanatory video will be included. For projects with a quantitative component, it is convenient to anticipate what kind of visualizations or tables of results will accompany the deliverable.

### 7. Relevant prior experience

This section allows the team to evaluate the builder's execution capacity. It should briefly describe the technical background relevant to the project, without the need for an exhaustive resume.

Useful elements to mention include experience in the project's domain (for example, media processing for Track A, computational finance for Track B), prior experience with Golem if any, similar projects built previously, and links to repositories or demos demonstrating the technical capacity of the builder or team.

For builders without prior experience with Golem, this section is not an obstacle: the programme is explicitly open to developers new to the protocol. What is evaluated is the general technical capacity to execute the proposed project, not prior familiarity with Golem.

### 8. Additional notes

Open section where the builder can include any information that helps the team evaluate the proposal and that does not naturally fit into the previous fields. Typical uses include identified risks that the builder anticipates, scope decisions that the builder wants to validate before starting, external dependencies that may affect the viability of the project, specific questions directed to the team, or any additional relevant context.

This section is optional. Pitches without additional notes are perfectly valid when the rest of the content is sufficiently clear.

---

## Clean template

Below is the template in a format ready to copy and complete. The fields between brackets must be replaced with the corresponding information.

```
GOLEM COMMUNITY BUILDER PROGRAMME — PITCH

1. CONTACT INFORMATION

Full name: [name of the builder or team point of contact]
Email: [email address]
Discord: [Discord identifier]
GitHub or portfolio: [link to professional profile]

Application type:
[ ] Individual builder
[ ] Team

If applying as a team, list additional members:
- [Name]: [role in the project] — [link to profile]
- [Name]: [role in the project] — [link to profile]

2. TRACK AND PROJECT TITLE

Track chosen:
[ ] Track A — Parallel Media Processing
[ ] Track B — Compute-Intensive Simulation
[ ] Track C — Provider Reputation & Benchmarking
[ ] Track D — Chess Engine / Game AI at Scale
[ ] Track E — Open Track

Tentative project title: [title]

3. PROJECT DESCRIPTION

[One or two paragraphs explaining what will be built, what problem
or use case it addresses, and what makes the project interesting
from the perspective of decentralized compute.]

4. TECHNICAL SCOPE

SDK to use:
[ ] @golem-sdk/task-executor
[ ] @golem-sdk/golem-js 3.x
[ ] Other: [specify and justify]

Execution network:
[ ] Testnet (hoodi)
[ ] Mainnet

Relevant auxiliary stack:
[Languages, libraries, external tools and significant technical
dependencies.]

Architecture decisions:
[How the work will be divided into parallelizable units, how the
results will be aggregated, and how errors or non-responsive
providers will be handled.]

5. WORK PLAN

Estimated duration: [number of weeks]

Planned milestones:
- Week 1: [main activities]
- Week 2: [main activities]
- Week 3: [main activities]
- Week 4 (if applicable): [main activities]

6. EXPECTED DELIVERABLES

Repository:
[What the repository will contain at the end of the project.]

Metrics to document:
[What metrics will be reported and how they will be obtained.]

Demonstration or evidence:
[Type of demo, screenshots, GIFs, video or visualizations that
will accompany the deliverable.]

7. RELEVANT PRIOR EXPERIENCE

[Brief description of the technical background relevant to the
project. Mention experience in the domain, prior experience with
Golem if any, and links to previous projects if applicable.]


8. ADDITIONAL NOTES (OPTIONAL)

[Identified risks, scope decisions to validate, external
dependencies, questions for the team, or any additional relevant
context. This section is optional.]
```

---

## Next steps

Once the template is completed, the pitch should be submitted through the **official programme form**: [pending]. The form is structured coherently with this template, so transferring the information is straightforward.

The programme team reviews each pitch and responds with one of three possibilities: direct approval, request for scope adjustments, or rejection with justification. The complete review policy is described in the general [README](../README.md) of the repository.

For queries prior to pitch submission, the recommended channel is the official Golem Discord at [discord.gg/golem](https://discord.gg/golem).
