# Stack & Queue in Python — Class-Based Data Structures

A deep dive into two of the most fundamental data structures, why OOP is the natural way to build them, and how they solve real problems.

> **Before the theory — a real problem:**
> You're asked to evaluate `((2+3)*5/5)` in code — without using Python's built-in `eval()`. Separately, you need to build a queue for a ticket counter, but `collections.deque` hasn't been taught yet — only plain lists (`[]`). Both problems get solved the same way: wrap a plain list inside a class, and let the class enforce the rules (LIFO for Stack, FIFO for Queue). By the end of this guide, you'll solve both — see section 2.7 for the expression, and section 3 for the queue.

---

## 1. Why We Need OOP for Data Structures

A data structure isn't just "data" — it's data **plus the rules for how you're allowed to touch it**. That combination is exactly what a class gives you.

- **Encapsulation:** The internal list/array that stores the data can be hidden (`_items` or `__items`), so users interact only through controlled methods like `push()`, `pop()`, `enqueue()`, `dequeue()`. This prevents someone from directly corrupting the internal state (e.g., inserting in the middle of a stack, which shouldn't be allowed).
- **Reusability:** Once you define a `Stack` class, you can create as many independent stacks as you want — each an `Stack()` instance with its own state — without rewriting logic.
- **Real-world modeling:** A stack of plates, a queue at a ticket counter — these are naturally "objects with behavior," which maps directly onto a class (state = the items; behavior = push/pop or enqueue/dequeue).
- **Abstraction:** Code that *uses* a stack doesn't need to know it's backed by a Python list internally. If you later swap the internal implementation (list → linked list), nothing outside the class needs to change.

This is the core argument for OOP in data structures: **bundle data with the operations that are valid on that data, and hide everything else.**

---

## 2. Stack

### 2.1 What Is a Stack?

A **Stack** is a **LIFO** (Last In, First Out) structure. The last item added is the first one removed — like a stack of plates: you add to the top, and you remove from the top.

**Core operations:**
- `push(item)` — add an item to the top
- `pop()` — remove and return the top item
- `peek()` — look at the top item without removing it
- `is_empty()` — check if the stack has anything in it

### 2.2 Why Stacks Are Used

- **Undo/Redo** in text editors — every action pushed onto a stack; undo pops the last one
- **Function call management** — the "call stack" in every programming language works this way
- **Browser back button** — each visited page is pushed; back pops the most recent
- **Expression evaluation and parsing** — matching brackets, evaluating postfix/prefix expressions
- **Backtracking algorithms** — maze solving, DFS traversal

### 2.3 Class-Based Implementation

```python
class Stack:
    def __init__(self):
        self._items = []   # protected — internal storage, not meant for direct access

    def push(self, item):
        self._items.append(item)

    def pop(self):
        if self.is_empty():
            raise IndexError("pop from an empty stack")
        return self._items.pop()

    def peek(self):
        if self.is_empty():
            raise IndexError("peek from an empty stack")
        return self._items[-1]

    def is_empty(self):
        return len(self._items) == 0

    def size(self):
        return len(self._items)

    def get_items(self):
        return self._items   # a plain method — lets us peek at everything for display purposes


s = Stack()
s.push(10)
s.push(20)
s.push(30)
print(s.get_items())  # [10, 20, 30]
print(s.pop())          # 30
print(s.peek())         # 20
print(s.size())         # 2
```

**Note:** No `__str__` here — that's a special method tied to *operator overloading* and *method overriding*, topics that come later in the curriculum. Until then, `get_items()` is just a regular method (like `pop()` or `peek()`) that returns the internal list so it can be printed directly with `print()`.

### 2.4 Real-World Problem: Balanced Parentheses Checker

A very common real problem — validating that brackets in code or an expression are properly matched (used by compilers, JSON/XML parsers, IDEs highlighting bracket errors).

```python
class Stack:
    def __init__(self):
        self._items = []

    def push(self, item):
        self._items.append(item)

    def pop(self):
        return self._items.pop()

    def peek(self):
        return self._items[-1] if self._items else None

    def is_empty(self):
        return len(self._items) == 0


def is_balanced(expression):
    stack = Stack()
    pairs = {')': '(', ']': '[', '}': '{'}

    for char in expression:
        if char in "([{":
            stack.push(char)
        elif char in ")]}":
            if stack.is_empty() or stack.pop() != pairs[char]:
                return False

    return stack.is_empty()


print(is_balanced("{[a + (b * c)] - d}"))  # True
print(is_balanced("[(a + b)]"))            # True
print(is_balanced("[(a + b])"))            # False — mismatched
print(is_balanced("((a + b)"))             # False — unclosed
```

### 2.5 Real-World Problem: Expression Evaluation (Postfix)

Compilers and calculators convert expressions to **postfix (Reverse Polish Notation)** specifically because it can be evaluated cleanly with a stack — no need to worry about operator precedence or parentheses.

**Example:** `3 4 + 2 *` means `(3 + 4) * 2 = 14`

```python
class Stack:
    def __init__(self):
        self._items = []

    def push(self, item):
        self._items.append(item)

    def pop(self):
        return self._items.pop()

    def is_empty(self):
        return len(self._items) == 0


def evaluate_postfix(expression):
    stack = Stack()
    operators = {'+', '-', '*', '/'}

    for token in expression.split():
        if token not in operators:
            stack.push(float(token))
        else:
            b = stack.pop()
            a = stack.pop()
            if token == '+':
                stack.push(a + b)
            elif token == '-':
                stack.push(a - b)
            elif token == '*':
                stack.push(a * b)
            elif token == '/':
                stack.push(a / b)

    return stack.pop()


print(evaluate_postfix("3 4 + 2 *"))       # 14.0
print(evaluate_postfix("5 1 2 + 4 * + 3 -"))  # 14.0
```

**How it works, step by step for `3 4 + 2 *`:**

| Token | Action | Stack after |
|---|---|---|
| `3` | push | `[3]` |
| `4` | push | `[3, 4]` |
| `+` | pop 4, pop 3, push 3+4 | `[7]` |
| `2` | push | `[7, 2]` |
| `*` | pop 2, pop 7, push 7*2 | `[14]` |

Final result: `14` — the stack naturally holds "pending operands" until an operator consumes them.

### 2.6 Real-World Problem: Infix to Postfix Conversion

This is how a real interpreter/compiler would actually convert human-readable expressions (`3 + 4 * 2`) into postfix before evaluating them — using **two stacks conceptually** (one for output, one for operators).

```python
class Stack:
    def __init__(self):
        self._items = []

    def push(self, item):
        self._items.append(item)

    def pop(self):
        return self._items.pop()

    def peek(self):
        return self._items[-1] if self._items else None

    def is_empty(self):
        return len(self._items) == 0


def infix_to_postfix(expression):
    precedence = {'+': 1, '-': 1, '*': 2, '/': 2}
    op_stack = Stack()
    output = []

    for token in expression.split():
        if token.isnumeric():
            output.append(token)
        elif token == '(':
            op_stack.push(token)
        elif token == ')':
            while op_stack.peek() != '(':
                output.append(op_stack.pop())
            op_stack.pop()  # discard the '('
        else:  # operator
            while (not op_stack.is_empty() and op_stack.peek() != '(' and
                   precedence.get(op_stack.peek(), 0) >= precedence[token]):
                output.append(op_stack.pop())
            op_stack.push(token)

    while not op_stack.is_empty():
        output.append(op_stack.pop())

    return ' '.join(output)


print(infix_to_postfix("3 + 4 * 2"))        # 3 4 2 * +
print(infix_to_postfix("( 3 + 4 ) * 2"))    # 3 4 + 2 *
```

### 2.7 Real-World Problem: Evaluating a Real Expression — `((2+3)*5/5)`

This is the problem from the top of the guide. Instead of converting to postfix first, this version evaluates a real infix expression — parentheses, precedence, and all — directly, using **two stacks working together**: one holding numbers (`values`), one holding operators and `(` (`operators`). No `eval()` involved.

```python
class Stack:
    def __init__(self):
        self._items = []

    def push(self, item):
        self._items.append(item)

    def pop(self):
        return self._items.pop()

    def peek(self):
        return self._items[-1] if self._items else None

    def is_empty(self):
        return len(self._items) == 0


def apply_operator(a, b, op):
    if op == '+':
        return a + b
    elif op == '-':
        return a - b
    elif op == '*':
        return a * b
    elif op == '/':
        return a / b


def evaluate_expression(expression):
    values = Stack()      # holds numbers
    operators = Stack()   # holds operators and '('
    precedence = {'+': 1, '-': 1, '*': 2, '/': 2}

    i = 0
    while i < len(expression):
        char = expression[i]

        if char == ' ':
            i += 1
            continue

        if char.isdigit():
            num = ''
            while i < len(expression) and expression[i].isdigit():
                num += expression[i]
                i += 1
            values.push(float(num))
            continue  # already advanced i past the number

        elif char == '(':
            operators.push(char)

        elif char == ')':
            while operators.peek() != '(':
                b = values.pop()
                a = values.pop()
                op = operators.pop()
                values.push(apply_operator(a, b, op))
            operators.pop()  # discard the matching '('

        elif char in '+-*/':
            while (not operators.is_empty() and operators.peek() != '(' and
                   precedence.get(operators.peek(), 0) >= precedence[char]):
                b = values.pop()
                a = values.pop()
                op = operators.pop()
                values.push(apply_operator(a, b, op))
            operators.push(char)

        i += 1

    while not operators.is_empty():
        b = values.pop()
        a = values.pop()
        op = operators.pop()
        values.push(apply_operator(a, b, op))

    return values.pop()


print(evaluate_expression("((2+3)*5/5)"))   # 5.0
```

**Walking through `((2+3)*5/5)`:**

| Step | What happens | `values` stack | `operators` stack |
|---|---|---|---|
| `(` `(` | both pushed | `[]` | `['(', '(']` |
| `2`, `+`, `3` | `2` pushed, `+` pushed, `3` pushed | `[2, 3]` | `['(', '(', '+']` |
| `)` | pops until `(`: computes `2+3=5` | `[5]` | `['(']` |
| `*` | pushed (no higher-precedence op waiting) | `[5]` | `['(', '*']` |
| `5` | pushed | `[5, 5]` | `['(', '*']` |
| `/` | same precedence as `*`, so `*` resolves first: `5*5=25` | `[25]` | `['(', '/']` |
| `5` | pushed | `[25, 5]` | `['(', '/']` |
| `)` | pops until `(`: computes `25/5=5.0` | `[5.0]` | `[]` |

Final result: **`5.0`** — matches `((2+3)*5/5)` evaluated by hand.

---

## 3. Queue

### 3.1 What Is a Queue?

A **Queue** is a **FIFO** (First In, First Out) structure. The first item added is the first one removed — like people standing in a line: whoever joined first gets served first.

**Core operations:**
- `enqueue(item)` — add an item to the back
- `dequeue()` — remove and return the item at the front
- `peek()` / `front()` — look at the front item without removing it
- `is_empty()` — check if the queue has anything in it

### 3.2 Why Queues Are Used

- **Task scheduling** — print jobs, CPU process scheduling
- **Handling requests in order** — web servers processing incoming requests, customer support ticket systems
- **Breadth-first search (BFS)** — level-by-level traversal of trees and graphs
- **Buffering / streaming data** — keeping data in the order it arrived (video buffering, message queues like RabbitMQ/Kafka)
- **Real-world simulations** — ticket counters, call centers, traffic systems

### 3.3 Class-Based Implementation

This one is built the same way as Stack — a plain Python list, no imports. (In production code you'd reach for `collections.deque`, since `list.pop(0)` is O(n) — it has to shift every remaining element down by one. That's a separate topic; a plain list keeps the focus on *how a queue behaves*, not on performance tuning.)

```python
class Queue:
    def __init__(self):
        self._items = []   # protected — plain list, front is index 0

    def enqueue(self, item):
        self._items.append(item)          # add to the back

    def dequeue(self):
        if self.is_empty():
            raise IndexError("dequeue from an empty queue")
        return self._items.pop(0)          # remove from the front

    def peek(self):
        if self.is_empty():
            raise IndexError("peek from an empty queue")
        return self._items[0]

    def is_empty(self):
        return len(self._items) == 0

    def size(self):
        return len(self._items)

    def get_items(self):
        return self._items   # a plain method — lets us peek at everything for display purposes


q = Queue()
q.enqueue("Customer 1")
q.enqueue("Customer 2")
q.enqueue("Customer 3")
print(q.get_items())  # ['Customer 1', 'Customer 2', 'Customer 3']
print(q.dequeue())      # Customer 1 — first one in, first one out
print(q.peek())          # Customer 2
```

### 3.4 Real-World Problem: Ticket Counter / Customer Service Simulation

A direct real-world mapping — simulating people being served in the order they arrived, tracking wait times.

```python
class TicketQueue:
    def __init__(self):
        self._items = []

    def enqueue(self, name):
        self._items.append(name)
        print(f"{name} joined the queue.")

    def dequeue(self):
        if self.is_empty():
            print("No customers waiting.")
            return None
        served = self._items.pop(0)
        print(f"Serving {served}.")
        return served

    def is_empty(self):
        return len(self._items) == 0

    def people_waiting(self):
        return len(self._items)


counter = TicketQueue()
counter.enqueue("Priya")
counter.enqueue("Rahul")
counter.enqueue("Sana")

print(f"People waiting: {counter.people_waiting()}")  # 3

counter.dequeue()  # Serving Priya
counter.dequeue()  # Serving Rahul

print(f"People waiting: {counter.people_waiting()}")  # 1
```

### 3.5 Real-World Problem: BFS Traversal (Task/Level Processing)

Queues are the backbone of **breadth-first search** — used for things like finding the shortest path in a network, level-order processing of an org chart, or finding friends-of-friends in a social graph.

```python
class Queue:
    def __init__(self):
        self._items = []

    def enqueue(self, item):
        self._items.append(item)

    def dequeue(self):
        return self._items.pop(0)

    def is_empty(self):
        return len(self._items) == 0


def bfs(graph, start):
    visited = {start}
    order = []
    queue = Queue()
    queue.enqueue(start)

    while not queue.is_empty():
        node = queue.dequeue()
        order.append(node)

        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.enqueue(neighbor)

    return order


# Example: a small social network graph
social_graph = {
    "Alex":  ["Priya", "Rahul"],
    "Priya": ["Alex", "Sana"],
    "Rahul": ["Alex", "Meera"],
    "Sana":  ["Priya"],
    "Meera": ["Rahul"],
}

print(bfs(social_graph, "Alex"))
# ['Alex', 'Priya', 'Rahul', 'Sana', 'Meera'] — closest connections found first
```

---

## 4. Stack vs Queue — Quick Comparison

| Aspect | Stack | Queue |
|---|---|---|
| Order | LIFO (Last In, First Out) | FIFO (First In, First Out) |
| Add operation | `push()` — adds to top | `enqueue()` — adds to back |
| Remove operation | `pop()` — removes from top | `dequeue()` — removes from front |
| Real-world analogy | Stack of plates | Line at a ticket counter |
| Common use cases | Undo/redo, call stack, DFS, expression evaluation | Task scheduling, BFS, request handling, buffering |
| Backing structure (in this guide) | Python `list` | Python `list` |
| Production backing structure | Python `list` | `collections.deque` (O(1) at both ends — not covered here) |

---

## 5. Why Building These With Classes (Not Just Raw Lists) Matters in Practice

If you just used a raw Python list everywhere and called `.append()` / `.pop(0)` directly, nothing would stop someone from doing `my_stack.pop(2)` — removing from the middle, which breaks the entire LIFO guarantee. Wrapping it in a class:

1. **Enforces correctness** — only the operations that make sense for that structure are exposed.
2. **Makes the intent obvious in code** — `order_queue.dequeue()` reads far better than `orders.pop(0)`, especially in a large codebase.
3. **Swaps implementation without breaking callers** — if you switch the internal storage from a `list` to a `deque` (as shown above, for performance), every place using `Queue()` keeps working unchanged.
4. **Prepares you for real systems** — production task queues, undo systems, and parsers are all built exactly this way: a class wrapping a raw structure with controlled access.

---

## 6. Try These — Real Problems to Solve With Stack or Queue

Now that the mechanics are clear, here are problems worth attempting with the `Stack` and `Queue` classes built above. Try coding a solution before checking any reference.

**Using Stack:**
1. **Reverse a string** — push every character, then pop them all off to build the reversed string.
2. **Text editor undo history** — push every edit made; "undo" pops the last edit and reverts it.
3. **Browser "back" button** — push every visited URL; "back" pops the most recent one.
4. **Next Greater Element** — for each number in a list, find the next number to its right that's larger, using a stack to track numbers still "waiting" for a bigger neighbor.

**Using Queue:**
1. **Print job scheduler** — jobs sent to a printer should print in the order they were submitted.
2. **Customer support ticket system** — tickets get resolved in the order they were raised.
3. **Level-order tree traversal** — print a tree's nodes level by level, top to bottom, left to right.
4. **Round-robin CPU scheduling** — each process gets a fixed time slice, then goes to the back of the queue if it isn't finished.

Pick one and code it with the `Stack` or `Queue` class from this guide before looking anything else up — that's where it actually sticks.
