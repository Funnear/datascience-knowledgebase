
## Use logging instead of `print()` for developer-only output

```python
import logging
logging.getLogger().setLevel(logging.DEBUG)

# DEBUG - what developers look at
# INFO - extra information on what's happening
# WARNING - this won't stop your code from running but you're doing something slightly off
# EXCEPTION / ERROR - this will stop your code but you'll get extra info on the error

# usage
logging.info(f"The age ({age}) is between 24 and 34")

```

### Downgrade logging level to reduce output when building plots
```python
logging.getLogger().setLevel(logging.ERROR)

# code that builds plots

logging.getLogger().setLevel(logging.DEBUG)
```