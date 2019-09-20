###########
Style Guide
###########

*******************
Style Guide for C++
*******************

-  4 space indentation

-  `snake\_case <https://en.wikipedia.org/wiki/Snake_case>`__ for
   variables filenames

-  underscores after class member variables

   -  eg. ``int size_``

-  `camelCase <https://en.wikipedia.org/wiki/Camel_case>`__ for
   functions, methods

-  `PascalCase <https://en.wikipedia.org/wiki/PascalCase>`__
   (capitalised camelCase) for classes

Refer to the `Google Style
Guide <https://google.github.io/styleguide/cppguide.html#General_Naming_Rules>`__
for naming.

**********************
Style Guide for Python
**********************

rUNSWift uses the Python community's standard
`PEP8 <https://www.python.org/dev/peps/pep-0008/>`__, as enforced by
`flake8 <http://flake8.pycqa.org/>`__ in a git hook.

.. tip::
    As PEP8 is strict, install a python linter for your IDE.

.. seealso::
    :ref:`ide_addons` for linters for your IDE

*****************
EditorConfig file
*****************

`EditorConfig <https://editorconfig.org/>`_ helps maintain consistent coding styles
for multiple developers working on the same project across various editors and IDEs.

``$RUNSWIFT_CHECKOUR_DIR/.editorconfig`` file contains the style settings for different languages.

.. seealso::
    :ref:`ide_addons` to see editorConfig addons for your IDE
