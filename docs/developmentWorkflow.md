---
sidebar_label: 'Development Workflow'
sidebar_position: 7
---

# Development Workflow

In order to distribute the work among the group elements, several tasks were assigned in Jira Software. 
We adopted three possible states for the Jira tasks as suggested by the software:
* To do - whenever a task was merely discussed and defined by the team and no work has been done yet;
* In progress - during the development of the task or when it has been finished but is waiting for tests and deployment (this requires team communication);
* Done - when the task meets the requirements of DoD (Definition of Done).

Each one of those tasks is focused on the development of a certain feature of a user story. In terms of development, a branch was created in GitHub for each Jira feature so that the work remains organized and easy to follow and track. Whenever the development of a task is completed (regarding the Definition of Done), and all tests are passing, a deploy to a staging environment or/and to a production environment is done, via Jenkins pipeline. 

When it comes to code review, we defined that for each Pull Request, there should be at least one reviewer apart from the element that started the Pull Request.
Regarding branch protection rules, we decided to lock Pushes for both “develop” and “main” branches in order to prevent unwanted errors/problems (in case someone forgot to create a branch to develop a feature).

Every once in a while, a Pull Request is made from the "develop" branch to the "main" branch in order to maintain a stable version of the module.
