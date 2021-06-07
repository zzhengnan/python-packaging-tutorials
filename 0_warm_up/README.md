What happens when you run this command?
```
$ python setup.py sdist
```

Two additional directories get created.
- `dist` contains a compressed tarball of the source distribution
- [Note to self: Find out more about `egg-info`]
```
├── alpha_pkg.egg-info
│   ├── PKG-INFO
│   ├── SOURCES.txt
│   ├── dependency_links.txt
│   └── top_level.txt
├── dist
│   └── alpha-pkg-0.0.0.tar.gz
```

Now try installing this package into your environment.
```
$ pip install dist/alpha-pkg-0.0.0.tar.gz
```

To test that the package has been correctly installed, first `cd` out of this repo -- this is important because otherwise python will just import what's in your working directory, which isn't what we want in this case. Then fire up the python REPL and try importing the package.
```
$ cd ~
$ python
```

```python
>>> import alpha
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'alpha'
```

Hmmm... Let's ask conda. Unless you are using an ancient version of conda, `conda list` will detect packages installed via either conda or pip.
```
$ conda list alpha
# packages in environment at /Users/bjw336/opt/miniconda3/envs/pkg-tut:
#
# Name                    Version                   Build  Channel
alpha-pkg                 0.0.0                    pypi_0    pypi
```

Clearly conda can detect this package in our environment. Maybe try `alpha-pkg`? After all, that's what we put inside `setup.py`.
```python
>>> import alpha-pkg
  File "<stdin>", line 1
    import alpha-pkg
                ^
SyntaxError: invalid syntax
```

What?!

By this point, two questions come to mind.
1. What's the canonical name of the package? Is it `alpha` or `alpha-pkg`?
1. Why are we not able to import the package, even though it clearly is detected in the environment?

Go to the next tutorial to find out. Before you do that though, uninstall the package so that you'll have a clean environment to work with.
```
$ pip uninstall alpha-pkg
```
