If you have been using python for a while chances are you’ve stumbled upon `yield` before and guess what, it’s super useful.

```python
def iterate_stuff(n:int):  
  for i in range(n):  
    doComplexTask(i) #a complex task to be executed on demand
```

`yield` is great when you want to do computations on the fly without keeping each result in memory. This is achieved using `generators` which are basically iterators you can only iterate once.

This means I can create a generator and have it *yield* each result as I need them

```python
gen = iterate_stuff(n=5)  
next(gen)  
#...
```

In essence, it is like `return` except that it returns a `generator` instead.

---
### The magic of assignment

Now that we’ve agreed that `yield` is magic and that you should definitely be using it more often, let us see an interesting application of it.

```python
def f():  
  while True:  
    data= (yield)  
    print("data passed:", data)
```

It turns out that you can assign `yield` to a variable. Which lets you pass data to the generator.

Still with me? Don’t worry, let me explain

If we ignore the assignment or rather treat it like any other use of yield calling `f()` should return a `generator` . This is exactly what happens here.

```python
>>gen = f()  
>>type(g)  
<class 'generator'>
```

Now we can treat it as a black box to which we can send some data and have it return some output

```python
>>next(g) #you need to call it once so that yield gets evaluated  
>>gen.send("Hello World")  
data passed: Hello World  
>>gen.send(123)  
data passed: 123
```

`send` is basically a function that lets us send values to a function that just yielded.
