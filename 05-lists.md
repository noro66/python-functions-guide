# 5️⃣ List Operations

---

## ✅ Shift List (Rotate Right)

### Purpose
Takes items from the END and puts them at the FRONT.

### Visual

```
Start:    [1, 2, 3, 4, 5]

Round 1:  pop 5 → insert front → [5, 1, 2, 3, 4]
Round 2:  pop 4 → insert front → [4, 5, 1, 2, 3] ✅
```

### Code

```python
def shift_list(lst, num):
    if not lst:
        return lst

    for i in range(num):
        nb = lst.pop()
        lst.insert(0, nb)

    return lst
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `if not lst` | If list is empty → return immediately |
| `for i in range(num)` | Repeat the shift `num` times |
| `lst.pop()` | Remove and return the LAST item |
| `lst.insert(0, nb)` | Put that item at the BEGINNING |

### Examples

```python
print(shift_list([1, 2, 3, 4, 5], 2))  # [4, 5, 1, 2, 3]
print(shift_list([1, 2, 3], 1))         # [3, 1, 2]
print(shift_list([], 3))                # []
print(shift_list([1], 5))               # [1]
```

---

## ✅ Merge Lists

### Purpose
Combines two lists and sorts the result.

### Visual

```
list1 = [3, 1]
list2 = [4, 2]

Step 1 — merge:  [3, 1, 4, 2]
Step 2 — sort:   [1, 2, 3, 4]
```

### Code

```python
def merge_list(list1, list2):
    list1 += list2
    return sorted(list1)
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `list1 += list2` | Adds all items from list2 to end of list1 |
| `sorted(list1)` | Returns a new sorted list ascending |

### Examples

```python
print(merge_list([1, 2, 3], [3, 2, 1]))  # [1, 1, 2, 2, 3, 3]
print(merge_list([], [5, 3]))             # [3, 5]
print(merge_list([10], [1]))              # [1, 10]
```

---

## ✅ Remove Duplicates

### Purpose
Removes duplicate items while keeping the original order.

### Visual — Bouncer Analogy 🚪

```
Guest list: [1, 2, 2, 3, 1, 4]

1 arrives → not seen → LET IN    → seen: [1]
2 arrives → not seen → LET IN    → seen: [1, 2]
2 arrives → SEEN     → REJECT    → seen: [1, 2]
3 arrives → not seen → LET IN    → seen: [1, 2, 3]
1 arrives → SEEN     → REJECT    → seen: [1, 2, 3]
4 arrives → not seen → LET IN    → seen: [1, 2, 3, 4]
```

### Code

```python
def remove_duplicates(lst):
    seen = []
    for item in lst:
        if item not in seen:
            seen.append(item)
    return seen
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `seen = []` | Empty list to store items already seen |
| `for item in lst` | Loop through each element |
| `if item not in seen` | Have I seen this before? |
| `seen.append(item)` | No → add it |
| `return seen` | Return cleaned list |

### Examples

```python
print(remove_duplicates([1, 2, 2, 3, 1, 4]))      # [1, 2, 3, 4]
print(remove_duplicates(['a', 'b', 'a', 'c']))     # ['a', 'b', 'c']
print(remove_duplicates([]))                        # []
```

---

## ✅ Flatten List

### Purpose
Converts a list of lists into a single flat list.

### Visual — Unpacking Boxes 📦

```
Input:  [[1, 2], [3, 4], [5]]

Box 1: [1, 2] → take out 1, take out 2
Box 2: [3, 4] → take out 3, take out 4
Box 3: [5]    → take out 5

Result: [1, 2, 3, 4, 5]
```

### Code

```python
def flatten_list(nested):
    flat = []
    for sublist in nested:
        for item in sublist:
            flat.append(item)
    return flat
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `flat = []` | Empty list for the final result |
| `for sublist in nested` | OUTER LOOP: grabs each sublist |
| `for item in sublist` | INNER LOOP: grabs each item inside |
| `flat.append(item)` | Adds each item to the flat list |
| `return flat` | Returns one single-level list |

### Examples

```python
print(flatten_list([[1, 2], [3, 4], [5]]))     # [1, 2, 3, 4, 5]
print(flatten_list([[], [1], [2, 3]]))          # [1, 2, 3]
print(flatten_list([[1], [2], [3]]))            # [1, 2, 3]
```

---

## ✅ Second Largest Number

### Purpose
Finds the second largest unique number in a list.

### Visual

```
Input: [5, 1, 9, 9, 3]

Step 1 — set():  {1, 3, 5, 9}   ← removes duplicate 9
Step 2 — list(): [1, 3, 5, 9]   ← convert back to list
Step 3 — sort(): [1, 3, 5, 9]   ← sort ascending
Step 4 — [-2]:   5              ← second from last

Index:  [-4] [-3] [-2] [-1]
Value:    1    3    5    9
                    ↑
              second largest!
```

### Code

```python
def second_largest(nums):
    unique = list(set(nums))
    unique.sort()
    if len(unique) < 2:
        return None
    return unique[-2]
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `set(nums)` | Removes duplicates |
| `list(set(nums))` | Converts set back to list |
| `unique.sort()` | Sorts ascending |
| `len(unique) < 2` | Less than 2 unique numbers? |
| `return None` | No second largest exists |
| `unique[-2]` | Second last = second largest |

### Examples

```python
print(second_largest([5, 1, 9, 9, 3]))   # 5
print(second_largest([4, 4, 4]))          # None
print(second_largest([1, 2]))             # 1
print(second_largest([10]))               # None
```

> ⚠️ Note: Returns `None` when there are fewer than 2 unique numbers.
