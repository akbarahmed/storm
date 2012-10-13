README: Storm Documentation Source
==================================

This is the Storm documentation source directory. Storm documentation
is written with Docbook 4.

Build the Documentation
-----------------------

$ cd $STORM_REPO_HOME/storm/docs

$ xmlto -m src/config.xsl xhtml src/QuickStartUbuntu.xml

# Rename the .html file (I need to make this part of the transformation step)
$ mv index.html QuickStartUbuntu.html

# Clean up after the build
rm *.proc

# Open the QuickStart.html file and make a few updates (again, I really need to use a better
# build process so that this is not necessary.
#
# %s/index.html/QuickStartUbuntu.html/gc
