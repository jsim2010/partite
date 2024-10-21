# Partite

operation
: An interaction with a project.

agent
: An entity that performs an operation.

vote
: A determination if a given operation shall be executed.

action
: An operation that shall only be executed after a vote affirms it.

ballot
: A declaration of a given agent's desire concerning a given vote.

voter
: An agent that is eligible to submit a ballot for a given vote.

roll call
: An operation that requests ballots concerning a given vote from its voters.

affirmation
: An operation that determines if a vote's action shall be executed.

## Assignment

role
: A classification of an agent which defines the operations the agent is eligible to perform.
: One of director, consul, inspector, architect, developer.

assignment
: A set of roles that are applied to a given agent.

reassignment
: An action that modifies an actor's assignment.

An agent must accept the addition of a role to their assignment.

A given agent shall not be able to execute any operations that are not explictly included in one of the roles included in their assignment.

When an agent requests any of the roles in their assignment be removed, it shall be done.

When a project is created, all agents responsible for the creation shall have the director role added to their assignment.

Each director shall be a voter in all reassignments.

## Standard

policy
: A condition that, when met, triggers the execution of a given operation.

standard
: A set of policies.

sanction
: An action that modifies a standard.

A project's standard shall define a policy for both the roll call and the affirmation of each defined action.

Each director shall be a voter in all sanctions.

## Vision

vision
: A succinct purpose tha describes the intention of a project.

adoption
: An action that modifies a vision.

Each director shall be a voter in all adoptions.

## Contract

requirement
: A description of a desired behavior.

contract
: A set of all the requirements of a project.

enactment
: An action that modifies a contract.

Each director shall be a voter in all enactments.

---



## Definitions

adjustment
: A set of modifications to a given standard.

alteration
: A set of modifications to a given vision.

edit
: A collection of modifications to a contract.

revision
: An object composed of:
  
  - a contract after an edit has been applied to it
  - the edit that was applied

objective
: An explanation of why the contract does not fulfill the vision.

agenda
: The list of objectives to be resolved.

ratification
: An action that adds a given objective to the agenda.

amendment
: An object composed of:
  
  - a non-empty set of objectives in the agenda
  - an edit intended to resolve the objectives

enactment
: An action on a given amendment that removes each of its objectives from the agenda, applies the edit to the contract, then creates a revision with the amendment and the new contract.

1) A director shall be able to:
   
   a) create an objective
   
   b) tender a ballot for a ratification
   
   c) tender a ballot for an enactment
2) A consul shall be able to:
   
   a) create an amendment

## IV) Strategy

specification
: An explanation of how one or more requirements shall be satisfied.

strategy
: A collection of specifications that cover the entirety of the contract in a given revision.

adaptation
: A collection of modifications to a strategy.

edition
: An object composed of:

  - a strategy after an adaptation has been applied to it
  - the adaptation that was applied

flaw
: An explanation of how a given strategy does not fulfill a given contract.

plan
: A list of flaws to be resolved for a given strategy.

confirmation
: An action that that adds a given flaw to the plan.
        
blueprint
: An object composed of:
- a flaw
- an adaptation
: It can be approved to indicate the adaptation resolves the flaw.

affirmation:
: An action on a given blueprint that removes the flaw from the plan, applies the adaptation, and creates an edition.

## VI) Product

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

## VII) Report

submission
: An object composed of:
- a revision of a contract
- a version of a product
: If can be endorsed to indicate the desire to test that the version satisfies the revision.

inspection
: An object composed of:
- a submission
- a requirement from the submission's revision

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
2) If a submission endorsement is affirmed, new inspections are added to the program, one for each requirement in the revision.
3) If an analysis certification is affirmed, its inspection is removed from the program and the analysis is added to its respective report.

## VIII) Roles

### C) Investigators

1) An investigator may create an analysis from an inspection in the program.
2) An investigator may tender a ballot for the following votes:
  - a) certifying an analysis
  - b) approving a blueprint

### D) Architects

1) An architect may create:
  - a) a submmission
  - b) a blueprint using a flaw in the plan.
3) An architect may tender a ballot for the following votes:
  - a) endorsing a submission
  - b) confirming a flaw
  - b) authorizing a proposal

### E) Developers

1) A developer may create a proposal that contains a task from the tasklist.


An executor shall perform the inspection on the product with the patch applied. If the inspection passes, the executor shall certify the submission, which applies the patch to the product to create a new version. Otherwise, the executor shall reject the submission, which appends a defect to the task and deletes the submission (leaving the task).

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
```
