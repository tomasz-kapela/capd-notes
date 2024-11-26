# CAPD Installation on Mac 

1) Install C++ compiler from Command Line Tools (it is also shipped with XCode) by doing one of the following:

   * Download and install **Command Line Tools** from Apple Developers.

     ```bash
     xcode-select --install
     ```
     
   * Install **Xcode** from App Store (it is quite heavy ~40GB). It provides also an IDE.
     
2. If you have an **M1, M2, M3 chip**, to use the filib interval library one needs **Rosetta** (Intel processor emulator).
   *If you have an Intel mac or if you want to use native CAPD interval library(experimental), ignore this step*.
   You can check architecture using  `arch` command. Result `arm` indicates `Mx` architecture, for intel and Rosetta emulator it should be `i386`.

   In Finder find Terminal (which should be in Applications/Utilities/), right mouse click on it, and choose “get
   info”. Choose the “open using Rosetta” tickbox. Install Rosetta when prompted if you do not have one.

   Restart Terminal.

   > You can . One running with Rosetta and the other to run without it.
   > To do so simply duplicate the Terminal application, and choose one of the terminal applications
   > to be under Rosetta and the other without it. Use the Rosetta terminal for the below installation steps.)

2. **Install homebrew** (if you already do not have one).
  
   In Terminal paste and execute:

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
   See https://brew.sh for details.
   
7. **Set up paths for homebrew and g++**. 

   Modify configuration file of your terminal shell (usually file `.zshrc` or <code>.bashrc</code>)
   by adding (change the first line if homebrew is installed to other location)

   ```bash
   eval "$(/opt/homebrew/bin/brew shellenv)"
   export CPLUS_INCLUDE_PATH="$CPLUS_INCLUDE_PATH:$HOMEBREW_PREFIX/include"
   export LIBRARY_PATH="$LIBRARY_PATH:$HOMEBREW_PREFIX/lib"
   ```

   Restart Terminal or execute `source .zshrc`

4. Install GNU tools and libraries, that CAPD depends on.
  
  * In Terminal execute the following command:

    ```bash
    brew install pkg-config make cmake boost git
    ```
   
   * To use multiple precision in CAPD execute
  
     ```bash
     brew install gmp mpfr
     ```
   
   * To generate documetnation one neeeds

     ```bash
     brew install doxygen
     ```

5. (*Optional/Experimental*) **Install GCC**
 
   OSX is using **clang** compiler (gcc and g++ are just symbolic links). We have not tested it for compatibility 
   with our code. You can compile the code, but we are not sure about compatibility with roundings etc. You can 
   experiment with original version of gcc/g++ which you can install using following commands:

   ```bash
   brew install gcc
   ```
   
4. **Download and compile source code of the library**

  * The most recent developed master branch can be cloned from the repository

    ```bash
    git clone https://github.com/CAPDGroup/CAPD
    cd CAPD
    mkdir build
    cd build
    cmake .. 
    make -j    
    ```

  * The latest stable relase can be also downloaded from

    [github.com/CAPDGroup/CAPD/releases](https://github.com/CAPDGroup/CAPD/releases)

