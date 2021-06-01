Compared with the previous tutorial, here's what's new.
```diff
-from setuptools import setup
+from setuptools import find_packages, setup


 setup(
-    name='alpha-pkg',
-    version='0.0.0'
+    name='does-this-help',
+    version='0.0.1',
+    packages=find_packages()
 )
```

Just like in the previous tutorial, let's first run the following command to create a source distribution.
```
$ python setup.py sdist
```

Did you notice anything different about the names of the newly created directories?
```
├── dist
│   └── does-this-help-0.0.1.tar.gz
├── does_this_help.egg-info
│   ├── PKG-INFO
│   ├── SOURCES.txt
│   ├── dependency_links.txt
│   └── top_level.txt
```

As before, let's install the package, back out of this repo, and try importing the package from the REPL.
```
$ pip install dist/does-this-help-0.0.1.tar.gz
$ cd ~
```

```python
>>> import alpha
>>> alpha
<module 'alpha' from '/Users/bjw336/opt/miniconda3/envs/pkg-tut/lib/python3.8/site-packages/alpha/__init__.py'>
```

Nice! Not only are we able to import the package, we also get to see the location where the package is installed. The `site-packages` directory is where third-party packages get installed by default -- this is true whether you use pip or conda.

The reason we weren't able to `import alpha` in the previous tutorial is that the source code wasn't copied to the `site-packages` directory. Can you guess which change in `setup.py` made the difference this time around?

You might have noticed we changed the `name` field in `setup.py` to `'does-this-help'`. Let's see if we can import the package using that name.

```python
>>> import does-this-help
  File "<stdin>", line 1
    import does-this-help
               ^
SyntaxError: invalid syntax
```

Nope.

As it turns out, the `name` inside `setup.py` dictates the _distribution name_ of the package. This is the name used by pip and conda, and is also the name for which the package is listed on [PyPI](https://pypi.org/) and the [Anaconda Repository](https://anaconda.org/).

On the other hand, the name of the _directory_ in which the source code lives (`alpha`, in our case) dictates the _import name_ of the package, and is the name that's used in an actual `import` statement.

While in most cases the distribution name and import name are identical, they certainly don't have to be. Here are two examples for which the two names differ. Try to find out which is which.
1. `scikit-learn` vs. `sklearn`. Link to [source code](https://github.com/scikit-learn/scikit-learn)
1. `beautifulsoup4` vs. `bs4`. Link to [source code](https://bazaar.launchpad.net/~leonardr/beautifulsoup/bs4/files)