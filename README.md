# Breakfast
A repo of all the best practises at Second Closet


## Using Git

### Name Convention
We use 3 different schemes for naming our branches. There should be a JIRA ticket created for each change. If not feel free to create it.

1. Hotfix
    
    This branching name should be used when there is an urgent fix required
    on the master branch.
    ```
    Eq: HOTFIX/PROJ-223/remove-buggy-code
    ```
    
2. OPPREF (Oppressive Refactor)

    This branching name should be used when the work being done is not a business requirement but and optimization for development happiness.
    For example, refactoring code, linting code, deleting unused files, etc.
    
    ```
    Eq: OPPREF/PROJ-224/lint-code
    ```
3. Generic (Task, Story)
    
    For all other purposes use the following branch name strategy.

    ```
    Eq: PROJ-225/add-a-new-user
    ```

### Pull Requests (PR)

#### Name convention
Please name all PRs the same as the branch. The key is that we tag it with the JIRA ticket to ensure that the smart commits are triggered.

### Branching Strategy

We use git flow to maintain and work in our git repositories.

Read [this](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) tutorial to get familiar with it.

## Style Guides
TODO

## On Boarding
Second Closet follows the AGILE Scrum methology.

### Daily Scrum
This is a daily meeting where everyone reports on their progress. More specifically, developers will share what they worked on the prior day, will work on the day and any blockers. Daily SCRUM is timeboxed to 15 minutes. Use this meeting to inform your teammates if you need help!!! We're all in this together :)

### Estimating Stories
Second Closet uses the Fibonacci sequence to estimate the weighting of a story. Please use the table below to guide you with your story estimates.

#### KSENIIA STAY AWAKE !!!!

|points| 1    | 2   | 3   | 5   | 8   | 13   | 21   | ∞   |
|:------:|------|-----|-----|-----|-----|------|------|-----|
|changes|one line change| multiple line changes | multiple files | multiple files | needs break down | needs break down | needs break down | too unknown
|time commitment| < 1 hr | < 2 hrs | < 4 hrs | < 8 hrs | multiple days | one week | whole sprint | requires further discussion
|other notes||||||Large feature||
