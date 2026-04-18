# 4️⃣ Number Systems

## ✅ Convert Base

```python
def convert_base(number, from_base, to_base):
    digits = "0123456789abcdefghijklmnopqrstuvwxyz"

    if to_base < 2 or to_base > 36 or from_base < 2 or from_base > 36:
        return "ERROR"

    try:
        decimal = int(number.lower(), from_base)
    except ValueError:
        return "ERROR"

    if decimal == 0:
        return "0"

    result = ""
    while decimal > 0:
        result += digits[(decimal % to_base)]
        decimal //= to_base

    return result[::-1].upper()
```
