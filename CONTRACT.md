# Partite

project
: An effort to create and/or maintain something.

operation
: A modification of a project.

agent
: An entity that can perform an operation.

procedure
: A definition of an action.

administrator
: The agent that executes a given procedure.

role
: A classification of an agent which defines the operations the agent shall perform.
: One of director, consul, judge, architect, developer.

## Acts

decision
: A process that determines if a given operation shall be executed.

act
: An operation that shall only be executed via a decision.

ballot
: A description of a given agent's desire regarding a decision.

voter
: An agent that is eligible to complete a ballot for a given decision.

roll call
: A procedure that requests ballots regarding a decision from its voters.

affirmation
: A procedure that executes an act.

## Standard

policy
: A condition that, when met, triggers a given procedure be executed by its respective administrator.

standard
: A set of policies defined for a project.

sanction
: An act that modifies a standard.

- A project's standard shall define the following for each of its acts: its administrator, a policy for its roll call and a policy for its affirmation.
- Each director shall be a voter in all sanctions.

## Assignment

assignment
: A set of roles that are applied to a given agent.

reassignment
: An act that modifies an actor's assignment.

- A given agent shall not be able to execute any operations that are not explictly included in one of the roles included in their assignment.
- The affirmation of a reassignment that adds any number of roles to an agent's assignment shall only proceed if the agent accepts it.
- Any agent shall be able to execute a reassignment that removes any number of roles from their assignment without a decision.
- When a project is created, all agents responsible for the creation shall have the director role added to their assignment.
- Each director shall be a voter in reassignment acts.

## Vision

vision
: A succinct description of the intention of a project.

adoption
: An act that modifies a vision.

- Each director shall be a voter in all adoptions.

## Contract

requirement
: A description of a desired behavior.

contract
: A set of all the requirements of a project.

enactment
: An act that modifies a contract.

- Each consul shall be a voter in all enactments.

## Strategy

specification
: An explanation of how one or more requirements shall be satisfied.

strategy
: A set of specifications that cover the entirety of a contract.

confirmation
: An act that modifies a strategy.

- Each architect shall be a voter in all confirmations.

## Product

product
: An implementation of a strategy.

authorization
: An act that modifies a product.

- Each judge shall be a voter in all authorizations.

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
2) A consul shall be able to:
   
   a) create an amendment

## IV) Strategy

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

affirmation
: An action that that adds a given flaw to the plan.
        
blueprint
: An object composed of:
- a flaw
- an adaptation
: It can be approved to indicate the adaptation resolves the flaw.

## VI) Product

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
How to add sub projects to a project.
How to branch projects that are have the same vision but different strategies or products.
Suggestions for voting:
- how shall the action be shared, discussed, and modified
- should the initial submitter be allowed to vote
- include a time frame so that votes cannot be dragged out
- consider "blank" ballots where an operative does not submit a ballot
```
