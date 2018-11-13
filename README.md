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

### Branching Strategy

We use git flow to maintain and work in our git repositories.

Read [This](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) tutorial to get familiar with it.


## Style Guides
TODO

## On Boarding
TODO
