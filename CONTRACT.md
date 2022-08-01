# Partite

## I) General

vision
: A succinct purpose that describes the intention of the project.

requirement
: A description of the behavior to a given set of inputs that fulfills the vision.

contract
: The collection of requirements enacted by the project.

specification
: An explanation of how one or more requirements shall be satisfied.

strategy
: A collection of specifications that cover the entirety of the contract.
: Any number of strategies may be defined for the contract.

product
: A result of executing a strategy.
: Any number of products may be created for a strategy.
        
## II) Roles

operative
: An entity that acts on the project.

role
: A classification that can be assigned to an operative which defines the actions that an operative is allowed to perform.

statute
: The conditions which permit modifying the assignment of a specified role to a given operative.

1) The following roles shall exist:
  - a) director: guides the direction of the project.
  - b) consul: maintains the contract of the project as directed.
  - c) architect: ensures a strategy satisfies the contract.
  - d) developer: creates a product that executes a strategy.
2) Each role shall have 1 statute for its appointment and 1 statute for its dismissal.
3) **Resignation:** Any operative shall be able to dismiss themselves from any of their current roles at any time of their choosing.

## III) Policies

policy
: A defined set of conditions that, when they occur, shall immediately result in a specified action.

vote
: An act of deciding if an action shall be taken.
: The outcomes of a vote shall be one of the following:
  - AFFIRMED: the action shall be taken
  - UNAFFIRMED: the action shall not be taken

ballot
: A declaration of an operative's opinion on a vote.
: A ballot shall be one of the following options: 
  - AGREE: the operative desires the action be done
  - DENY: the operative desires the action not be done

1) Each type of vote described in this contract shall have a policy that defines how a vote is initiated and how the ballots for a given vote shall determine the decision.

## IV) Motions

premise
: An explanation of why the statutes, policies, and/or vision of the project should be improved.

docket
: The list of accepted premises.

alteration
: A collection of modifications to the statutes, policies, and/or vision of the project.

motion
: An object composed of:
- a list of premises
- an alteration

1) Any director may create a premise.
2) **Premise Acceptance:** Any director may submit a ballot for a vote on accepting a premise.
3) If a premise acceptance is affirmed, the premise is added to the docket.
4) Any director may create a motion that contains one or more of the premises in the docket.
5) **Motion Adoption:** Any director may submit a ballot for a vote on adopting a motion.
6) If a motion adoption is affirmed, each premise in the motion is removed from the docket and the modifications are applied.

## V) Contract

objective
: An explanation of why the contract should be modified.

agenda
: A list of confirmed objectives.

revision
: A collection of modifications to a contract.

amendment
: An object composed of:
- an objective
- a revision

version
: An object composed of:
- the revision that created the version
- the contract at a given time
- a name

1) Any operative may create an objective.
2) **Objective Ratification:** Any director may submit a ballot for a vote on ratifying an objective.
3) If an objective ratification is affirmed, the objective is added to the agenda.
4) Any consul may create an amendment that contains an objective from the agenda.
5) **Amendment Enactment:** Any director may submit a ballot for a vote on enacting an amendment.
6) If an amendment enactment is affirmed, the objective is removed from the agenda, the revision is applied, and a version is created.

## VI) Strategy

flaw
: An explanation of how the strategy does not fulfill the contract.

plan
: A list of flaws.

adaptation
: A collection of modifications to a strategy.
        
blueprint
: An object composed of:
- a flaw
- an adaptation

edition
: An object composed of:
- the adaptation that created the edition
- the state of the strategy at a given time
- a name

1) When a version is created, a flaw shall be created for fulfilling the new version and added to the plan.
2) Any operative may create a flaw.
3) **Flaw Confirmation:** Any consul may submit a ballot for a vote on confirming a flaw.
4) If a flaw confirmation is affirmed, the flaw is added to the plan.
5) Any designer may create a blueprint that contains a flaw from the plan.
6) **Blueprint Approval:** Any consul may submit a ballot for a vote on approving a blueprint.
7) If a blueprint approval is affirmed, the flaw is removed from the plan, the adaptation is applied, and an edition is created.

## 10) Product

### 10.1) Definitions

problem
: A description of a difference between an expected output and the one given after a test.

report
: An object composed of:
        - problem: a problem


argument
: An explanation of why the product will not be able to pass a given inspection.

issue
: An object composed of:
        - report: the report
        - adjustment: the adjustment
        - arguments: a list of arguments

inspector
: An agent who develops the inspection.

upgrade
: An object composed of:
        - edition: the edition
        - adjustment: the adjustment
        - arguments: a list of arguments

ratifier
: An agent who ratified an issue or upgrade.

patch
: A collection of modifications to a product.

defect
: An explanation of how running an inspection with the given patch did not produce the expected outputs.

task
: An object composed of:
        - cause: the issue or upgrade from which the task was generated
        - inspector: the AID of the agent who generated the task
        - patch: a patch
        - defects: a list of defects

developer
: An agent who develops the product.

submitter
: An agent who submitted a submission.

submission
: An object composed of:
        - task: the task
        - submitter: the AID of the agent who submitted this

version (change to release)
: The state of a product at a given time.

---
```
graph LR
        3((begin)) --report--> Report
        Report --publish--> Issue
        Report --redact--> 4((end))
        Issue --ratify--> Task
        Issue --contend--> Report
        Edition --bump--> Upgrade
        Upgrade --authorize--> Task
        Task --implement--> Submission
        Task --protest--> fork
        fork{ } --> Upgrade
        fork --> Issue
        Submission --certify--> Version
        Submission --reject--> Task
end
```

Any agent can report a report, which initializes a report with the following values:
        - id: an identifier unique from the RID's of all reports
        - reporter: the AID of the agent who reported the report
        - problem: blank
        - challenges: empty
The reporter can perform the following actions on the report:
        - edit its problem
        - redact it, which deletes the report
        - publish it, which initializes an issue with the following values:
                - report: the report that was published
                - adjustment: empty
Any inspector can perform the following actions on an issue:
        - edit its adjustment
        - contend it, which appends a challenge to the report and deletes the issue (leaving the report)
        - if the adjustment is non-empty and covers the problem, ratify the issue, which initializes a task with the following values:
                - cause: the issue from which the task was generated
                - inspector: the AID of the inspector
                - patch: blank
                - defects: empty
When an edition is generated, an executor shall bump it, which initializes an upgrade with the following values:
        - edition: the edition
        - adjustment: empty
Any inspector can perform the following actions on an upgrade:
        - edit its adjustment
        - if the adjustment is non-empty and covers the revision of the edition, authorize the upgrade, which initializes a task with the following values:
                - cause: the upgrade from which the task was generated
                - inspector: the AID of the inspector
                - patch: blank
                - defects: empty
Any developer can perform the following actions on a task:
        - edit its patch
        - protest it, which appends an argument to the issue or upgrade and deletes the task (leaving the issue or upgrade)
        - if its patch is non-empty, implement the task, which initializes a submission with the following values:
                - task: the task
                - submitter: the submitter
An executor shall perform the inspection on the product with the patch applied. If the inspection passes, the executorshall certify the submission, which applies the patch to the product to create a new version. Otherwise, the executor shall reject the submission, which appends a defect to the task and deletes the submission (leaving the task).

```
These shall be moved to their respective sections.
1) A project shall have defined the following pairs of policies that define how the executor responds to votes.
  - e) Analyses
    + i) endorsement: When an executor shall endorse an analysis.
    + ii) refusal: When an executor shall refuse an analysis.
```

APPENDIX

**piece**: A part of the product that, by itself, meets a specification.

The following table shows the relation of the different entities in a project.
| Single  | requirement | specification | piece |
| Collection | contract | strategy | product |
| Modifications | revision | adaptation | patch |
| State | version | edition | release |



## 8) Inspection

### 8.1) Definitions

**test**: A comparison between a requirement and the actual outcome of the product.

**inspection**: A collection of tests that cover the entirety of the contract.

**adjustment**: A collection of modifications to the inspection.

**analysis**: An object composed of:
- an issue
- an adjustment
- a register of each consul's vote on authorizing the analysis.

**program**: An object composed of:
- an issue
- the state of the inspection at a given time

### 8.2 Actions

present an analysis

- Roles: `controller`
- Intent: `To request the inspection be modified in order to cover the issue.`
- Outcome: `Creates an analysis with the issue, the adjustment, and all votes in the register marked as blank.`

assess an analysis

- Roles: `consul`
- Intent: `To indicate the consul's opinion on the adjustment sufficiently covering the issue.`
- Outcome: `Marks the consul's vote in the register of the analysis.`

authorize an analysis

- Roles: `executor`
- Outcome: `Creates a program with the issue from the analysis and the inspection after applying the adjustment.`

dismiss an analysis

- Roles: `executor`
- Outcome: `Removes the analysis from consideration and returns its issue to consideration.`

```
How to divide a project into sub projects.
How to branch projects that are taking separate paths.
Suggestions for voting:
- how shall the action be shared, discussed, and modified
- should the initial submitter be allowed to vote
- include a time frame so that votes cannot be dragged out
- consider "blank" ballots where an operative does not submit a ballot
Rules for the name - perhaps semantic versioning?
```
