# Partite
        
## I) Statutes

operative
: An entity that acts on the project.

role
: A classification that can be assigned to an operative which defines the actions that the operative is allowed to perform.

statute
: The conditions which permit modifying the assignment of a given role to an operative.

1) Each role shall have at least 1 statute for its appointment and at least 1 statute for its dismissal.
2) **Resignation:** Any operative shall be able to dismiss themselves from any of their current roles at any time of their choosing.

## II) Policies

policy
: A defined set of conditions that, when they occur, shall immediately result in a specified action.

vote
: An act of deciding if an action shall be taken.
: The outcomes of a vote shall be one of the following:
  - AFFIRMED: the action shall be taken
  - DENIED: the action shall not be taken

ballot
: A declaration of an operative's opinion on a vote.
: A ballot shall be one of the following options: 
  - APPROVE: the operative desires the action be done
  - DISAPPROVE: the operative desires the action not be done

1) Each type of vote described in this contract shall have a policy that defines:
  - a) when a vote is initiated
  - b) when a vote shall be affirmed
  - c) when a vote shall be denied

## III) Motions

vision
: A succinct purpose that describes the intention of the project.

premise
: An explanation of why the statutes, policies, and/or vision of the project should be improved.
: It can be accepted to indicate it is desirable that the premise be resolved.

docket
: A list of accepted premises.

alteration
: A collection of modifications to the statutes, policies, and/or vision of the project.

motion
: An object composed of:
- a list of 1 or more premises that are currently in the docket
- an alteration
: It can be adopted to indicate the alteration shall be applied in order to resolve the list of premises.

1) A vote shall decide the following actions:
  - a) the acceptance of a premise
  - b) the adoption of a motion
2) If a premise acceptance is affirmed, the premise shall be added to the docket.
3) If a motion adoption is affirmed, each premise in the motion is removed from the docket and the alteration is applied.

## IV) Contract

requirement
: A description of a behavior that fulfills the vision. It is comprised of a set of inputs and the expected outcome.

contract
: All of a project's requirements.

objective
: An explanation of why the contract should be modified.
: It can be ratified to indicate it is desirable that the objective be resolved.

agenda
: A list of ratified objectives.

edit
: A collection of modifications to a contract.

amendment
: An object composed of:
- an objective from the agenda
- an edit
: It can be enacted to indicate the edit shall be applied to the contract in order to resolve the objective.

revision
: An object composed of:
- the edit that created the revision
- the contract after the given edit was applied
- a name

1) A vote shall decide the following actions:
  - a) the ratification of an objective
  - b) the enactment of an amendment
2) If an objective ratification is affirmed, the objective is added to the agenda.
3) If an amendment enactment is affirmed, the objective is removed from the agenda and a revision is created.

---
Need to go review everything below

## V) Report

submission
: An object composed of:
- a revision of a contract
- a version of a product
: If can be endorsed to indicate the desire to test that the version satisfies the revision.

inspection
: An object composed of:
- a submission
- a requirement from the revision

program
: A list of incomplete inspections.

analysis
: An object composed of:
- an inspection
- a record of a version's behavior when the set of inputs in a requirement are applied
- an statement describing if the version's behavior met the expectations of the requirement
: It can be certified to confirm that its information is accurate.

report
: An object composed of:
- a collection of analyses of the same submission

1) A vote shall decide the following actions:
  - a) an enodorsement of a submission
  - b) a certification of an analysis
2) If a submission endorsement is affirmed, a new inspection with the submission for each requirement in the revision is created and added to the program.
3) If an analysis certification is affirmed, its inspection is removed from the program and the analysis is added to its respective report.

## VI) Strategy

specification
: An explanation of how one or more requirements shall be satisfied.

strategy
: A collection of specifications that cover the entirety of a contract.

flaw
: An explanation of how a strategy does not fulfill the contract.
: It can be confirmed to indicate the flaw is valid.

plan
: A list of flaws.

adaptation
: A collection of modifications to a strategy.
        
blueprint
: An object composed of:
- a flaw
- an adaptation
: It can be approved to indicate the adaptation resolves the flaw.

edition
: An object composed of:
- the adaptation that created the edition
- the state of the strategy at a given time
- a name

1) When a revision is created, one or more flaws shall be created for fulfilling the new revision and added to the plan.
2) If a flaw confirmation is affirmed, the flaw is added to the plan.
3) If a blueprint approval is affirmed, the flaw is removed from the plan, the adaptation is applied, and an edition is created.

## VII) Product

product
: An execution of a strategy.

defect
: A failed analysis

upgrade
: An object composed of:
- an edition

task
: An object that is either a defect or upgrade.

tasklist
: A collection of tasks.

patch
: A collection of modifications to a product.

proposal
: An object composed of:
- the task
- a patch
: It can be authorized to indicate the patch resolves the task.

version
: The state of a product at a given time.

1) When an edition is created, an upgrade shall be created from it and added to the tasklist.
2) If a proposal authorization is affirmed, the task is removed from the tasklist, the patch is applied, and a version is created.

## Roles
1) The following roles shall exist:
  - a) director
  - b) consul
  - c) inspector
  - d) architect
  - e) developer
  - f) member
2) All operatives shall not be able to perform any actions that are not explictly given to one of their assigned roles.
3) 
### A) Directors

1) A director may create:
  - a) a premise
  - b) a motion
2) A director may tender a ballot for the following votes:
  - a) accepting a premise
  - b) adopting a motion
  - c) ratifying an objective
  - d) enacting an amendment

### B) Consuls

1) Any consul may create an amendment.

### C) Investigators

1) Any investigator may create an analysis from an inspection in the program.
2) Any investigator may tender a ballot for the following votes:
  - a) certifying an analysis
  - b) approving a blueprint

### D) Architects

1) Any architect may create:
  - a) a submmission
  - b) a blueprint using a flaw in the plan.
3) Any architect may tender a ballot for the following votes:
  - a) endorsing a submission
  - b) confirming a flaw
  - b) authorizing a proposal

### E) Developers

1) Any developer may create a proposal that contains a task from the tasklist.

### F) Members

1) Any member may create:
  - a) an objective
  - b) a flaw

---

Any agent can report a report, which initializes a report with the following values:
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

APPENDIX

**piece**: A part of the product that, by itself, meets a specification.

The following table shows the relation of the different entities in a project.
| Single  | requirement | specification | piece |
| Collection | contract | strategy | product |
| Modifications | revision | adaptation | patch |
| State | version | edition | release |



```
How to divide a project into sub projects.
How to branch projects that are taking separate paths.
Suggestions for voting:
- how shall the action be shared, discussed, and modified
- should the initial submitter be allowed to vote
- include a time frame so that votes cannot be dragged out
- consider "blank" ballots where an operative does not submit a ballot
Rules for the name - perhaps semantic versioning?
Specifications can be seen as requirements for unit tests. Is there a way to test them?
```
