# Development Workflow Process

![ProductOps - Development Workflow (Jira).jpg](./attachments/ProductOps%20-%20Development%20Workflow%20(Jira).jpg)

###### Edit on:

[https://miro.com/app/board/o9J_lZXSFDM=/](https://miro.com/app/board/o9J_lZXSFDM=/)


---

## Normal Flow

| **Move**                           | **When**                                                                                                                               | **By**          |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| Roadmap 
>> Backlog                | Create a story or hotfix, they’re added automatically                                                                                  | Product Manager |
| Backlog 
>> To Do                  | A story or hotfix fit into the sprint/week’s scope                                                                                     | Product Manager |
| To Do 
>> In Progress              | Start working on the story, hotfix or sub-task                                                                                         | Developer       |
| In Progress 
>> Code Review        | Finished the development                                                                                                               | Developer       |
| Code Review 
>> Ready For QA       | Code is acceptable and integrated to the parent’s branch.
🔗 [See Git Management](https://blackstonestudio.atlassian.net/l/c/E5g1EgQM) | Product Manager |
| Ready For QA 
>> Ready For Release | Code completely performs the expected and the whole system remains working                                                             | Product Manager |
| Ready For Release 
>> Done         | Code was integrated to the develop branch. 
🔗 [See Git Management](https://blackstonestudio.atlassian.net/l/c/E5g1EgQM)               | Product Manager |

## Reopened Flow

| **Move**                       | **When**                                                   | **By**          |
| ------------------------------ | ---------------------------------------------------------- | --------------- |
| Code Review 
>> Reopened       | Code failed unit testing or it breaks something else       | Dev Lead        |
| Ready For QA 
>> Reopened      | Issues were found or task is incomplete                    | QA Specialist   |
| Ready For Release 
>> Reopened | Something went wrong and cannot merge to develop or master | Product Manager |
| >> Blocked                     | People, time or resources are missing so we can’t continue | Product Manager |


---

> Legacy flow
>
> `Unknown Attachment`
> [https://drive.google.com/file/d/1qP8qLotkKWu3CMVJSFE11V29zeTOm52d/view?usp=sharing](https://drive.google.com/file/d/1qP8qLotkKWu3CMVJSFE11V29zeTOm52d/view?usp=sharing)


