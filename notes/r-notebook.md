# R + packrat + Jupyter notebook
(on Ubuntu)

#### R
The R distro from Ubuntu is bad. I'm not sure what exactly is wrong with it, but it was apparently compiled without some necessary components, so that it is unable to do some things which we need to be able to do for this recipe. Add the `cran` mirror to the `/etc/apt/sources.list` file. More details [here](https://cran.r-project.org/bin/linux/ubuntu/README). Make sure to install `r-base-dev`. This way you also get the latest stable R, and not the older ones in the ubuntu mirrors.

#### Packrat
Virtualenv for R. Operate from within the R console, not from commandline. Important commands:

- `install.packages("packrat")` to install it
- `packrat::init("/path/to/project")` to initialize a new env
- `packrat::on("/path/to/project")` to tell packrat to use that env

#### Python
Jupyter is Python, so we also need a Python environment. I don't know yet if Python 3 is a problem for bio tools (that is, if there are essential libraries that only work on Python 2), so I'll give Python 3 a shot.

- Download and compile whatever version you want
- install `virtualenv` and `virtualenvwrapper`
- make a virtual env pointed at your latest python
- in that virtualenv, `pip install jupyter`

#### IRKernel
This is the R kernel for Jupyter. Instructions on how to install it are [on it's github page](https://github.com/IRkernel/IRkernel). I had some problems with wrong packages installed on my Ubuntu, which I fixed by:

- compiling and installing `libsodium`, found [here](https://download.libsodium.org/libsodium/releases/)
- then, compiling and installing the latest `zeromq`, found [here](http://zeromq.org/intro:get-the-software)
- and then it works.

You need to install `IRKernel` in the system R libs, and **not only in your packrat project**. This is because when you start a new Jupyter notebook with the R kernel, it looks for system R. (maybe unless you are in the right working directory, but that's limiting?).

#### Using the notebook
```bash
jupyter notebook
```

This starts the notebook server and opens your browser pointing at it. You can open new notebooks and pick the R kernel.

Inside your new notebook, make sure to, in the first line, hit

```r
packrat::on("/path/to/project")
```

so that the notebook will use your correct environment when you try to load libraries.

### Example notebook
[here](r_notebook.html).



