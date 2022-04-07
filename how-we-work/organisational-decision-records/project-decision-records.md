# ODR1: Organisational Decision Records

**Proposed by: JD Bothma, Adi Eyal, Adrian Kearns, Lailah Ryklief**

**Date: 2020-09-16**

**Status: Work in progress**

### Context

Project and organisational decisions are often made on an ad hoc basis, either in meetings, Slack, or around the water cooler. These decisions are often not adequately documented limits communication and our ability to learn from project decision-making. We propose a more formal approach to recording these decisions.

### Benefits

1. ODRs can be useful in project retrospectives to review decision-making and capturing project learnings. In some cases project outcomes differ from the outcomes that were expected at the start of the project. Incorporating an ODR review in the retrospective can help improve future designs and implementation.
2. ODRs also serve as documentation to ensure that all team members are aware of decisions. This is especially important when onboarding new team members.&#x20;

### Proposals

We recognise that additional documentation can additional burden team members with heavy workloads. In light of this, ODRs should only as detailed as is necessary and recognising time constraints. A single sentence can be sufficient as a starting point to allow others to comment and contribute. One proposal is to encourage the use of [Y statements](https://medium.com/@docsoc/y-statements-10eb07b5a177). An example of a Y statement is

```
In the context of the Web shop service,
facing the need to keep user session data consistent and current across shop instances,
we decided for the Database Session State pattern
and against Client Session State or Server Session State
to achieve data consistency and cloud elasticity,
accepting that a session database needs to be designed and implemented.
```

Each template element appears on one line in the above example:

1\. _context_: functional requirement (story, use case) or arch. component,\
2\. _facing_: non-functional requirement, for instance a desired quality,\
3\. _we decided_: decision outcome (arguably the most important part),\
4\. _and neglected_ alternatives not chosen (not to be forgotten!),\
5\. _to achieve_: benefits, the full or partial satisfaction of requirement(s),\
6\. _accepting that_: drawbacks and other consequences, for instance impact on other properties/context and effort/cost (both short term and long term).

Y statements capture a great deal of information in a single, albeit long, sentence.&#x20;
