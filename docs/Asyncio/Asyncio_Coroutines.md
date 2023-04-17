Coroutines are great, but they have some whacky behavior

## 1. They can only be `await` ed once

Let's say you made a function

```python
def func():
    print("Hello World")
```

If you wanted to store a reference you'd simply do this

```python
func_ref = func

func_ref()
#Hello World
func_ref()
#Hello World
```

What if we tried this with a coroutines instead?

```python
async def coro():
	print("Hello World")
```

```python
import asyncio

coro_ref = coro
asyncio.run(coro_ref2())
#Hello World
asyncio.run(coro_ref2())
#Hello World
```

This works as intended, feel free to test them on your own

But what if you didn't want to pass a reference, but a function with predefined arguments instead?

With regular functions we can simply use `partial`  functions from `functools`

```python
from functools import partial
```

```python
def func(arg):
    return(arg)
```

Now we create a partial function
```python
partial_func = partial(func, "Hello World")
```

Now we can execute this function wherever we want by calling `partial_func`

```python
partial_func()
#Hello World
partial_func()
#Hello World
```

If I were to try the same thing with coroutines this will happen

```python
async def coro(arg):
    print(arg)

coro_ref = coro("Hello World")
```

```python
asyncio.run(coro_ref)
#Hello World
asyncio.run(coro_ref)
#RuntimeError: cannot reuse already awaited coroutine
```