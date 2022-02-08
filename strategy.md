# Partite

## 1) Definitions

The given terms shall be defined as follows:

**product**: The item resulting from the development process.

**project**: The management of the product's development.

**operative**: An entity that influences the development of the product.

**vote**: Indicates an operative's opinion on a decision.

**vision**: A succinct purpose that describes the intention of the product.

**relation**: An item that has a dependence on the product.

**contract**: The expectations that a relation requires the product to meet.

**strategy**: A detailed specification of the product.

**role**: A classification that can be assigned to an operative which defines the actions that an operative is allowed to perform.

**statute**: The conditions which permit modifying the assignment of a specified role to a given operative.

**policy**: The conditions that shall cause an operative to perform a specified action.
        
## 2) Roles

The given roles shall be defined as follows:

**director**: Guides the direction of the project.

**executor**: Enacts the policies of the project.

**architect**: Maintains the strategy as directed.

## 3) Project Creation

In order to create a project, the following steps shall be followed:

1. Establish one or more operatives that shall be assigned the director role.
2. Every director shall agree on the following:
    1. The vision of the project.
    2. The assignment of the executor role to at least 1 active operative.
    3. The assignment and unassignment statutes for each role.
    4. Each of the project's policies.

> TODO: Perhaps codify this more.

## 4) Statutes

Each role shall have an assignment statute and an unassignment statute.

## 5) Policies

The available choices shall at least include:
- UNKNOWN
- YES
- NO

TODO: Who defines/changes the policies?

adoption
> When the executor shall adopt a motion.

defeat
> When the executor shall defeat a motion.

acceptance
> When the executor shall accept an appraisal.

declination
> When the executor shall decline an appraisal.

validation
> When the executor shall validate a blueprint.

invalidation
> When the executor shall invalidate a blueprint.

## Motions

> TODO: Change to include motions for policies and statutes.

premise
> An explanation of what is unclear in the current vision.

alteration
> A collection of modifications to the vision.

amendment
> An object composed of:
        - a premise
        - an alteration

motion
> An object composed of:
        - an admendment
        - a mapping of each director to their vote on adopting the motion.

### Actions

advance an amendment

> Roles: `director`
> Intent: `To propose a modification to the vision to improve its clarity.`
> Outcome: `Creates a motion with the amendment and all votes marked as UNKNOWN.`

support a motion

| Roles | director |
| Intent | To indicate the director desires the motion be adopted. |
| Outcome | Marks the director's vote for the motion as YES. |

oppose a motion

| Roles | director |
| Intent | To indicate the director desires the motion not be adopted. |
| Outcome | Marks the director's vote for the motion as NO. |

adopt a motion

| Roles | executor |
| Outcome | Modifies the vision as specified by the alteration. |

defeat a motion

| Roles | executor |
| Outcome | Removes the motion from consideration. |

## Contract

TODO: How does a contractor modify their contract? Do directors and/or designers need to approve modifications?

## Strategy

critique
: An explanation of why the current strategy does not fully meet the vision.

mission
: An explanation of how the strategy could meet the vision

petition
: An object composed of:
        - a critique
        - a mission

appraisal
: An object composed of:
        - a petition
        - a mapping of each director with their vote on accepting the appraisal

directive
: An object composed of:
        - a mission

revision
: A collection of modifications to a strategy.
        
blueprint
: An object composed of
        - a directive
        - a revision
        - a mapping of each director with their vote on confirming the blueprint

edition
: The state of a strategy at a given time.

### Actions

submit a petition

| Role | any operative |
| Intent | To state the strategy does not meet the full intent of the vision. |
| Outcome | Creates an appraisal with the given petition and all votes marked as UNKNOWN. |

endorse an appraisal

| Role | director |
| Intent | To indicate the director believes the critique is valid. |
| Outcome | Marks the director's vote in the appraisal as YES. |

dispute an appraisal

| Role | director |
| Intent | To indicate the director believes the critique is not valid. |
| Outcome | Marks the director's vote in the appraisal as NO. |

accept an appraisal

| Role | executor |
| Outcome | Creates a directive with the mission. |

decline an appraisal

| Role | executor |
| Outcome | Removes the petition from consideration. |

draft a blueprint

| Role | designer |
| Intent | To make a revision that completes a directive. |
| Outcome | Creates a blueprint with the directive, the revision, and all votes marked as UNKNOWN. |

approve a blueprint

| Role | director |
| Intent | To indicate the director believes the blueprint successfully meets the mission. |
| Outcome | Marks the director's vote in the blueprint as YES. |

disapprove a blueprint

| Role | director |
| Intent | To indicate the director believes the blueprint does not successfully meet the mission. |
| Outcome | Marks the director's vote in the blueprint as NO. |

validate a blueprint

| Role | executor |
| Outcome | Creates an edition. |

invalidate a blueprint

| Role | executor |
| Outcome | Creates a directive from the mission. |

## Product

product
: A result of implementing a strategy.

version
: The state of a product at a given time.

test
: A comparison between an expected output and the output generated after applying a given input to a product.

inspection
: A collection of tests.

RID
: Report IDentifier
: A symbol that uniquely identifies a report.

reporter
: The agent who reported a report.

problem
: A description of a difference between an expected output and the one given after a test.

challenge
: An explanation of why a report does not fit the scope of the strategy.

report
: An object composed of:
        - id: a RID
        - reporter: the AID of the agent who reported the report
        - problem: a problem
        - challenges: a list of challenges

adjustment
: A collection of modifications to an inspection.

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

TODO How to close/archive a project.
