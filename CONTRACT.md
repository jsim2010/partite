# Partite
        
## Structure

operative
: An entity that operates on the project.

policy
: A condition that when met, triggers the execution of a given operation.

vote
: A defined process of determining if a given operation shall be executed.

action
: An operation that can only be executed via a vote.

ballot
: A declaration of a given voter's desire concerning a given vote.

role
: A classification that can be assigned to an operative which defines the operations the operative is allowed to perform.

reassignment
: An action that modifies the assignment of a given role to an operative.

---

1) A ballot shall declare one of the following:

   a) *Approve*: the voter desires the action be executed
   
   b) *Disapprove*: the voter desires the action not be executed
2) Each defined action shall have a policy for each of the following operations:
   
   a) *Vote Initiation*: when a vote for the action shall be initiated
   
   b) *Affirmation*: when the action shall be executed
3) The possible types of reassignment shall be:
   
   a) *Appointment*: Adds a role assignment
   
   b) *Dismissal*: Removes a role assignment
4) Each role shall have at least 1 policy for its appointment.
5) **Resignation**: Any operative shall be able to dismiss themselves from any of their current roles at any time.
6) The following roles shall exist:
   
   a) director
   
   b) consul
   
   c) inspector
   
   d) architect
   
   e) developer
7) Each operative shall not be able to execute any operations that are not explictly given to one of their assigned roles.
8) **Founders**: When a project is created, all operatives responsible for the creation shall be appointed the director role.
9) A director shall be able to:
   
   a) tender a ballot for a reassignment of any role

## Vision

vision
: A document containing a succinct purpose that describes the intention of the project.

premise
: An explanation of why the policies and/or vision of the project should be improved.

docket
: The list of premises to be resolved.

acceptance
: An action that adds a given premise to the docket.

alteration
: A collection of modifications to the policies and/or vision of the project.

motion
: An object composed of:
  
  - a set of references to 1 or more premises in the current docket
  - an alteration

adoption
: An action on a given motion that removes each of its premises from the docket and applies the alteration to the components of the project.

---

1) A director shall be able to:
   
   a) create a premise
   
   b) create a motion
   
   c) tender a ballot for an acceptance
   
   d) tender a ballot for an adoption

## Contract

requirement
: An object composed of:

  - a set of inputs
  - the behavior that fulfills the vision

contract
: A list containing all requirements of a project.

objective
: An explanation of why the contract should be modified.

agenda
: The list of objectives to be resolved.

ratification
: An action that adds a given objective to the agenda.

edit
: A collection of modifications to a contract.

amendment
: An object composed of:
  
  - a set of references to 1 or more objectives in the agenda
  - an edit

revision
: An object composed of:
  
  - an amendment
  - a contract

enactment
: An action on a given amendment that removes each of its objectives from the agenda, applies the edit to the contract, then creates a revision with the amendment and the new contract.

---

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

`perhaps add a step that formally defines the process of generating flaws from a revision`

1) When a revision is created, one or more flaws shall be created for fulfilling the new revision and added to the plan.
2) If a flaw confirmation is affirmed, the flaw is added to the plan.
3) If a blueprint approval is affirmed, the flaw is removed from the plan, the adaptation is applied, and an edition is created.

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
Specifications can be seen as requirements for unit tests. Is there a way to test them?
```
