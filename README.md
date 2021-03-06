# swarmlib

[![Pypi](https://img.shields.io/pypi/v/swarmlib.svg?style=flat-square)](https://pypi.python.org/pypi/swarmlib) [![PyPI - Python Version](https://img.shields.io/pypi/pyversions/swarmlib.svg?style=flat-square)](https://pypi.python.org/pypi/swarmlib) [![PyPI - Downloads](https://img.shields.io/pypi/dm/swarmlib.svg?style=flat-square)](https://pypistats.org/packages/swarmlib) [![Stars](https://img.shields.io/github/stars/HaaLeo/swarmlib.svg?label=Stars&logo=github&style=flat-square)](https://github.com/HaaLeo/swarmlib/stargazers)  
[![PyPI - License](https://img.shields.io/pypi/l/swarmlib.svg?style=flat-square)](https://raw.githubusercontent.com/HaaLeo/swarmlib/master/LICENSE.txt) 
[![Build Status](https://img.shields.io/travis/HaaLeo/swarmlib/master.svg?style=flat-square)](https://travis-ci.org/HaaLeo/swarmlib) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)  
[![Chat on Gitter](https://img.shields.io/badge/-chat%20on%20gitter-753a88.svg?logo=gitter&style=flat-square&labelColor=grey)](https://gitter.im/HaaLeo/swarmlib) [![Donate](https://img.shields.io/badge/☕️-Buy%20Me%20a%20Coffee-blue.svg?&style=flat-square)](https://www.paypal.me/LeoHanisch/3eur)

## Description

This repository implements several swarm optimization algorithms and visualizes their (intermediate) solutions.
To run the algorithms one can either use the CLI (recommended) or the API.
Currently, the following algorithms are implemented:
* [Firefly Algorithm](#firefly-algorithm)
* [Cuckoo Search](#cuckoo-search)
* [Particle Swarm Optimization](#particle-swarm-optimization)
* [Ant Colony Optimization](#ant-colony-optimization)
* [Artificial Bee Colony](#artificial-bee-colony)
* [Grey Wolf Optimization](#grey-wolf-optimization)

## Installation

You can install the package with `pip` from [pypi](https://pypi.org/project/swarmlib).
Installing the library in a virtual environment is recommended:

```zsh
# Create virtual environment
python3 -m venv .venv
source .venv/bin/activate

# Install swarmlib
pip install swarmlib

# Verify installation
swarm --version
```

## Usage

To print all available algorithms:

```
swarm --help
```

## Contribution

If you found a bug or are missing a feature do not hesitate to [file an issue](https://github.com/HaaLeo/swarmlib/issues/new/choose).  
Do not hesitate to ask questions on [gitter](https://gitter.im/HaaLeo/swarmlib).

Pull Requests are welcome!

## Support
When you like this package make sure to [star the repository](https://github.com/HaaLeo/swarmlib/stargazers).
I am always looking for new ideas and feedback.

In addition, it is possible to [donate via paypal](https://www.paypal.me/LeoHanisch/3eur).

## Algorithms

### Firefly Algorithm

This repository includes the _firefly algorithm_ like Xin-She Yang introduced in his paper [Firefly Algorithms for Multimodal Optimization](https://link.springer.com/chapter/10.1007%2F978-3-642-04944-6_14) in 2009 (DOI: 10.1007/978-3-642-04944-6_14).  
The implementation was part of the course [Natural computing for learning and optimisation](https://is.cuni.cz/studium/eng/predmety/index.php?do=predmet&kod=NPFL107) at Charles University Prague in winter 2018/2019.

#### Features

Enables to apply the firefly algorithm to one of the provided 2D functions. The algorithm tries to find the global minimum of the selected function.  

Currently two functions can be selected:
* [ackley](https://www.sfu.ca/~ssurjano/ackley.html)
* [michalewicz](https://www.sfu.ca/~ssurjano/michal.html)

![firefly algorithm](https://raw.githubusercontent.com/HaaLeo/swarmlib/master/doc/fireflies.gif)

To print all available options execute:

```
swarm fireflies -h
```

#### API

In addition to the cli you can also use the API:

```python
from swarmlib import FireflyProblem, FUNCTIONS

problem = FireflyProblem(function=FUNCTIONS['michalewicz'], firefly_number=14)
best_firefly = problem.solve()
problem.replay()
```

### Cuckoo search

This repository also implements the _cuckoo search_ that was introduced by Xin-She Yang and Suash Deb in their paper [Cuckoo Search via Lévy flights](https://ieeexplore.ieee.org/document/5393690) in 2009 (DOI: 10.1109/NABIC.2009.5393690).  

#### Features

Enables to apply cuckoo search to one of the provided 2D functions. The algorithm tries to find the global minimum of the selected function.  

Currently two functions can be selected:
* [ackley](https://www.sfu.ca/~ssurjano/ackley.html)
* [michalewicz](https://www.sfu.ca/~ssurjano/michal.html)

![cukoo search](https://raw.githubusercontent.com/HaaLeo/swarmlib/master/doc/cuckoos.gif)

The plot shows all nests of the current cuckoo generation as _red_ markers. The best nests of all (previous) generations are indicated by _yellow_ markers. The abandonment of a nest is indicated by a _dark grey_ transition.

To print all available options execute:

```
swarm cuckoos -h
```

#### API

In addition to the cli you can also use the API:

```python
from swarmlib import CuckooProblem, FUNCTIONS

problem = CuckooProblem(function=FUNCTIONS['michalewicz'], nests=14)
best_nest = problem.solve()
problem.replay()
```
### Particle Swarm Optimization

This repository also implements modified _particle swarm optimization_ that was introduced by Yuhui Shi and Russell C. Eberhart in their paper [A modified particle swarm optimizer](https://ieeexplore.ieee.org/document/699146) in 1998 (DOI: 10.1109/ICEC.1998.699146). Their approach introduces a so called _inertia weight_ w. To get the [original particle swarm optimization](https://ieeexplore.ieee.org/document/488968) algorithm, just set the parameter `--weight=1`.

#### Features

Enables particle swarm optimization to one of the provided 2D functions. The algorithm tries to find the global minimum of the selected function.  

Currently two functions can be selected:
* [ackley](https://www.sfu.ca/~ssurjano/ackley.html)
* [michalewicz](https://www.sfu.ca/~ssurjano/michal.html)

![particle swarm optimization](https://raw.githubusercontent.com/HaaLeo/swarmlib/master/doc/particles.gif)

The plot shows all particles and their velocities.

To print all available options execute:

```
swarm particles -h
```

#### API

In addition to the cli you can also use the API:

```python
from swarmlib import PSOProblem, FUNCTIONS

problem = PSOProblem(function=FUNCTIONS['michalewicz'], particles=14)
best_particle = problem.solve()
problem.replay()
```

### Ant Colony Optimization

This repository includes an _ant colony optimization_ algorithm for the traveling salesman problem (TSP) like Marco Dorigo, Mauro Birattari, and Thomas Stuetzle introduced in the [IEEE Computational Intelligence Magazine](https://ieeexplore.ieee.org/document/4129846) in November 2006 (DOI: 10.1109/MCI.2006.329691).  
The implementation was part of the course [Natural computing for learning and optimisation](https://is.cuni.cz/studium/eng/predmety/index.php?do=predmet&kod=NPFL107) at Charles University Prague in winter 2018/2019.

#### Features

Enables to apply the ant colony optimization algorithm to a TSP using a [TSPLIB95](http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/) file and plots the result.

![ACO Sample](https://raw.githubusercontent.com/HaaLeo/swarmlib/master/doc/ants.gif)

The algorithm solves the TSP and plots the result all _n_ iterations.  
The nodes are plot according to their coordinates read from the TSPLIB95 file. The _widths_ of the edges indicate the _amount of pheromone_ that is associated with this edge. If an edge is _blue_, it is part of the _best found path_.

To print all available options execute:

```
swarm ants -h
```

#### API

In addition to the cli you can also use the API:

```python
from swarmlib import ACOProblem

problem = ACOProblem(ant_number=10)
path, distance = problem.solve()
problem.replay()
```

### Artificial Bee Colony

The Artificial Bee Colony (ABC) algorithm was initially proposed 2005 by Dervis Karaboga in his paper [An Idea Based on Honey Bee Swarm For Numerical Optimization](https://pdfs.semanticscholar.org/015d/f4d97ed1f541752842c49d12e429a785460b.pdf).
In his paper Karaboga did not specify _how exactly_ new solutions shall be discovered. 

Research has shown that the flight behavior of birds, fruit flies and other insects model properties of Levy flights ([Brown, Liebovitch & Glendon, 2007](https://link.springer.com/article/10.1007/s10745-006-9083-4); [Pavlyukevich, 2007](https://arxiv.org/pdf/cond-mat/0701653.pdf)). Therefore, this library's ABC implementation leverages levy flights to generate new solutions.

#### Features

Enables the ABC algorithm to one of the provided 2D functions. The algorithm tries to find the global minimum of the selected function.

Currently two functions can be selected:
* [ackley](https://www.sfu.ca/~ssurjano/ackley.html)
* [michalewicz](https://www.sfu.ca/~ssurjano/michal.html)

![ABC Sample](https://raw.githubusercontent.com/HaaLeo/swarmlib/master/doc/bees.gif)

The plot shows all _employee bees_ as _red_ markers, the _onlooker bees_ are visualized as _blue_ markers. The best bees of all (previous) iterations are indicated by _yellow_ markers. When an employee bee exceeded its maximum _trials_ the bee is assigned a new random position. This is visualized by a _dark grey_ transition.
Since the onlooker bees pick up an employee bee's position randomly visualizing their transitions confuses rather than it helps understanding the algorithm and therefore is omitted.

To print all available options execute:

```
swarm bees -h
```

#### API

In addition to the cli you can also use the API:

```python
from swarmlib import ABCProblem, FUNCTIONS

problem = ABCProblem(bees=10, function=FUNCTIONS['michalewicz'])
best_bee = problem.solve()
problem.replay()
```

### Grey Wolf Optimization

The Grey Wolf Optimization (GWO) algorithm was proposed by S. Mirjalili et  al. in the paper [Grey Wolf Optimizer](https://www.sciencedirect.com/science/article/pii/S0965997813001853?casa_token=IJMUjrkkBVkAAAAA:TIW5bZqXDqgQwD1aX-5vqsDvmf4AgWFODvWepUiZi79MgSii3MlDMXMwgMVPcQvuGlZYLKm5GA).
The paper proposed a novel algorithm based on the hunting and the hierarchy structure in grey wolves

#### Features

Enables the GWO algorithm to one of the provided 2D functions. The algorithm tries to find the global minimum of the selected function.

Currently two functions can be selected:
* [ackley](https://www.sfu.ca/~ssurjano/ackley.html)
* [michalewicz](https://www.sfu.ca/~ssurjano/michal.html)

![GWO Sample](https://raw.githubusercontent.com/HaaLeo/swarmlib/master/doc/gwo.gif)

To print all available options execute:

```
swarm wolves -h
```

#### API

In addition to the cli you can also use the API:

```python
from swarmlib import GWOProblem, FUNCTIONS

problem = GWOProblem(wolves=10, function=FUNCTIONS['michalewicz'])
best_wolf = problem.solve()
problem.replay()
```
