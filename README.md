# Kattis Problem Tools - For icelandic programming competitions

## Modifications: 

Currently:
* "Sample Input", "Sample Output" and "Sample Interaction" translated in problem2pdf

Planned:
* translate the rest of problem2pdf and problem2html

## Programs Provided

The problem tools provide the following three programs:

 - `verifyproblem`: run a complete check on a problem
 - `problem2pdf`: convert a problem statement to pdf
 - `problem2html`: convert a problem statement to html

Running any of them with the command-line option `-h` gives
documentation on what arguments they accept.


## Example Problems

A few examples of problem packages can be found in [examples](examples).


## Installing problemtools

There are four supported ways of installing and running problemtools.
(For non-Linux users, "Method 2" below, to use Docker, is probably the least painful.)

Install the Python package

Run
```
sudo pip3 install git+https://github.com/Tskoli-Kodun/problemtools-is
```

Or if you don't want a system-wide installation,
```
pip3 install --user git+https://github.com/Tskoli-Kodun/problemtools-is
```
With this second option, in order to get the command line scripts, you need
to make sure that the local user bin path used (e.g., on Linux,
`$HOME/.local/bin`) is in your `$PATH`.

In order for problemtools to build and run properly, you also need to have LaTeX
and various LaTeX packages installed.  See [Requirements and
compatbility](#requirements-and-compatibility) below for details on
which packages are needed.


### Method 2: Run directly from the repository.

If you intend to help develop problemtools, or if you just want a
bare-bones way of running them, this is your option.

For this method, you need to clone the repository (just downloading a
zip archive of it does not work because the project has submodules
that are not included in that zip archive).

In order for the tools to work, you first have to compile the various
support programs, which can be done by running `make` in the root
directory of problemtools.

When this is done, you can run the three programs
`bin/verifyproblem.sh`, `bin/problem2pdf.sh`, and
`bin/problem2html.sh` directly from the repository.

See [Requirements and compatibility](#requirements-and-compatibility)
below for what other software needs to be installed on your machine in
order for problemtools to work correctly.


## Configuration

System-wide problemtools configuration files are placed in
`/etc/kattis/problemtools/`, and user-specific configuration files are placed
in `$HOME/.config/problemtools/` (or in `$XDG_CONFIG_HOME` if this is defined).  The following files can be used to change
problemtools' configuration:

1. `languages.yaml`.  Use it to override problemtools' default
   programming language configuration.  For instance, while the
   problemtools default is to use the CPython `/usr/bin/python3`
   interpreter for Python 3, many contests, as well as the Kattis
   online judge, use Pypy as the interpreter for Python 3.  To change
   this on your machine, you can simply place a file
   `/etc/kattis/problemtools/languages.yaml` (or
   `~/.config/problemtools/languages.yaml` if you only want to make the
   change for your user) containing the following:

   ```yaml
   python3:
      name: 'Python 3 w/Pypy'
      run: '/usr/bin/pypy3 "{mainfile}"'
   ```
   Here, overriding the name of the language is not strictly
   necessary, but it is often helpful to clearly indicate that Pypy is
   being used.

   For more details on the format of the language specifications and
   what the default settings are, see the [default version of
   languages.yaml](problemtools/config/languages.yaml)

2. `problem.yaml`.  For most users, this should not be edited.  If you
   are not sure whether you should use it, then you probably shouldn't.
   This file can be used to specify the system defaults for those
   problem limits which are not given a fixed default value in the
   [problem format specification](http://www.problemarchive.org/wiki/index.php/Problem_Format#limits).
   The system defaults assumed by problemtools can be found in
   (problemtools/config/problem.yaml).  For instance, if you are
   primarily working against a system with a default memory limit of 2 GiB,
   you can place a file `~/.config/problemtools/problem.yaml` containing:

   ```yaml
   limits:
       memory: 2048 # (unit is MiB)
   ```

   (In principle, it is possible to override the defaults of other values than the
   system-dependent defaults in the problem.yaml metadata files this way, but such
   usage is very strongly discouraged.)


## Requirements and compatibility

To build and run the tools, you need Python 3 with the YAML and PlasTeX libraries,
and a LaTeX installation.

### Ubuntu

The dependencies needed to *build/install* problemtools can be installed with:

    sudo apt install automake g++ make libboost-regex-dev libgmp-dev libgmp10 libgmpxx4ldbl python3 python3-pytest python3-setuptools python3-yaml python3-plastex

And the dependencies needed to *run* problemtools can be installed with:

    sudo apt install ghostscript libgmpxx4ldbl python3-minimal python-pkg-resources python3-plastex python3-yaml texlive-fonts-recommended texlive-lang-cyrillic texlive-latex-extra texlive-plain-generic tidy

### Fedora

On Fedora, these dependencies can be installed with:

    sudo dnf install boost-regex gcc gmp-devel gmp-c++ python3 python3-pyyaml texlive-latex texlive-collection-fontsrecommended texlive-fancyhdr texlive-subfigure texlive-wrapfig texlive-import texlive-ulem texlive-xifthen texlive-overpic texlive-pbox tidy ghostscript

Followed by:

    pip3 install --user plastex

### Arch
Package is available on the AUR [kattis-problemtools-git](https://aur.archlinux.org/packages/kattis-problemtools-git). Use your favorite AUR helper or follow the installation instructions found [here](https://wiki.archlinux.org/title/Arch_User_Repository#Installing_and_upgrading_packages).

### Other platforms

The problem tools have not been tested on other platforms.  If you do
test on another platform, we would be happy to hear what worked and what
did not work, so that we can write proper instructions (and try to
figure out how to make the non-working stuff work).
