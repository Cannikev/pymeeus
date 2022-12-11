# PyMeeus
> **Library of astronomical algorithms in Python**.

PyMeeus is a Python implementation of the astronomical algorithms described in
the classical book 'Astronomical Algorithms, 2nd Edition, Willmann-Bell Inc.
(1998)' by Jean Meeus.

There are great astronomical libraries out there. For instance, if you're
looking for high precision and speed you should take a look at
[libnova](http://libnova.sourceforge.net/). For a set of python modules aimed
at professional astronomers, you should look at [Astropy](http://www.astropy.org/).
On the other hand, the advantages of PyMeeus are its simplicity, ease of use,
ease of reading, ease of installation (it has the minimum amount of
dependencies) and abundant documentation.

## Installation

The easiest way of installing PyMeeus is using pip:

```sh
pip install pymeeus
```

Or, for a per-user installation:

```sh
pip install --user pymeeus
```

If you prefer Python3, you can use:

```sh
pip3 install --user pymeeus
```

If you have PyMeeus already installed, but want to upgrade to the latest version:

```sh
pip3 install -U pymeeus
```

## Properly Using PyMeeus

It is very common to try to run PyMeeus like this:


```sh
import pymeeus

mydate = pymeeus.Epoch(1992, 10, 13.0)
```

But if you do that, you'll get an error like this:

```sh
Traceback (most recent call last):
  File "/home/user/test/test.py", line 3, in <module>
    epoch = pymeeus.Epoch(1992, 10, 13.0)
AttributeError: module 'pymeeus' has no attribute 'Epoch'
```

This issue points to a misunderstanding that is very common in the Python world. The keyword ``import`` is used to import **MODULES**... but PyMeeus is **_NOT_** a module: It is a **LIBRARY** composed of **MULTIPLE** modules (``Angle``, ``Epoch``, ``Coordinates``, etc). As of today, the library Pymeeus has 19 different modules (if you look into the directory where ``pip`` stores the library, you'll find one ".py" file per module).

Therefore if you want to use, for example, the module ``Angle`` you should use:

```sh
import pymeeus.Angle
```

I.e., your _module_ is ``pymeeus.Angle``, and not just ``Angle``.

But there is more! When you use ``import`` to fetch a module, you must then use the _dot_ notation to access the components of the module (classes, functions, etc). For instance:

```sh
import pymeeus.Angle

i = pymeeus.Angle.Angle(11.94524)
```

In this case, you are telling the Python interpreter that you want to use the class ``Angle`` (with parameter '11.94524') from the module ``Angle`` belonging to the library ``pymeeus``.

There is, however, a more practical (and common) way to handle modules using the statement ``from <MODULE> import <COMPONENT>``. For instance:

```sh
from pymeeus.Angle import Angle
from pymeeus.Epoch import Epoch, JDE2000
from math import sin, cos, tan, acos, atan2, sqrt, radians, log10
```

This way is preferred because, among other reasons, only the required components are loaded into memory instead of the whole module. Also, now the component is directly added to your execution environment, which means that you no longer need to use the _dot_ notation.

Therefore, the script at the beginning would become:

```sh
from pymeeus.Epoch import Epoch

mydate = Epoch(1992, 10, 13.0)
```

## Meta

Author: Dagoberto Salazar

Distributed under the GNU Lesser General Public License v3 (LGPLv3). See
``LICENSE.txt`` and ``COPYING.LESSER`` for more information.

Documentation: [https://pymeeus.readthedocs.io/en/latest/](https://pymeeus.readthedocs.io/en/latest/)

GitHub: [https://github.com/architest/pymeeus](https://github.com/architest/pymeeus)

If you have Sphinx installed, you can generate your own, latest documentation going to directory 'docs' and issuing:

```sh
make html
```

Then the HTML documentation pages can be found in 'build/html'.

## Contributing

The preferred method to contribute is through forking and pull requests:

1. Fork it (<https://github.com/architest/pymeeus/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request

Please bear in mind that PyMeeus follows the PEP8 style guide for Python code
[(PEP8)](https://www.python.org/dev/peps/pep-0008/?). We suggest you install
and use a linter like [Flake8](http://flake8.pycqa.org/en/latest/) before
contributing.

Additionally, PyMeeus makes heavy use of automatic tests. As a general rule,
every function or method added must have a corresponding test in the proper
place in `tests` directory.

Finally, documentation is also a big thing here. Add proper and abundant
documentation to your new code. This also includes in-line comments!!!.

## Contributors

* [Neil Freeman](https://github.com/fitnr) - Fixed undefined variable in Epoch.tt2ut
* [molsen234](https://github.com/molsen234) - Fixed bug when using fractional seconds, minutes, hours or days
* [Sebastian Veigl](https://github.com/sebastian1306) - Added functionality for Jupiter's moons
* Sophie Scholz - Added functionality for Jupiter's moons
* Vittorio Serra - Added functionality for Jupiter's moons
* Michael Lutz - Added functionality for Jupiter's moons
* [Ben Dilday](https://github.com/bdilday) - Added `__hash__()` method to class Epoch
* [Zivoslav](https://github.com/zivoslav) - Bug report of winter solstice
* [Devid](https://github.com/sevdog), [Hugo van Kemenade](https://github.com/hugovk) - Test suggestions

## What's new

* 0.5.12
    * Fixed a bug in the computation of the winter solstice. Added new tests and information about proper use of the library.
* 0.5.11
    * Added parameter `local` to the `Epoch` class constructor and the methods `get_date()` and `get_full_date()`.
* 0.5.10
    * Added methods ``moon_librations()`` and ``moon_position_angle_axis()``.
* 0.5.9
    * Added method ``moon_maximum_declination()``.
* 0.5.8
    * Fixed several bugs in ``Epoch`` class, and added method ``doy()``.
* 0.5.7
    * Added method ``moon_passage_nodes()``.
* 0.5.6
    * Added method ``moon_perigee_apogee()``.
* 0.5.5
    * Added method ``moon_phase()``.
* 0.5.4
    * Added methods ``illuminated_fraction_disk()`` and ``position_bright_limb()`` to ``Moon`` class.
* 0.5.3
    * Fixed error in the return type of method `Sun.equation_of_time()`.
* 0.5.2
    * Added methods to compute the Moon's longitude of ascending node and perigee.
* 0.5.1
    * Changes in the organization of the documentation.
* 0.5.0
    * Added `Moon` class and `position()` methods.
* 0.4.3
    * Added method `ring_parameters()` to Saturn class.
* 0.4.2
    * Added method `__hash__()` to Epoch. Now Epoch objects can be used as keys in a dictionary.
* 0.4.1
    * Added funtionality to compute the positions of Jupiter's Galilean moons.
* 0.4.0
    * Added methods to compute Saturn's ring inclination and longitude of ascending node.
* 0.3.13
    * Additional encoding changes.
* 0.3.12
    * Deleted `encoding` keyword from setup.py, which was giving problems.
* 0.3.11
    * Added encoding specification to setup.py.
* 0.3.10
    * Fixed characters with the wrong encoding.
* 0.3.9
    * Relaxed requirements, added contributor molsen234, and fixed format problems showed by flake8.
* 0.3.8
    * Fixed undefined variable in `Epoch.tt2ut`.
* 0.3.7
    * Fix bug when using fractional seconds, minutes, hours or days, plus documentation improvements.
* 0.3.6
    * Add method to compute rising and setting times of the Sun.
* 0.3.5
    * Add method `magnitude()` to planet classes.
* 0.3.4
    * Add method to compute the parallax correction to Earth class.
* 0.3.3
    * Add methods to compute the passage through the nodes.
* 0.3.2
    * Add methods to compute the perihelion and aphelion of all planets.
* 0.3.1
    * Fix errors in the elongation computation, add tests and examples of use of methods `geocentric_position()`, and tests and examples for `Pluto` class.
* 0.3.0
    * Added `Pluto` class.
