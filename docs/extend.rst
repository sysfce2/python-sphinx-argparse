Extending results of ``argparse`` directives
============================================

You can add extra content or even replace some parts of the documentation generated by the ``argparse`` directive.
For example, any content you put inside directives (you must follow ReStructuredText identation rules) will be inserted just before the argument and option list:

.. code:: rst

   .. argparse::
      :module: my.module
      :func: my_func_that_return_parser
      :prog: fancytool

       My content here that will be inserted right before the argument list.

       Also any valid markup...
       *************************

       ... may ``be`` *applied* here

       including::

            any directives you usually use.


Also, there is an option to insert custom content into a specific argument/option/subcommand/argument-group description.
Just create a name:definition pair, where the name is an argument/option/subcommand/argument-group name and the definition is any reStructured markup.
Changes to options/arguments appearing in multiple action groups can either be targeted (i.e., only one instance of the argument is changed) or general (i.e., all instances are modified).

.. code:: rst

   .. argparse::
      :module: my.module
      :func: my_func_that_return_parser
      :prog: fancytool

      My content here that will be inserted right before the argument list.

      foo
           This text will go right after the "foo" positional argument help.

      install
           This text will go right after the "install" subcommand help and before its arguments.

           --upgrade -u
               This text will go after the upgrade option of the install subcommand. Nesting is unlimited.
               Note the space between --upgrade and -u, which differs from the comma that would normally
               be used.

       --output -o
           Content appended to the --output option, regardless of the argument group.


You can also add classifiers, which will change how these definitions are incorporated:

.. code:: rst

   .. argparse::
      :module: my.module
      :func: my_func_that_return_parser
      :prog: fancytool

      My content that will be inserted right before the argument list.

      foo : @before
           This text will go before the "foo" positional argument help.

      install : @replace
           This text will replace the "install" subcommand help/description.

           --upgrade : @after
               The after directive is the default, so you needn't specify it.

      advanced arguments : @skip
           skip advanced arguments


@before
    Insert content before the parsed help/description message of the argument/option/subcommand/argument-group.

@after
    Insert content after the parsed help/description message of argument/option/subcommand/argument-group. This is the default.

@replace
    Replace content of help/description message of argument/option/subcommand/argument-group.

@skip
    Skip the content of help/description message of subcommand/argument-group.
