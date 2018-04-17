# Introduction
This repository holds doxygen configuration files for ps2sdk.

# Notes
HAVE_DOT = YES is set.
If the graphviz package is not installed, please set to NO in each of the configuration files.

# Generating documentation
```
Copy docs directory to ps2sdk
```

Then execute the following commands in the following order from the root of ps2sdk.
```sh
cd docs
doxygen doxy-index.conf
doxygen doxy-ee.conf
doxygen doxy-iop.conf
doxygen doxy-index.conf
```

# Location
HTML documents will be located in docs/html.

# TODO
 - Add doxygen commands to assembly files so they parse correctly
 - Add descriptions of ee sublibraries to ee.md
 - Add descriptions of iop sublibraries to iop.md
 - Flesh out index.md
 - Customize layout
 - Fix warnings
