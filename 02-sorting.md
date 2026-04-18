# 2️⃣ Sorting Algorithms

---

## ✅ Sort Strings (By Length)

### Purpose
Sort by:
1. Length
2. Alphabetical
3. Original position

### Code

```python
def sort_strings1(lst):
    s = sorted(enumerate(lst), key=lambda x: (len(x[1]), x[1].lower(), x[0]))
    return [i for _, i in s]
```

### Example

```python
print(sort_strings1(["banana", "apple", "cat", "an"]))
```

Output:

```
["an", "cat", "apple", "banana"]
```

---

## ✅ Sort Strings (With Vowel Count)

```python
def sort_strings(lst):
    vowels = "aeiou"

    def count_vowels(s):
        return sum(1 for char in s if char.lower() in vowels)

    lst.sort(key=lambda s: (len(s), s.lower(), count_vowels(s)))
    return lst
```
