███╗   ██╗███████╗     ██████╗ 
████╗  ██║██╔════╝     ╚════██╗
██╔██╗ ██║███████╗█████╗█████╔╝
██║╚██╗██║╚════██║╚════╝╚═══██╗
██║ ╚████║███████║     ██████╔╝
╚═╝  ╚═══╝╚══════╝     ╚═════╝ 

╦┌┐┌┌─┐┌┬┐┌─┐┬  ┬  ┌─┐┌┬┐┬┌─┐┌┐┌
║│││└─┐ │ ├─┤│  │  ├─┤ │ ││ ││││
╩┘└┘└─┘ ┴ ┴ ┴┴─┘┴─┘┴ ┴ ┴ ┴└─┘┘└┘

To install the lastest version of ns-3 (This example uses ns-3.35, change according to current version):

Go to https://www.nsnam.org/releases/latest/ and download the latest release in the home folder.
Open a terminal and execute the following commands:
(having an src folder to store program builds is good practice)
$ mkdir -p ~/src
$ mv ns-allinone-3.35.tar.bz2 ~/src
$ cd ~/src
$ tar -xjf ns-allinone-3.35.tar.bz2
$ cd ns-allinone-3.35

Here there is 3 options (Option 2 is preferred):

1.  You can build it using native build system "waf":
    $ cd ns-3.35
    You have to configure the waf with allowed values: 'debug', 'optimized' or 'release' (use ./waf --help for more info):
    $ ./waf clean
    $ ./waf configure --build-profile=optimized --enable-examples --enable-tests

    The program will start to configure the waf with the variant you chose, and it will print out a message similar to the one bellow:
    > 'configure' finished successfully (3.798s)

    Finally, start to build using the following command
    $ ./waf

2.  You can build it using the convenience script "build.py" which calls tne "waf" and installs all available modules:
    $ ./build.py --enable-examples --enable-tests

3.  You can build it using "bake" which is similar to "build.py" but might have dependency issues:
    $ ./bake.py build

The program will start to build ns-3, which will take some time. The result will show a message similar to the one bellow along with a list of installed modules:
> 'build' finished successfully (3m17.374s)

Now you can delete the file you downloaded and start using ns-3
$ rm ~/src/ns-allinone-3.35.tar.bz2

╔╦╗┌─┐┌─┐┌┬┐┬ ┌┐┌┌─┐
 ║ ├┤ └─┐ │ │ ││││ ┬
 ╩ └─┘└─┘ ┴ ┴ ┘└┘└─┘

To use the ns-3 program you must be under the path:
$ cd ~/src/ns-allinone-3.35/ns-3.35

Now, you can test your build by executing the following commands:
$ ./test.py -c core # For core modules
$ ./test.py # For all modules (this will take longer)

You can also run a script:
$ ./waf --run hello-simulator

To build your own programs, place them under /scratch/. In this example, a program "my-program.cc" is created and built.
$ touch ./scratch/my-program.cc
$ ./waf
> Compiling scratch/my-program.cc
>'build' finished successfully (2.755s)

To run your own programs, use the following command, arguments are optional:
$ ./waf --run my-program --command-template="%s arguments"
or just run them with no build:
$ ./waf --run-no-build 'my-program --arg1=value1 --arg2=value2 ...'

╔═╗─┐ ┬┌─┐┌┬┐┌─┐┬  ┌─┐┌─┐
║╣ ┌┴┬┘├─┤│││├─┘│  ├┤ └─┐
╚═╝┴ └─┴ ┴┴ ┴┴  ┴─┘└─┘└─┘
