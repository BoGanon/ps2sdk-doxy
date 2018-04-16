# Introduction
This repository holds doxygen configuration files for ps2sdk.

# Notes
HAVE_DOT = YES is set.
If the graphviz package is not installed, please set to NO in each of the configuration files.

# Generating documentation
```
Copy index.md and doxy-index.conf to ps2sdk
Copy ee/ee.md and ee/doxy-ee.conf to ps2sdk/ee
Copy iop/ee.md and iop/doxy-iop.conf to ps2sdk/iop
```
Then execute the following commands in the following order from the root of ps2sdk.
```sh
doxygen doxy-index.conf
cd ee
doxygen doxy-ee.conf
cd ../iop
doxygen doxy-iop.conf
cd ..
doxygen doxy-index.conf
```
# Location
HTML documents will be located in ps2sdk-doc/html.
# TODO
 - Change ps2sdk's function macros to support doxygen
 - Add doxygen commands to assembly files so they parse correctly
 - Increase GRAPH_MAX_NODES
 - Add descriptions of ee sublibraries to ee.md
 - Add descriptions of iop sublibraries to iop.md
 - Flesh out index.md
 - Customize layout
 - Fix warnings
