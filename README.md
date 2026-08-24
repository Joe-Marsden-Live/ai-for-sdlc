# AI Tool Adoption for Software Development

## Table of Contents

- [AI Tool Adoption for Software Development](#ai-tool-adoption-for-software-development)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Metadata \& Licensing](#metadata--licensing)
  - [Key Terms \& Concepts](#key-terms--concepts)
  - [Potential Rewards](#potential-rewards)
  - [Operational Risks](#operational-risks)
    - [Productivity Risks](#productivity-risks)
    - [Quality Risks](#quality-risks)
    - [Financial \& Dependency Risks](#financial--dependency-risks)
    - [Security \& Compliance Risks](#security--compliance-risks)
  - [Technical Architecture \& Options](#technical-architecture--options)
    - [Workflow Paradigms](#workflow-paradigms)
    - [Harness Options](#harness-options)
    - [Model Options \& Selection Factors](#model-options--selection-factors)
    - [Hosting Models](#hosting-models)
    - [Product Architectures \& Ecosystems](#product-architectures--ecosystems)
  - [Governance \& Change Management](#governance--change-management)
    - [Strategic Considerations](#strategic-considerations)
  - [Implementation Plans](#implementation-plans)

## Overview

This document provides an operational overview of the factors that organizations must consider when adopting AI for software development. How these factors impact individual enterprises will vary based on their specific technical architectures, security requirements, and organizational maturity. 

While Large Language Models (LLMs) represent the primary technology used today, the core considerations apply across wider AI implementations. 


---

## Metadata & Licensing

* **License:** This work is licensed under a Creative Commons Attribution 4.0 International License (CC BY 4.0). You are free to share and adapt this content provided appropriate credit is given.
* **AI Statement:** Written by Joe Marsden, with review input from AI.

---

## Key Terms & Concepts

* **Chatbots:** Applications that utilize AI models to answer questions from a user. These work on a request and response basis: ask a question and it will come up with a response. Depending on the chatbot and model, it may be able to accept other inputs such as documents and pictures and likewise produce such things as outputs. They are widely available in browsers, phone, and desktop applications and can also be server-hosted to provide this functionality inside other applications.
* **Agents:** Given a task to execute, agents work to complete it. Tasks can vary from a custom task, such as adding a new button to an interface, to more generic tasks, such as checking code changes for security flaws. Agents are not limited to purely writing code; they can use tools provided to them to perform other tasks, such as checking code into a repository or creating a build and deploying it. They tend to execute in cycles—making changes, checking them, and then making more changes until their tasks are completed. They may have restrictions built in to prevent them from cycling endlessly and using too many tokens.
* **Model:** In the case of LLMs at least, a model is at its core a series of nodes and weighted connections between these nodes that take a series of inputs and transform them into a series of outputs. The structure of the nodes and connections is determined by a mixture of engineering design and training.
* **Harness:** Describes an application wrapped around a model to provide a useful function. Chatbots, agents, and IDE tools are examples of harnesses. In the example of a chatbot, it converts the user’s inputs (text, documents, images, etc.) into a series of tokens that the model can read, feeds them in, and then converts the model's output into human-readable outputs (text, documents, images, etc.). Additionally, if the model determines that calling the internet will assist with its response, the harness will facilitate this (harness tools are available for a wide variety of interactions with other systems).
* **Open-Weight Model:** A model where the weights (effectively the ‘source code’ of the model) have been made public. Anyone with access to the required hardware can run the model, and the ability to use it cannot be withdrawn (short of governmental legislative action).
* **Closed-Weight Model:** A model where the weights are withheld by the lab that developed them and are effectively intellectual property. To run the model, a user must do so via the model vendor (or one of their partners).
* **Context:** Considered to be a working memory of what has happened so far in a multistage process that an AI is working on. For example, in a chat, when a follow-up question is asked, the model needs to be fed the details of the previous interaction(s) to understand the context of the new question.
* **Context Rot:** Refers to the degradation of a model's recall and reasoning accuracy as the context gets larger, even before hitting the theoretical model limit. Methods to combat this are an active area of research, but it is an issue that needs to be taken into account when working on large codebases.

---

## Potential Rewards

Below is a list of potential rewards for implementing AI as part of the development process. How changes are implemented will determine whether these benefits deliver in the form of increased productivity, increased quality, or reduced costs.

| Development Phase | Potential Benefit |
| :--- | :--- |
| **Design** | Has the capability to enhance the design process by either fully designing a solution based on user input or assisting with the design process by providing ideas and alternative approaches as well as reviewing proposed solutions. |
| **Code Generation** | Capable of writing code at high speed and with high quality. This includes creating brand new products as well as modifying existing systems. |
| **Code Refactoring** | Can completely refactor code. This may be to make the existing code more uniform, increase maintainability or can even be used to completely rewrite the code in a new language or technology (either to create a uniform codebase across an enterprise or to move away from no longer supported versions of existing development platforms). |
| **Test Generation & Testing** | Can examine existing code or design/specification documents and produce a list of suggested test cases to cover them. Can also author and run automated tests. Some AI agents can even do ad hoc testing of user interfaces by using them directly. Testing is not limited to code – it can also design and build tests for data.  |
| **Bug Fixing** | Can identify bugs by inspection of the code, bug reports, description of the error behaviour by a user, by examination of error logs, or any combination of the above – Agents can work in a closed-loop to pick up bugs, identify and fix the issue and test/release the changes (human intervention and input can be built into the process if required). |
| **Review** | Can be used to review anything created as part of the development process. |
| **Learning** | Augmenting a coder’s learning in all aspects of the development process via its extensive knowledge. |
| **Development Process** |Designing or suggesting improvements to development workflows. Can be used to implement workflow processes including writing user stories and work items, updating them throughout the development process, applying automated tests, producing and deploying builds. |
| **Documentation** | Write and enhance documentation including technical overviews and user guides. |
| **Deployment** | Design and implement software build and deployment processes.  |
| **Environments** | Design and deploy local or cloud environments for development, testing and live production systems. |
| **Security** | Some overlap here with bug fixing, build processes and reviews, but standalone security agents can also be a consideration.  |
| **Project Planning** | Can produce project plans based on work requirements and resource availability, leveraging knowledge/experience from other organizations. |
| **Risk Management** | Producing or renewing risk analysis documentation and potentially updating it based on changing circumstances.  |
| **Strategic** | Can suggest or advise on strategic direction for software products. |

---

## Operational Risks

### Productivity Risks

* **Adoption Issues:** Staff may be resentful of AI due to worries about displacement or general resistance to change. This may result in users passively or actively creating problems in new AI workflows.
* **Code Errors Leading to Rework:** Mistakes by an agent can lead to rework. If rework can be done by AI (before release), this is a cost issue; if human developers are required to intervene, it impacts productivity.

### Quality Risks

* **Overly Complex Code:** Without proper direction, AI may produce code that is overly complicated, making it hard to understand for both humans and AI systems, leading to errors and refactoring issues.
* **Inaccurate Code:** Current models can produce inaccuracies; the severity depends on the functional area.
* **Missing or Inaccurate Test Cases:** Given the volume of tests produced by AI, checking that they are accurate and cover required bases is critical.
* **Risk Management:** AI systems are generally eager to please and, without correct prompting, could ignore risks to ingratiate themselves rather than warning of important risk factors.
* **Review Fatigue:** While AI speeds up code authoring, human developers can become bottlenecks during code reviews, leading to fatigue from evaluating large volumes of AI-generated code.

### Financial & Dependency Risks

* **Token Unit Costs:** Differences exist between closed-weight and open-weight models. Closed-weight providers currently heavily subsidize per-token costs. While subsidies will not last forever, whether innovations/economies of scale or resource shortages (e.g., data center buildouts) will dictate future base costs is unknown. Open-weight models (self-hosted or rented cloud hardware) may offer more cost predictability.
* **Token Counts:** The number of tokens used to complete a task varies widely based on task type, model, and harness tool used.
* **Human Skill and Faculty Loss:** As employees become reliant on AI, they may lose their ability to perform tasks manually.
* **Complacency:** Credible AI outputs can lower user vigilance regarding hidden mistakes.

### Security & Compliance Risks

* **Indirect Prompt Injection & Data Poisoning:** Current AI systems face security vulnerabilities where they act on malicious instructions hidden within ingested data/files where a human would be far more suspicious. Safeguards must also account for rising supply chain attacks in common libraries.
* **Data Privacy:** Transferring customer data outside specific jurisdictions (e.g., EU/UK under GDPR) requires legal safeguards (Adequacy Decisions, Standard Contractual Clauses) that frontier model providers may not have in place.
* **Code Privacy:** Many frontier model providers reserve the right to use submitted data for model training, creating copyright and IP risks for proprietary codebases.
* **Copyright & Licensing Risk:** There have been examples of AI implementations ignoring licensing constraints on libraries, code and other materials that they have obtained online.
* **General Mischief:** AI models have been trained to be helpful, which can lead to them to prioritize following instructions over other concerns such as legality, morality, cost or risk. There is also the possibility that models may have latent agendas that do not align with the instructions they are given. Guardrails and prompt engineering can help to mitigate these risks. 

---

## Technical Architecture & Options

### Workflow Paradigms

It is possible to fit AI into existing workflows or adapt them to maximize benefits:

* **Specification-Driven Development:** Work with LLMs to produce a detailed specification, then have a coding agent implement the plan incrementally or all at once. Focuses heavily on quality and process, requires technical skill, and offers good token cost control.
* **Vibe Coding:** A developer starts with an idea and interactively prompts an agent to progressively build a solution. Focuses on rapid prototyping rather than initial code quality. While it can theoretically be performed by non-technical users, doing so without technical oversight introduces risks in production code bases. Token usage is higher as the model has to think for itself about system design etc.
* **Looping:** Define the exact end result required and set agents off to autonomously complete the task. Requires technical knowledge to define goals well; poses high token usage risks.
* **Autonomous Agentic Tasks:** Background tasks (e.g., creating/deploying builds) handled by scheduled agents. Requires human intervention only when issues occur, alongside effective monitoring and safeguards.

### Harness Options

| Harness Type | Description & Characteristics |
| :--- | :--- |
| **Chatbots** | Very capable of assisting users in advisory or single-task roles, but iterating across multi-file codebases can become onerous. |
| **Coding IDE Tools** | Integrate with existing IDEs (e.g., VS Code) or standalone environments. Provide context-aware chat (can act as an advisor or actually implement changes) and auto-complete (lines or full blocks) based on code or user comments. |
| **Agents** | Execute coding and development tasks autonomously or semi-autonomously. Can be directed by users, triggered by work items, or run on schedules (e.g., security scanning). |

### Model Options & Selection Factors

* **Capability:** Current generalist models perform differently across specific tasks (new code vs. refactoring vs. testing). Modular architectures (e.g., microservices) with smaller code footprints can achieve better results with less complex models.
* **Cost Efficiency:** Evaluates cost-per-token alongside input/output token efficiency. Optimization tools (e.g., Caveman, Ponytail) can reduce token footprints without impacting quality.
* **Open-Weight vs. Closed-Weight:** The balance between security, complexity, availability, performance and costs should be considered. Keeping options open now and in the future is also a consideration.
* **In-House Models:** It is possible to train models specifically for the task – This could provide a better fit and even competitive advantage. Training a whole model from scratch is currently quite a big undertaking, but ‘Post Training’ an existing model can be effective. 

### Hosting Models

| Option | Control & Cost Profile | Key Considerations |
| :--- | :--- | :--- |
| **Third-Party** | High convenience, variable long-term costs. | Mandatory for closed-weight models. Data privacy and cross-border regulatory compliance are key risks. |
| **First-Party** | High control over data and costs. | Hosted on VMs, cloud infrastructure, or on-premises servers. Requires dedicated administrative and security overhead. |
| **Edge / Local** | Maximum privacy and predictable costs. | Hosted directly on developer machines. Constrained by hardware limits, though capability is improving over time. |

### Product Architectures & Ecosystems

* **Codebase Size:** Codebases under 10,000 lines of code yield significantly better results and prevent context rot.
* **Language & Framework Popularity:** Programming languages and frameworks with higher representation in training data yield more accurate outputs.
* **Third-Party Libraries:** Controls must manage third-party dependencies to defend against supply chain attacks.

---

## Governance & Change Management

### Strategic Considerations

* **Buy-in:** Requires alignment across all organizational levels, addressing specific worries and motivations per role.
* **Vendor & Product Dependency:** Subsidized models may become more expensive over time, coupled with the Jevons effect (where lower unit costs increase overall consumption).
* **Security & Data Privacy Frameworks:** Clear guidelines must define private data, prevent unauthorized data transmission to external models, and stop AI from generating compromised code.
* **Evolving Capabilities:** Organizations must balance execution against the ability to change course as technology evolves.

---

## Implementation Plans

The following elements must be structured into the implementation plan:

1. **Consultation & Assessment:** This process can gather information about current AI skills within the organization, attitudes to AI adoption, implementation ideas, potential risks, and current workflows that may be impacted. This should also address shadow AI usage where employees use unapproved tools in development workflows. 
2. **Risk Management:** Risk management is as important with an AI tool rollout as with any other project or programme of work. 
3. **Legal Advice:** Legal advice in the areas of data protection, processing and liabilities for AI actions should be sought – changes may be required to product Terms and Conditions etc. 
4. **Policies & Procedures:** It is important that policies and procedures are in place to govern the use of AI within the organization and that they specifically address development. These policies and procedures need to be communicated effectively to relevant employees. 
5. **Metrics:** How will success of the rollout(s) be measured? How will costs, productivity and quality be monitored and controlled? 
6. **Pilot Implementations:** Piloting of tools and processes can reduce risks and develop best practices before a full rollout. 
7. **Rollout Plan:** A comprehensive rollout plan will cover multiple phases, procurement, procedures and workflows, training, communication, implementation phases, monitoring and reviews. 
8. **Continuous Improvement:** Refining processes and adapting to new innovations. 