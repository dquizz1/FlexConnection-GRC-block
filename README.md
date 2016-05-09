# FlexConnection-GRC-block
GRC block that connects to a flexradio and receives IQ data stream

Steps:
First Install Mono using commands:
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF 

$ echo "deb http://download.mono-project.com/repo/debian wheezy main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list

$ sudo apt-get update

$ sudo apt-get install Mono-Complete

$ mono --version (MAKE SURE ITS MOST RECENT)

Next Download FlexlibMono from github using command

$ git clone https://github.com/krippendorf/FlexlibMono.git && cd FlexlibMono && ./buildtools.sh    
(Checkout github.com/krippendorf)
To test downloaded package code use command to connect to Flex radio

$ cd FlexlibMono/tools

$ ./HB9FXQ.DaxIqCat.exe 192000 1 "192.168.1.123" 4992

The values but on the command above after .exe are [samplerate] [daxchannel] [users Ip address] [Port number]
Is successful, a "Waiting for radio" SENTENCE should appear with connection details like frequency and dax channels that are streaming

Installing GRC:
Use the following commands to install GRC

$ git clone --recursive http://git.gnuradio.org/git/gnuradio.git

$ cd gnuradio

$ mkdir build

$ cd build

$ cmake ../

$ make && make test

$ sudo make install

****Note: If it requires boost and cheetah use commands below to get them

$ sudo apt-get install python-cheetah

$ sudo apt-get install libboost-all-dev

Then use commands to install GRC companion

$ sudo apt-get install gnuradio

When successfull check installation by using

$ grc

to open gnu radio companion software.

Using Flex Block
The flex block is created using gr_modtool (http://gnuradio.org/redmine/projects/gnuradio/wiki/OutOfTreeModules), the code can be editted if the user wants to enhance its functions. Access to codes are in gr-Flexradio/lib directory to edit "flex_impl.cc" and "flex_impl.h" and also gr-flex/include/flex directory to edit "flex.h" codes.
Basic function for Flex block are:
Connect to any Flexradio IQ stream using Samplerate, daxchannel, IP address and Port number.
It also generates the telnet feature on the terminal for input of desired commands to radio


BUILDING BLOCK IN GRC

Once the codes have been updated, the following commands are used to install and make a gnu radio block using CMake.

•	$ cd gr-flex $ mkdir build (to create build directory) 

•	gr-flex $ cd build

•	gr-flex/build $ cmake ../

•	gr-flex/build $ make clean (to make sure there is no preexisting make file)

•	gr-flex/build $ make

•	gr-flex/build $ make test (to run python test file to confirm if radio is connectable)

When this test case is run the terminal should open and create a connection to Flex radio as previously observed when the .exe mono file was run. After inputting this steps, the flexconnect codes are compiled and built into the operating system. Next I used the following commands to first make an xml file then install the block code.

•	gr-flex/build $ cd ..

•	gr-flex $ gr_modtool makexml flexconnect (creates an xml file)

•	Input yes if asked to overwrite pre-existing xml file then

•	gr-flex $ cd build

•	gr-flex/build $ sudo make install (installing our block code to grc)

•	gr-flex/build $ sudo ldconfig (this configures our block)

