# GDXRRW #

GDXRRW is an interface between General Algebraic Modeling System (GAMS) and R. It includes functions to transfer data between GDX and R and a function to call gams from within R.

# How to install #

GDXRRW package can be installed using devtools package. Devtools can be installed by running the following command in R.
```
install.packages("devtools")
```

devtools can then be loaded
```
library(devtools)
```

GDXRRW can be installed as follows.
```
install_github("GAMS-dev/gdxrrw")
```

# Checking if GDXRRW is installed correctly #

After you install GDXRRW you may want to verify that the installation is functioning correctly. The GDXRRW package is not loaded by default, so before the package is available you must load it. This is easily done with the `library(gdxrrw)` command. Once the package is loaded, you can get help on the package as a whole (`help(gdxrrw)`) or the functions or data elements in the package (e.g. `help(igdx)`).

For GDXRRW to work it must load shared libraries from the GAMS system directory. One common problem is a failure to find the GAMS system directory and these shared libraries. The `igdx` command can be used to show what GAMS system directory GDXRRW has found (`igdx()`) and to point GDXRRW to a particular GAMS system directory if so desired (`igdx(“/usr/local/gams/24.4.1”)`). Depending on your system setup, environment variables, and how you start R, GDXRRW may not need any help finding the GAMS system directory, but the `igdx` command allows this binding to be queried and customized if desired.

The R `sessionInfo()` command tells you the version number of packages you have loaded, including gdxrrw. If you need SVN revision info, some commands print that, e.g. `rgdx(“?”)`.

The help pages for the other GDXRRW functions include examples that you can run to quickly verify your system is working.


# The install worked - what next? #
If you are seeing GDXRRW for the first time you should look at the examples and tests that come with GDXRRW. For example, each of the functions `wgdx`, `rgdx`, `igdx`, and `gams` comes with integrated help and examples that can be accessed in the usual way within the R environment, e.g.: `help(rgdx)`. In addition, more complete tests and more substantive examples are included in the `gdxrrw` package. For more recent package versions (0.6.0 and following), package tests are collected in the `tests` directory. Earlier versions put the tests in `extdata`. The sample commands below assume a recent version and sufficient access permission in the package install directory. If you lack such permission copy the files before using them. Some helpful R commands for testing are:

* `setwd (paste0(path.package('gdxrrw'),'/tests'))`
* execute the `tAll.R` script `(source(“tAll.R”)` to run the tests

Some examples are collected in the `extdata` directory:

* `setwd (paste0(path.package('gdxrrw'),'/extdata'))`
* In subdir `TSP`, execute the `egTSP.R` script to export data for a traveling salesman problem to GAMS, solve it, and return the solution to R for plotting
* In subdir `LS`, run the `egLeastSquares.gms` model from GAMS - this calls R as part of the GAMS run to do the data fitting and return the results

# R startup #
R provides multiple ways to customize the environment at startup, e.g. to start with the GDXRRW package loaded. One way is to use the .Rprofile script that is executed from the HOME directory when R starts up.

* For a description of how R starts up: `help(Startup)`
* To find your home directory, especially useful on Windows: `Sys.glob(“~”)`
* To load non-default libraries like GDXRRW on Linux startup, use a .Rprofile with this line:
```
    .First <- function() { library(gdxrrw) ; igdx("/home/sdirkse/gams/24.4.1")}
```
* On 64-bit Windows you can run 64- and 32-bit R. The .Rprofile handles the initialization easily:
```
    .First <- function() {
      library(gdxrrw)
      a <- R.Version()$arch
      if (a == "x86_64")  igdx("/gams_64/24.4.1")
      else                igdx("/gams_32/24.4.1")
    }
```
* To get system information, try `Sys.getenv`:
	* `Sys.getenv(“R_LIBS_USER”)` helps to find user-installed packages
	* `Sys.getenv(“R_USER”)` helps to locate the .Rprofile file, especially on Windows
* To get version information: `R.Version`

# Feedback #
We would love to get feedback on GDXRRW. Please direct your questions, comments, and suggestions to R@gams.com.