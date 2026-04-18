# 7️⃣ Classic Algorithms

---

## ✅ Valid Parentheses

### Purpose
Checks if all brackets are properly opened and closed
in the correct order.

### The Stack Concept — Plate Analogy 📚

```
Think of a stack of plates:

→ You can only ADD a plate on TOP      ( append() )
→ You can only REMOVE from the TOP     ( pop()    )

Opening bracket? → Push onto stack
Closing bracket? → Check if top matches
                   YES → Pop it off
                   NO  → INVALID ❌
End of string?   → Stack must be EMPTY
```

### Visual Walkthrough — `"([{}])"`

| Char | Action | Stack |
|------|--------|-------|
| `(` | Opening → push | `['(']` |
| `[` | Opening → push | `['(', '[']` |
| `{` | Opening → push | `['(', '[', '{']` |
| `}` | Matches `{` → pop | `['(', '[']` ✓ |
| `]` | Matches `[` → pop | `['(']` ✓ |
| `)` | Matches `(` → pop | `[]` ✓ |

Stack is empty → `True` ✅

### Visual Walkthrough — `"([)]"` (INVALID)

| Char | Action | Stack |
|------|--------|-------|
| `(` | Opening → push | `['(']` |
| `[` | Opening → push | `['(', '[']` |
| `)` | Needs `(` but top is `[` | ❌ |

→ `False`

### Code

```python
def valid_parentheses(s):
    stack = []
    pairs = {')': '(', ']': '[', '}': '{'}

    for char in s:
        if char in '([{':
            stack.append(char)
        elif char in ')]}':
            if not stack:
                return False
            if stack[-1] != pairs[char]:
                return False
            stack.pop()

    return len(stack) == 0
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `stack = []` | Empty list used as a stack |
| `pairs = {')':'(',...}` | Maps closing → opening brackets |
| `char in '(['` | Is it an opening bracket? |
| `stack.append(char)` | Push onto stack |
| `if not stack` | Stack empty? Nothing to match → False |
| `stack[-1] != pairs[char]` | Top doesn't match → False |
| `stack.pop()` | Match found → remove top |
| `len(stack) == 0` | All brackets matched? |

### Examples

```python
print(valid_parentheses("()"))             # True
print(valid_parentheses("([{}])"))         # True
print(valid_parentheses("(]"))             # False
print(valid_parentheses("((())"))          # False (unclosed)
print(valid_parentheses(""))               # True  (empty is valid)
print(valid_parentheses("hello(world)"))   # True  (ignores non-brackets)
```

---

## ✅ All Chars from S1 in S2

### Purpose
Checks if every character in `s1` exists somewhere in `s2`.

### Visual — Shopping List Analogy 🛒

```
s1 = "abc"     ← Shopping list  (what I NEED)
s2 = "abcdef"  ← Store shelves  (what's AVAILABLE)

Check 'a' → in store? ✅
Check 'b' → in store? ✅
Check 'c' → in store? ✅
All found → True ✅

─────────────────────────────

s1 = "abc"
s2 = "ab"

Check 'a' → in store? ✅
Check 'b' → in store? ✅
Check 'c' → in store? ❌ → False immediately!
```

### Code

```python
def all_chars_in(s1, s2):
    for char in s1:
        if char not in s2:
            return False
    return True
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `for char in s1` | Loop through every character in s1 |
| `if char not in s2` | Is this character missing from s2? |
| `return False` | Even ONE missing → immediately False |
| `return True` | Got through all → all found |

### Shorter Alternative

```python
def all_chars_in(s1, s2):
    return all(char in s2 for char in s1)
```

### Examples

```python
print(all_chars_in("abc", "abcdef"))     # True
print(all_chars_in("abc", "ab"))         # False (missing 'c')
print(all_chars_in("hello", "helo"))     # True  (duplicates ok)
print(all_chars_in("", "anything"))      # True  (nothing to check)
print(all_chars_in("ABC", "abc"))        # False (case sensitive!)
```
