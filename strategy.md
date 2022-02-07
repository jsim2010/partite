# Partite

AID
: Agent IDentifier
: A symbol that uniquely identifies an agent.

executor
: An agent who follows a specified set of rules as part of the workflow.

## Vision

vision
: A purpose that describes the intention of a concept.
: Should be succinct and avoid any specification or implementation details.

MID
: Motion IDentifier
: A symbol that uniquely identifies a motion

alteration
: A collection of modifications to a vision.

premise
: A description of what an alteration is meant to clarify.

proposer
: An agent who proposed a motion.

motion
: An object composed of:
        - id: a MID
        - proposer: the AID of the proposer
        - alteration: an alteration
        - premise: a premise

amendment
: An object composed of:
        - motion: a motion
        - ayes: a counter of ayes
        - nos: a counter of nos

director
: The role of an agent who creates and maintains the vision.

---
```
graph LR
        1((begin)) --propose--> Motion
        Motion --advance--> Amendment
        Motion --drop--> 2((end))
        Amendment --favor--> Amendment
        Amendment -- oppose--> Amendment
        Amendment --adopt--> 3((adoption))
        Amendment --defeat--> 2((end))
end
```

Any director can propose a motion, which initializes a motion with the following values:
        - id: an identifier unique from the MID's of all motions
        - proposer: the AID of the director who proposed the motion
        - alteration: blank
        - premise: blank
A proposer can:
        - edit the alteration and/or premise of the motion.
        - drop the motion, which deletes it.
        - advance the motion, which initializes an amendment with the following values:
                - motion: the motion that was advanced
                - ayes: 0
                - nos: 0
Every director shall act on each amendment by performing one of the following actions upon it:
        - favoring the amendment, which adds 1 to the ayes.
        - oppposing the amendment, which adds 1 to the nos.
After all directors have acted on an amendment, if the ayes is greater than the nos, an executor shall adopt the amendment, which applies its alteration to the vision; otherwise, an executor shall defeat the amendment by deleting it.

## Contract

contract
: The expectations that an external object requires the concept must meet.

## Strategy

strategy
: A detailed specification of a concept.

mission
: A description of a desired modification to a strategy.
: Should provide the following:
        - an explanation of the current state of the strategy that does not fully meet the vision
        - a proposal to modify the strategy in a way that is believed to better meet the vision

petitioner
: An agent who started a petition.

rationale
: An explanation of why a mission does not fit the scope of a vision or work with the current strategy.

PID
: Petition IDentifier
: A symbol that uniquely identifies a petition.

petition
: An object composed of:
        - id: a PID
        - petitioner: the AID of the petitioner
        - mission: a mission
        - rationales: a list of all rationales from previous denials or appeals of the petition.

appraisal
: An object composed of:
        - petition: a petition

approver
: An agent who approved an appraisal.

revision
: A collection of modifications to a strategy.

flaw
: An explanation of why a revision does not satisfy the intent of a mission.

blueprint
: An object composed of:
        - petition: a petition
        - approver: the AID of the approver
        - revision: a revision
        - flaws: a list of all flaws from previous vetos

designer
: An agent who develops the strategy.

committer
: An agent who committed a blueprint.

review
: An object composed of:
        - blueprint: a blueprint
        - committer: the AID of the committer
        - petitioner_affirmation: a flag indicating the affirmation of the petitioner
        - approver_affirmation: a flag indicating the affirmation of the approver

edition
: The state of a strategy at a given time.

---
```
graph LR
        4((begin)) --start--> Petition
        Petition --tender--> Appraisal
        Petition --withdraw--> 5((end))
        Appraisal --approve--> Blueprint
        Appraisal --deny--> Petition
        Blueprint --commit--> Review
        Blueprint --appeal--> Petition
        Review --affirm--> Review
        Review --confirm--> Edition
        Review --veto--> Blueprint
end
```

Any agent can start a petition, which initializes a petition with the following values:
        - id: an identifier unique from the PID's of all petitions
        - petitioner: the AID of the petitioner
        - mission: blank
        - rationales: empty
The petitioner of a petition can:
        - edit the mission of the petition
        - withdraw the petition, which deletes it.
        - tender the petition, which initializes an appraisal with the following values:
                - petition: the petition that was requested
Any director can perform the following actions on an appraisal:
        - approve it, which initializes a blueprint with the following values:
                - petition: the petition
                - approver: the AID of the approver
                - revision: blank
                - flaws: blank
        - deny it, which appends a rationale to the petition and deletes the appraisal (leaving the petition)
Any designer can perform the following actions on a blueprint:
        - edit its revision
        - appeal it which appends a rationale to the petition and deletes the blueprint (leaving the petition)
        - if the revision is non-empty, commit it, which initializes a review with the following values:
                - blueprint: the blueprint
                - committer: the AID of the committer
                - petitioner_affirmation: false
                - approver_affirmation: false
Both the petitioner and the approver of a petition can perform the following actions on a review containing the petition:
        - veto it, which appends a flaw to the blueprint and deletes the review (leaving the blueprint)
        - affirm it, which sets the appropriate affirmation flag to true
If both affirmation flags of a review are set to true, an executor SHALL confirm the review, which applies the revision to the strategy to generate a new edition.

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
