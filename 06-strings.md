# 6️⃣ String Algorithms

---

## ✅ Shift String (Caesar Cipher)

### Purpose
Shifts each letter by a number of positions in the alphabet.
This is the Caesar Cipher — one of the oldest encryption methods.

### Visual — Alphabet Shift by 3

```
Original:  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
Shifted:   D E F G H I J K L M N O P Q R S T U V W X Y Z A B C
                                                           ↑ wraps!
```

### The Magic Formula

```
chr((ord(char) - start + number) % 26 + start)
```

Breaking it down with `char = 'X'`, `number = 3`:

```
Step 1: ord('X')    = 88    ← letter to number
Step 2: 88 - 65     = 23    ← position in alphabet (0-25)
Step 3: 23 + 3      = 26    ← shift forward
Step 4: 26 % 26     = 0     ← wrap around! (past Z → back to A)
Step 5: 0 + 65      = 65    ← back to ASCII range
Step 6: chr(65)     = 'A'   ← number back to letter

Result: 'X' shifted by 3 → 'A' ✅
```

### ASCII Quick Reference

| Character | ASCII Number |
|-----------|-------------|
| `'A'` | 65 |
| `'Z'` | 90 |
| `'a'` | 97 |
| `'z'` | 122 |

### Code

```python
def shift_string(s, number):
    result = ""

    for char in s:
        if char.isalpha():
            if char.islower():
                start = ord('a')
            else:
                start = ord('A')
            new_char = chr((ord(char) - start + number) % 26 + start)
            result += new_char
        else:
            result += char
    return result
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `char.isalpha()` | Is it a letter? |
| `char.islower()` | Is it lowercase? |
| `ord('a')` / `ord('A')` | Starting ASCII value |
| `ord(char) - start` | Position in alphabet (0-25) |
| `+ number` | Shift forward |
| `% 26` | Wrap around the alphabet |
| `+ start` | Convert back to ASCII range |
| `chr(...)` | ASCII number → character |
| `else: result += char` | Non-letters stay unchanged |

### Examples

```python
print(shift_string("Xyz", 3))           # "Abc"
print(shift_string("Hello", 1))         # "Ifmmp"
print(shift_string("abc", 26))          # "abc"  (full rotation)
print(shift_string("Hello World!", 5))  # "Mjqqt Btwqi!"
```

---

## ✅ Upper Lower (Alternating Case)

### Purpose
Alternates between UPPERCASE and lowercase based on position.

```
Even positions → UPPERCASE
Odd positions  → lowercase
```

### Visual Walkthrough — "hello world"

| Char | Position | Even/Odd | Result |
|------|----------|----------|--------|
| `h` | 0 | EVEN | `H` |
| `e` | 1 | ODD | `e` |
| `l` | 2 | EVEN | `L` |
| `l` | 3 | ODD | `l` |
| `o` | 4 | EVEN | `O` |
| ` ` | 5 | — | ` ` |
| `w` | 6 | EVEN | `W` |
| `o` | 7 | ODD | `o` |
| `r` | 8 | EVEN | `R` |
| `l` | 9 | ODD | `l` |
| `d` | 10 | EVEN | `D` |

Final result: `"HeLlO WoRlD"`

### Code

```python
def upper_lower(str_1: str) -> str:
    result = ""
    number = 0

    for char in str_1:
        if char.isalpha():
            if number % 2 == 0:
                char = char
            else:
                char = char
            result += char
        else:
            result += char
        number += 1
    return result
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `number = 0` | Counter tracking position |
| `char.isalpha()` | Is it a letter? |
| `number % 2 == 0` | Is position even? |
| `.upper()` | Even positions → UPPERCASE |
| `.lower()` | Odd positions → lowercase |
| `number += 1` | Increment counter for ALL characters |

> ⚠️ Note: Counter increases for ALL characters including spaces.
> Move `number += 1` inside `if char.isalpha()` to count only letters.

### Examples

```python
print(upper_lower("hello world"))   # "HeLlO WoRlD"
print(upper_lower("python"))        # "PyThOn"
print(upper_lower("123abc"))        # "123AbC"
```

---

## ✅ Is Palindrome

### Purpose
Checks if a string reads the same forwards and backwards.

### Visual — Mirror Analogy 🪞

```
"racecar" → reverse → "racecar"  → SAME      → True  ✅
"hello"   → reverse → "olleh"    → DIFFERENT  → False ❌
```

### Code

```python
def is_palindrome(s):
    s = s.lower().replace(" ", "")
    return s == s[::-1]
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `.lower()` | Makes everything lowercase |
| `.replace(" ", "")` | Removes all spaces |
| `s[::-1]` | Reverses the string |
| `s == s[::-1]` | Compares original with reversed |

### Examples

```python
print(is_palindrome("Racecar"))                       # True
print(is_palindrome("hello"))                         # False
print(is_palindrome("A man a plan a canal Panama"))   # True
```

---

## ✅ Are Anagrams

### Purpose
Checks if two strings contain the exact same letters in any order.

### Visual — Scrabble Tiles 🎲

```
"listen" → sort → ['e','i','l','n','s','t']
"silent" → sort → ['e','i','l','n','s','t']

Same? → True ✅
```

### Code

```python
def are_anagrams(s1, s2):
    s1 = s1.replace(" ", "")
    s2 = s2.replace(" ", "")

    if len(s1) != len(s2):
        return False

    return sorted(s1) == sorted(s2)
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `.replace(" ", "").lower()` | Clean: remove spaces, lowercase |
| `len(s1) != len(s2)` | Different lengths → not anagrams |
| `sorted(s1) == sorted(s2)` | Sort both and compare |

### Examples

```python
print(are_anagrams("listen", "silent"))         # True
print(are_anagrams("hello", "world"))           # False
print(are_anagrams("Dormitory", "Dirty room"))  # True
```

---

## ✅ Compress String (Run-Length Encoding)

### Purpose
Compresses a string by counting consecutive repeated characters.

```
"aaabbc" → "a3b2c1"
```

### Visual Walkthrough — "aaabbc"

| Index | Current | Previous | Same? | Count | Result |
|-------|---------|----------|-------|-------|--------|
| 1 | `a` | `a` | YES | 2 | `""` |
| 2 | `a` | `a` | YES | 3 | `""` |
| 3 | `b` | `a` | NO | 1 | `"a3"` |
| 4 | `b` | `b` | YES | 2 | `"a3"` |
| 5 | `c` | `b` | NO | 1 | `"a3b2"` |

After loop → add last streak → `"a3b2c1"` ✅

### Code

```python
def compress_string(s):
    if not s:
        return ""

    result = ""
    count = 1

    for i in range(1, len(s)):
        if s[i] == s[i - 1]:
            count += 1
        else:
            result += s[i - 1] + str(count)
            count = 1

    result += s[-1] + str(count)
    return result
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `if not s` | Empty string → return `""` |
| `count = 1` | Start counting at 1 |
| `range(1, len(s))` | Start at index 1 |
| `s[i] == s[i-1]` | Same as previous? |
| `count += 1` | Yes → increase streak |
| `result += s[i-1] + str(count)` | No → save streak, reset |
| `result += s[-1] + str(count)` | Save the LAST streak |

### Examples

```python
print(compress_string("aaabbc"))      # "a3b2c1"
print(compress_string("aaa"))         # "a3"
print(compress_string("abcd"))        # "a1b1c1d1"
print(compress_string(""))            # ""
print(compress_string("aabbbcccc"))   # "a2b3c4"
```

---

## ✅ Pattern Tracker

### Purpose
Counts how many times two consecutive characters are digits that increase by exactly 1.

```
"a123b47" → pairs: (1,2), (2,3), (4,7)
Only (1,2) and (2,3) match → result = 2
```

### Code

```python
def pattern_tracker(s: str):
    count = 0
    for i in range(len(s) - 1):
        if s[i].isdigit() and s[i + 1].isdigit():
            if int(s[i]) + 1 == int(s[i + 1]):
                count += 1
    return count
```

### How It Works Line by Line

| Line | What It Does |
|------|-------------|
| `count = 0` | Starts the match counter |
| `range(len(s) - 1)` | Loops through each index with a next character available |
| `s[i].isdigit() and s[i + 1].isdigit()` | Checks that both characters are digits |
| `int(s[i]) + 1 == int(s[i + 1])` | Verifies the second digit is exactly one greater |
| `count += 1` | Adds one valid pattern match |
| `return count` | Returns total matches |

### Examples

```python
print(pattern_tracker("a123b47"))   # 2
print(pattern_tracker("x4567"))     # 3
print(pattern_tracker("98"))        # 0
print(pattern_tracker("ab12cd34"))  # 2
```
