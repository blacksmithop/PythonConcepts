When we talk about concurrency in Python we're often looking for a way to execute programs/tasks simultaneously. 

The catch here is that `asyncio` and `threading` run on a single processor and therefore only run one task at a time! In effect, they're taking turns to speed up the overall process, true concurrency was never achieved.

This is where `multiprocessing` comes in.

Before we get our hands dirty lets go over what the other two libraries do

### Threading

In `threading` the OS is aware of each thread and hence can interrupt one to run the other. This is called `pre-emptive multitasking`. This naturally presents problems of it own as operation of a thread can be interrupted *anytime*.

### Asyncio

`asyncio` on the other hand uses `cooperative multitasking` and hence the tasks must cooperate and annouce when they're ready to be switched out. This must be defined in the code.

> The tradeoff is that we can control *where* the task will be switched.

### Parallelism

With `multiprocessing`, python creates a new process for each task. Since they're seperate they can be run on a different core, hence *concurrency*. Voila!

