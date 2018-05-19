# Introduction #
Doxygen configuration files for ps2sdk. For complete documentation use the `posix` branch of ps2sdk located in my fork.

HAVE_DOT = YES is set.

If the graphviz package is not installed, please set to NO in each of the configuration files.

# Generating documentation #

Copy docs directory to ps2sdk

Then execute the following commands in the following order from the root of ps2sdk. This creates an `html` directory and allows for the search engine to be used from the main page. Some results are repeated since the common subdirectory is included in both the ee and iop configurations.
```sh
cd docs
doxygen doxy-index.conf
doxygen doxy-ee.conf
doxygen doxy-iop.conf
doxygen doxy-index.conf
```
HTML documents will be located in docs/html.

# TODO #
 - Add more descriptions of ee libraries to ee.md
 - Add more descriptions of iop libraries to iop.md
 - Document more of ps2sdk
