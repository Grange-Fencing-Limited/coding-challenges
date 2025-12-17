Master Answer Sheet — Coding Challenges

## React (answers)

Notes: These are minimal components using modern React. Save each as a separate file (e.g., `Greeting.jsx`, `ToggleButton.jsx`, etc.). They are written to be easy to test with React Testing Library.

1) Greeting (Greeting.jsx)
```jsx
export default function Greeting({ name }) {
  return (
    <div>
      Hello, {name ?? 'World'}
    </div>
  );
}
```

2) ToggleButton (ToggleButton.jsx)

```jsx
import React, { useState } from 'react';

export default function ToggleButton({ initialOn = false }) {
  const [on, setOn] = useState(initialOn);
  return (
    <button aria-pressed={on} onClick={() => setOn((s) => !s)}>
      {on ? 'ON' : 'OFF'}
    </button>
  );
}
```

3) Counter (Counter.jsx)

```jsx
import React, { useState } from 'react';

export default function Counter({ start = 0 }) {
    const [value, setValue] = useState(Math.max(0, start));
    return (
        <div>
            <button aria-label="decrement" onClick={() => setValue((v) => Math.max(0, v - 1))}>-</button>
            <span style={{padding: '0 8px'}}>{value}</span>
            <button aria-label="increment" onClick={() => setValue((v) => v + 1)}>+</button>
        </div>
    );
}
```

4) TodoList (TodoList.jsx)

```jsx
export default function TodoList({ items = [] }) {
  if (!items || items.length === 0) return <div>No todos</div>;

  return (
    <ul>
      {items.map((item) => (
        <li
          key={item.id}
          className={item.done ? 'done' : ''}
          style={item.done ? { textDecoration: 'line-through' } : {}}
        >
          {item.text}
        </li>
      ))}
    </ul>
  );
}
```

5) EmailForm (EmailForm.jsx)

```jsx
import React, { useState } from 'react';

export default function EmailForm({ onSubmit }) {
  const [email, setEmail] = useState('');
  const [error, setError] = useState('');

  function isValidEmail(v) {
    if (typeof v !== 'string') return false;
    const at = v.indexOf('@');
    if (at < 1) return false; // must have at least one char before @
    const dot = v.indexOf('.', at + 2);
    return dot > at + 1;
  }

  function handleSubmit(e) {
    e.preventDefault();
    if (isValidEmail(email)) {
      if (onSubmit) onSubmit(email);
      setEmail('');
      setError('');
    } else {
      setError('Invalid email');
    }
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        aria-label="email"
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <button type="submit">Submit</button>
      {error && <div role="alert">{error}</div>}
    </form>
  );
}
```

---

## PHP (answers)

1) maskify

```php
<?php
function maskify(string $s): string
{
    if ($s === '') return '';
    if (strlen($s) < 6) return $s;

    $len = strlen($s);
    $out = '';
    
    for ($i = 0; $i < $len; $i++) {
        if ($i !== 0 && $i < $len - 4 && ctype_digit($s[$i])) {
            $out .= '#';
        } else {
            $out .= $s[$i];
        }
    }
    return $out;
}
```

2) number_to_ordinal

```php
<?php
function number_to_ordinal(int $n): string
{
    $abs = abs($n);
    $mod100 = $abs % 100;
    if ($mod100 >= 11 && $mod100 <= 13) {
        $suffix = 'th';
    } else {
        switch ($abs % 10) {
            case 1: $suffix = 'st'; break;
            case 2: $suffix = 'nd'; break;
            case 3: $suffix = 'rd'; break;
            default: $suffix = 'th';
        }
    }
    return (string)$n . $suffix;
}

```


3) Reverse Polish Notation calculator (`calculate`)

```php
<?php
function calculate(string $input)
{
    $input = trim($input);
    if ($input === '') return 0;

    $tokens = preg_split('/\s+/', $input);
    $stack = [];

    foreach ($tokens as $tok) {
        if (is_numeric($tok)) {
            $stack[] = $tok + 0; // keep numeric type
            continue;
        }

        // operator expected
        if (count($stack) < 2) {
            throw new InvalidArgumentException('Invalid RPN syntax');
        }

        $b = array_pop($stack);
        $a = array_pop($stack);

        switch ($tok) {
            case '+': $stack[] = $a + $b; break;
            case '-': $stack[] = $a - $b; break;
            case '*': $stack[] = $a * $b; break;
            case '/':
                if ($b == 0) throw new InvalidArgumentException('Division by zero');
                $stack[] = $a / $b;
                break;
            default:
                throw new InvalidArgumentException('Unknown token: ' . $tok);
        }
    }

    // If multiple values left, return the top of the stack (last value)
    return end($stack);
}

```

4) Review the example function (multiply)

Given:

```python
def multiply(x, y):
    if y > 0:
        return (1 + multiply(x, y-1))
    else:
        return 0
```

Observations and improvements:
- The function does not use `x` at all. As written it returns `y` for positive y, not x*y.
- Recursion depth: using recursion like this will blow the call stack for large y (e.g., > tens of thousands). Prefer iteration or built-in multiplication.
- Negative y values are not handled.
- Add type hints and docstring, meaningful name, and tests.

Simple fixes in Python (preferred):

```python
def multiply(x: int, y: int) -> int:
    """Return the product of x and y using built-in operator."""
    return x * y
```

If you must implement by repeated addition and handle negative numbers without recursion:

```python
def multiply_iter(x: int, y: int) -> int:
    sign = -1 if (x < 0) ^ (y < 0) else 1
    a, b = abs(x), abs(y)
    result = 0
    for _ in range(b):
        result += a
    return sign * result
```

5) In-place mirroring of a 1D array (PHP)

```php
<?php
function mirror_in_place(array &$arr): void
{
    $n = count($arr);
    for ($i = 0; $i < intdiv($n, 2); $i++) {
        $j = $n - $i - 1;
        $tmp = $arr[$i];
        $arr[$i] = $arr[$j];
        $arr[$j] = $tmp;
    }
}
```

---

## MySQL (answers)

Use the `mysql` CLI or any client. Run the commands below in a safe test environment.

Task 1 — Create DB and users table

```mysql
CREATE DATABASE IF NOT EXISTS test_db;
USE test_db;

CREATE TABLE IF NOT EXISTS users (
                                     id INT AUTO_INCREMENT PRIMARY KEY,
                                     name VARCHAR(100) NOT NULL,
                                     email VARCHAR(150) NOT NULL
);
```

Task 2 — Insert rows and SELECT

```mysql
INSERT INTO users (name, email) VALUES
  ('Alice', 'alice@example.com'),
  ('Bob', 'bob@example.com');
```

-- Select all
```mysql
SELECT * FROM users;
```
-- Select with WHERE

```mysql
SELECT id, name FROM users WHERE email = 'alice@example.com';
```

Task 3 — Update and delete

-- Update name for user id = 1

```mysql
UPDATE users SET name = 'Alicia' WHERE id = 1;
```
-- Verify

```mysql
SELECT * FROM users WHERE id = 1;
```

-- Delete user id = 2

```mysql
DELETE FROM users WHERE id = 2;
```
-- Verify deletion should return zero rows

```mysql
SELECT * FROM users WHERE id = 2;
```

Task 4 — Simple INNER JOIN

```mysql
CREATE TABLE IF NOT EXISTS orders (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT NOT NULL,
  amount DECIMAL(10,2) NOT NULL,
  FOREIGN KEY (user_id) REFERENCES users(id)
);

INSERT INTO orders (user_id, amount) VALUES (1, 19.99), (1, 5.50);

SELECT o.id AS order_id, u.name AS customer, o.amount
FROM orders o
INNER JOIN users u ON o.user_id = u.id;
```

Task 5 — Cleanup (optional)

```mysql
DROP DATABASE IF EXISTS test_db;
```
---