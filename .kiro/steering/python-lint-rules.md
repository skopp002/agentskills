---
inclusion: fileMatch
fileMatchPattern: "**/*.{py,ipynb}"
---

# Python Lint Rules

When writing or editing Python files, always follow these rules:

## No f-strings without placeholders

Do not use f-strings that contain no `{}` interpolation expressions. Use regular strings instead.

Bad:
```python
print(f"Hello world")
print(f'No variables here')
```

Good:
```python
print("Hello world")
print('No variables here')
```

## No bare except clauses

Never use bare `except:`. Always specify an exception type.

- For general error handling: use `except Exception:`
- For JSON parsing: use `except (json.JSONDecodeError, ValueError):`
- For index/type errors: use `except (ValueError, IndexError):`
- For specific AWS errors: use the specific exception class (e.g., `except self.ssm.exceptions.ParameterNotFound:`)

Bad:
```python
try:
    do_something()
except:
    pass
```

Good:
```python
try:
    do_something()
except Exception:
    pass

try:
    data = json.loads(text)
except (json.JSONDecodeError, ValueError):
    data = None
```
