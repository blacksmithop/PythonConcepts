If I wanted to print `Hello World!` in python, you'd do something like this

```python
print("Hello World!")
```

## What if you wanted to do it in Cython instead?

The reason why Cython is preferred over native Python lies in the fact many libraries are written in C and depending on the task at hand speedup obtained can be massive.

We start off by creating a file with a `.pyx` extension

```python
#helloworld.pyx
print("Hello World")
```

Now we create a `setup.py`

```python
from setuptools import setup
from Cython.Build import cythonize

setup(
    ext_modules = cythonize("helloworld.pyx")
)
```

We can build this by running

```sh
python setup.py build_ext --inplace
```

You will notice that this created a bunch of files and a directory where you ran the command, pay attention to the file ending with `.pyd`

You're able this file as it were a python module

```python
>>> import helloworld
Hello World
```
