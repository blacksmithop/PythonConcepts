We can all agree that coroutines are great and much easier to understand than threading. Now this might be because the `asyncio` library abstract much of the inner working making the end-user not worry as much about what goes in the background.

For this example we are going to treat the functions as a black box

We start off by creating a coroutine

```python
import asyncio

async def coro(num):
	print(">", num)
	await asyncio.sleep(1)
	print("<", num)

	return num****
```

Now we create a `loop`

```python
loop = asyncio.get_event_loop()
```

Think of it as an environment to execute coroutines in a single thread

Next, we will use `gather`

```python
group = asyncio.gather(coro(1), coro(2))****
```

`gather` simply runs the awaitable objects / coroutines *concurrently*

> Note that `gather` does not accept a list, so remember to unpack it `*list_of_coroutines`

Now we run the `loop`

```python
results = loop.run_until_complete(group)
loop.close()
  
print(results)
```

```json
1
2
1
2
[1, 2]
```

