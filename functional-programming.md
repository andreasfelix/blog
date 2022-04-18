# functional programming

## Examples

Check there is at least one uppercase, lowercase, and one digit charactar in password:

```python
def is_valid(password):
    has_upper = False
    has_lower = False
    has_digit = False

    for char in password:
        has_upper |= char.isupper():
        has_lower |= char.islower():
        has_digit |= char.isdigit():
    return has_upper and has_lower and has_digit
```

```python
is_valid = lambda password: all(
    any(map(func, password)) 
    for func in [str.isupper, str.islower, str.isdigit]
)
```

```elm
isValid password = 
    [ Char.isUpper, Char.isLower, Char.isDigit ]
        |> List.all (\func -> String.any func password)
```

