# Assignment
Understand the concepts of HTTP RPC (Remote Procedure Calling) and
implement a simple API in your scenario.
## 1. Find Scenario
<details>
<summary>TASK: Topic: Group 10 -> Event Booking</summary>
You have randomly been assigned a group ID. Use this group ID to find your
scenario from the following list. If your ID is greater than 10, start back at 1, e.g.
13 → 3.

| Group ID | Scenario      | Description                   |
| -------- | ------------- | ----------------------------- |
| 10       | Event Booking | Events, locations, tickets, … |

As a first step, get familiar with your scenario and make sure you have the
same understanding of the general concepts.

> Example: Let’s assume our scenario is a Task Management App.
Users can create tasks, e.g. “Repair bike” and put them onto lists, e.g.
“Sport”. A task can be only be assigned to a single user and is either
completed or not.
</details>

## 2. Create Entity-Relationship Model
<details>
<summary>TASK: ER-Diagram in Mermaid</summary>
To further specify the application, create a small Entity-Relationship Diagram
depicting the important entities, their relations to each other and some
important attributes.
You can use the Live Editor of mermaid.js:

https://mermaid.js.org/syntax/entityRelationshipDiagram.html

> Example: The following ERD allows to implement a very simple task
management app.

```
erDiagram
    User ||--o{ Task : "has many"
    User ||--o{ List : "has many"
    Task }o--|| List : "belongs to"

        Task {
          string title
          bool completed
        }
        User {
          string name
        }
        List {
          string name
        }
```
</details>

## 3. Define Access Patterns
<details>
<summary>TASK: Create access patterns</summary>
Define four (4) access patterns you want to implement for your application. A
single access pattern is best imagined as a screen of an application, which
displays information or allows to enter information. This is always performed as
a role, e.g. a user, a guest, an admin, and so on.<br>
Write them down in a numbered list.

>Example: For the task management app, we want to implement the
following access patterns:
>1. As a logged in user, I want to fetch a list of all my open tasks. The
response should be grouped by lists, so I can put it into nice user
interface.
>2. As a logged in user, I want to create a new task for a list. The
response should return all details of the created task.
>3. As a logged in user, I want to complete a task. The response
should return all details of the created task.
>4. As a logged in user, I want to move a task from one list to another.
The response should return all details of the created task.
</details>

## 4. Implement JSON-RPC API
<details>
<summary>TASK: Install Node Express, create static dataset, implement JSON-RPC request and answers, test with Postman</summary>
**Install Node.js and Express**<br>
Use and install Node.js and the express framework to setup a very lightweight JSON API.

https://nodejs.org/

https://expressjs.com/

Use the express json middleware, to automatically parse JSON:

https://expressjs.com/en/4x/api.html#express.json

**Define Static Dataset**<br>
Next up, define a very simple, static dataset that suits your scenario and allows
you to respond to your access patterns with useful data. You can put it into the
same file as the server.js.

> For the task management app, the dataset could look like the
following. In this example, we use human readable ids, like “bob”,
“shopping” and “buyOranges”, which in a real system would probably be numbers or UUIDs.

```JavaScript
let users = {
    bob: { name: "Bob" },
    alice: { name: "Alice" },
};
let lists = {
    shopping: {
        name: "Shopping",
        userId: "bob",
    },
    sport: {
        name: "Sport",
        userId: "alice",
    },
};
let tasks = {
    buyOranges: {
        title: "Buy Oranges",
        listId: "shopping",
        completed: false,
    },
    repairBike: {
        title: "Repair Bike",
        listId: "sport",
        completed: false,
    },
};
```

**Implement JSON-RPC Requests and Responses**<br>
Carefully read through the JSON-RPC 2.0 specification and make sure you
understand the concepts. Make sure to only use the HTTP POST method to the
same endpoint.

https://www.jsonrpc.org/specification

Now, implement all four access patterns, so they comply with the specification.

**Test with Postman**<br>
Start your API from a terminal and use Postman to test all four access patterns.
Make sure, the server responds as expected. If your restart your API, the
previous data will be lost, but that’s okay for this assignment.
</details>

## Criteria
<details>
<summary>What to pay attention to for grading.</summary>
The following criteria will be used for grading. If all criteria are met, you will
receive 100 points.
|||
|-|-|
|ERD and Access Patterns|You defined four access patterns in the form “<ID>: As a <Role>, I want to be able to <Functionality>”. At least two patterns have to modify - not only read data. The patterns cover useful and common functionality for the scenario and make sense.|
|Implementation|You implemented the functionality using the expected technology. All access patterns are working and following the specification. No extra dependencies, but the specified, are used.|
</details>