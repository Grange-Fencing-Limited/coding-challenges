### React Tests

Five small React tasks intended to be implemented and tested with Jest + React Testing Library.

### Task 1

Create a functional component `Greeting` that renders a greeting message.

Requirements:

- The component accepts a prop `name` (string).
- If `name` is provided, render `Hello, {name}`; otherwise render `Hello, World`.
- Export the component as the default export.
- Keep it a simple, pure functional component (no hooks required).

Example assertions (tests):

- Render `<Greeting name="Alice" />` and expect the text content to contain `Hello, Alice`.
- Render `<Greeting />` and expect the text content to contain `Hello, World`.

---

### Task 2

Create a `ToggleButton` component that toggles between `ON` and `OFF`.

Requirements:

- Accepts an optional boolean prop `initialOn` (default: `false`).
- Clicking the button toggles the displayed state between `ON` and `OFF`.
- The button should have `aria-pressed` reflecting the current on/off state (true when ON).
- Keep implementation simple using `useState`.

Example assertions:

- Render `<ToggleButton initialOn={true} />` and expect initial text `ON` and `aria-pressed="true"`.
- Simulate a click and expect `OFF` and `aria-pressed="false"`.

---

### Task 3

Create a `Counter` component with increment and decrement controls.

Requirements:

- Accepts a numeric prop `start` (default: `0`).
- Renders the current value and two buttons labelled `+` and `-`.
- Clicking `+` increments the value by 1; `-` decrements by 1.
- Do not allow the counter to go below 0 (it should stay at 0 if `-` is clicked at 0).

Example assertions:

- Render `<Counter start={2} />`, click `+`, expect value `3`.
- Render `<Counter start={0} />`, click `-`, expect value `0` (not negative).

---

### Task 4

Create a `TodoList` component that renders a list of todos.

Requirements:

- Accepts a prop `items` which is an array of objects: `{ id: string|number, text: string, done?: boolean }`.
- Render each todo's text in a list (`<ul>` / `<li>`). Use `id` as the React key.
- If `items` is empty, render the message `No todos`.
- For each item that has `done: true`, render the text with a `line-through` style or add a `done` class.

Example assertions:

- Render with `items` containing two todos and expect two `<li>` elements with the correct text.
- Render with `items = []` and expect to see `No todos`.
- Render an item with `done: true` and assert the element has the `done` class or a `text-decoration: line-through` style.

---

### Task 5

Create a simple `EmailForm` component that validates an email and calls `onSubmit`.

Requirements:

- Renders a text input (type `email` or `text`) and a submit button.
- Accepts an `onSubmit` prop (function). When a valid email is submitted, call `onSubmit(email)` and clear the input.
- If the email is invalid, do not call `onSubmit` and render an error message `Invalid email`.
- Keep validation simple (e.g., check for presence of `@` and `.` after `@`).

Example assertions:

- Type a valid email into the input, click submit, and expect `onSubmit` to have been called once with the email, and the input is emptied.
- Type `not-an-email`, click submit, and expect `onSubmit` not to have been called and the error message `Invalid email` to be present.

---

Notes:

- These tasks are intentionally small and unit-test focused. Use React Testing Library for rendering and firing events, and Jest for assertions and mocks.
- Keep components minimal and easy to test.

