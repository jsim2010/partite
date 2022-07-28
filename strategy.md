# Partite

## I) Definitions

operative
: An entity that influences the project.

role
: A classification that can be assigned to an operative which defines the actions that an operative is allowed to perform.

statute
: The conditions which permit modifying the assignment of a specified role to a given operative.

policy
: The conditions that shall cause an operative to execute a specified action.

product
: A result of completing the project.

vision
: A succinct purpose that describes the intention of the project.

requirement
: A description of the behavior that a product is expected to exhibit in response to a given input.

contract
: The collection of requirements that encompass the project.

specification
: An explanation of how a product shall satisfy a requirement.

strategy
: A collection of specifications that cover the entirety of the contract.

vote
: Indicates an operative's opinion on a decision.

blank
: Indicates an operative's vote is not yet known.

register
: A mapping of a list of operatives to their vote.
        
## II) Roles

1) The following roles shall exist:
        a) director: Guides the direction of the project.
        b) executor: Enacts the policies of the project.
        c) consul: Maintains the contract as directed.
        d) architect: Ensures the strategy satisfies the contract.
2) Each role shall have 1 statute for its appointment and 1 statute for its dismissal.
3) Any operative shall be able to dismiss themselves from any of their current roles at any time of their choosing.

## III) Project Creation

1) In order to create a project, one or more operatives shall establish and agree on the following:
        a) The vision of the project.
        b) The appointment and dismissal statutes for each role.
        c) Each of the project's policies.

## IV) Policies

1) A project shall provide the ability to define the following pairs of policies that define how the executor responds to votes.
        a) Motions
                i) adoption: When an executor shall adopt a motion.
                ii) defeat: When an executor shall defeat a motion.



#### 5.1.2) Requests
**acceptance**: When an executor shall accept a request.

**declination**: When an executor shall decline a request.

#### 5.1.3) Amendments
**enactment**: When an executor shall enact an amendment.

**repealment** When an executor shall repeal an amendment.

#### 5.1.4) Blueprints
**approval**: When an executor shall approve a blueprint.

**rejection**: When an executor shall reject a blueprint.

#### 5.1.5) Analyses
**authorization**: When an executor shall authorize an analysis.

**dismissal**: When an executor shall dismiss an analysis.
2) For each pair of policies, the conditions of one policy must have no overlap with the conditions of the other policy.

## 6) Motions

### 6.1) Definitions

**alteration**: a collection of modifications to the statutes, policies, and/or vision of the project.

**premise**: an explanation of what issue an alteration intends to resolve.

**motion**: an object composed of:
- a premise
- an alteration
- a register of each director's vote on weighing the motion

### 6.2) Actions

The following actions related to a motion may be performed:

propose a motion

- Roles: `director`
- Intent: `To improve the statutes, policies or vision of the project.`
- Outcome: `Creates a motion with a premise and alteration and all votes in its register marked as blank.`

weigh a motion

- Roles: `director`
- Intent: `To indicate the director's opinion on the correction improving the project.`
- Outcome: `Marks the director's vote in the motion.` 

adopt a motion

- Roles: `executor`
- Outcome: `Modifies the statutes, policies and/or vision of the project as specified by the alteration.`

defeat a motion

- Roles: `executor`
- Outcome: `Removes the motion from consideration.`

## 7) Contract

### 7.1) Definitions

**objective**: An explanation why the contract needs to be modified.

**petition**: An object composed of:
- an objective
- a register of each director's vote on judging the petition

**directive**: An object composed of:
- an objective

**revision**: A collection of modifications to a contract.

**amendment**: An object composed of:
- an objective
- a revision
- a register of each director's vote on appraising the amendment

**version**: An object composed of:
- the state of the contract at a given point

### 7.2) Actions

introduce a petition

- Roles: `any`
- Intent: `To request the contract be modified to more fully meet the vision.`
- Outcome: `Creates a petition with the objective and all votes in its register marked as blank.`

judge a petition

- Roles: `director`
- Intent: `To indicate the director's opinion on the validity of the objective.`
- Outcome: `Marks the director's vote in the register of the petition.`

accept a petition

- Roles: `executor`
- Outcome: `Creates a directive with the mission of the petition.`

decline a petition

- Roles: `executor`
- Outcome: `Removes the petition from consideration.`

draft an amendment

- Roles: `consul`
- Intent: `To create a revision that fulfills the objective of a directive.`
- Outcome: `Creates an amendment with the objective, the revision and all votes in the register marked as blank.`

appraise an amendment

- Roles: `director`
- Intent: `To indicate the director's opinion on the revision meeting the mission and the vision.`
- Outcome: `Marks the director's vote in the register of the amendment.`

enact an amendment

- Roles: `executor`
- Outcome: `Updates the contract as specified by the revision and creates a version.`

repeal an amendment

- Roles: `executor`
- Outcome: `Creates a directive with the amendment's mission.`

## 8) Strategy

### 8.1) Definitions

**adaptation**: A collection of modifications to a strategy.
        
**blueprint**: An object composed of:
- an amendment
- an adaptation
- a register of each controller's vote on approving the blueprint

**edition**: An object composed of:
- a program
- the state of the strategy at a given time

### 8.2) Actions

design a blueprint

- Roles: `architect`
- Intent: `To create an adaptation that aligns the strategy with an amendment of the contract.`
- Outcome: `Creates a blueprint with the amendment, adaptation and all votes in the register marked as blank.`

review a blueprint

- Roles: `controller`
- Intent: `To indicate the controller's opinion on the blueprint fulfilling the amendment.`
- Outcome: `Marks the controller's vote in the register of the blueprint.`

approve a blueprint

- Roles: `executor`
- Outcome: `Creates an edition with the program from the audit and the state from applying the adaptation to the strategy.`

reject a blueprint

- Roles: `executor`
- Outcome: `Removes the blueprint from consideration and puts the audit back into consideration.`

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

TODO How to close/archive a project.
