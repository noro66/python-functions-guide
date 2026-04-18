# 8️⃣ Common Bugs & Fixes

---

## ✅ Bugs Found in This Guide

| Bug | Where | Problem | Fix |
|-----|-------|---------|-----|
| `and` vs `or` | `convert_base` | `x < 2 and x > 36` is impossible | Change to `or` |
| Indentation | `shift_list` | `for` loop not aligned | Fix spacing |
| Variable name | `shift_list` | Used `list` which shadows built-in | Rename to `lst` |
| Semicolon | `shift_list` | `return list;` unnecessary | Remove `;` |
| Typo | `marge_list` | Wrong spelling | Fix to `merge_list` |

---

## ✅ Common Python Mistakes

### ❌ Using Built-in Names as Variables

```python
# BAD ❌
list = [1, 2, 3]
str = "hello"
dict = {"a": 1}
```

```python
# GOOD ✅
my_list = [1, 2, 3]
my_str = "hello"
my_dict = {"a": 1}
```

---

### ❌ Confusing `and` with `or` in Validation

```python
# BAD ❌ — This condition is IMPOSSIBLE
# Nothing can be both less than 2 AND greater than 36
if x < 2 and x > 36:
    return "ERROR"
```

```python
# GOOD ✅ — Catches EITHER case
if x < 2 or x > 36:
    return "ERROR"
```

---

### ❌ Modifying a List While Iterating

```python
# BAD ❌ — Skips items silently
for item in my_list:
    my_list.remove(item)
```

```python
# GOOD ✅ — Create a new list instead
new_list = [item for item in my_list if item != target]
```

---

### ❌ Forgetting to Handle Edge Cases

```python
# BAD ❌ — Crashes on empty list
def second_largest(nums):
    unique = list(set(nums))
    unique.sort()
    return unique[-2]   # IndexError if less than 2 items!
```

```python
# GOOD ✅ — Check first
def second_largest(nums):
    unique = list(set(nums))
    unique.sort()
    if len(unique) < 2:
        return None
    return unique[-2]
```

---

## ✅ General Tips

> 💡 Don't name variables after built-in functions.

> 💡 Always handle edge cases: empty lists, empty strings, single elements.

> 💡 Use `or` when checking boundary conditions, not `and`.

> 💡 Never modify a list while looping over it.
