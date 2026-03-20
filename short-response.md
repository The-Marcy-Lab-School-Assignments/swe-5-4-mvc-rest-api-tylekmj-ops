# Short Response Questions

Answer each question below in your own words. Aim for 3–5 sentences per answer. Be specific — use exact terms and concepts from the lesson.

Your responses will each be evaluated out of 3 points for writing quality and 3 points for technical accuracy (6 points per question, 30 points total).

---

## Question 1 — REST Principles

The Todo Tracker API is a **RESTful** API. Identify at least **3 specific design decisions** in the API that make it RESTful, and explain what each one communicates to a client developer. Consider the URL structure, HTTP methods, and status codes used.

**Your answer here**:
The API uses proper status codes which tells clients how the request data is being handled. The API endpoints uses proper methods such as GET,POST,PATCH,DELETE to communicate to the client what the data is going to do whether that be reading data, deleting it, etc. The endpoint urls are indicating a clear hierarchy which tells clients where the data is coming from when they try handling data from a specific id

---

## Question 2 — Separation of Concerns

What problem is caused by mixing data logic and request/response logic in a single file? What does separating them into a model and controller enable? Be specific about what gets harder and what gets easier.

**Your answer here**:
When you mix data logic and request/response logic in a single file, you get a code monolith where all the logic is handled in one codebase which makes it harder for maintain since you might tons of lines of code if you had multiple controllers. Using the MVC method allows for programmers to separate logic into 3 files which makes the code easier to scale and maintain, also becomes a lot easier for collaboration since all the files are delegated. It becomes harder to do at first because you'll have to do a lot of importing and exporting and it's more coding since you would have to handle the data storing in the model and the logic in the controller, but for larger scale projects it'll be less lines of code to write compared to having everything in one file.

---

## Question 3 — Request Lifecycle

Walk through what happens, step by step, when the user clicks a checkbox to toggle a todo's `isDone` field. Name each file and function in your MVC structure that gets involved, in the order it runs, and describe what it does.

**Your answer here**:
When the user clicks on a checklist, thats considered as the user sending a patch request in this context, which means that the code will start in the index.js file is where the endpoints are stored. Then the endpoint will direct that patch request to the the controllers.js file and go to corresponding controller for updating the isDone field. In the controller.js file, functions from models.js will get imported so that the controllers will have access to the stored data. After getting the request id path parameter, the controller will use a function in todoModel to update isDone based on the id then finally the controller will send a response containing the updated isDone data.

---

## Question 4 — Code Sorting

Below is a `createTodo` function that does everything in one place. For each numbered line, identify whether it belongs in the **model** or the **controller**, and explain why.

```js
const createTodo = (req, res) => {
  /* 1 */ const { task } = req.body;
  /* 2 */ if (!task) return res.status(400).send({ message: 'task is required' });
  /* 3 */ const newTodo = { id: getId(), task, isDone: false };
  /* 4 */ todos.push(newTodo);
  /* 5 */ res.status(201).send(newTodo);
};
```

**Your answer here**:
The first line should be in a controller because the code is handling the request body by parsing it. The second line is also a controller since we're using the request data to send a response. Lines 3 and 4 are both models because they're manipulating the todos data which is stored in an array. Line 5 is a controller since similarly to line 2 we're using request data to send a response.
