# Basic instructions to set up JUCE in Linux(PopOS)
- This repo is a test project using an example from JUCE Projucer to install JUCE in Linux and to create a simple sinewave synthesizer.

The idea is to 
- Build the Projucer app.
- Run Projucer app.
- Make a new project and save it.
- In vscode open the project folder and add the two json files
- First build the demo and then run it.
---

### **Step 1: Install Necessary Tools**

1. **JUCE Framework**  
   - Download JUCE from the [official website](https://juce.com/get-juce).
   - Extract the files into a directory on your system (e.g., `~/JUCE`).

2. **Install C++ Compiler**  
   - Linux: Install GCC or Clang and other dependencies. Run:  
     ```bash
     sudo apt update
     sudo apt install build-essential cmake git -y
     sudo apt install clang
     sudo apt install libx11-dev libxcomposite-dev libxcursor-dev libxext-dev libxinerama-dev libxrandr-dev libasound2-dev libfreetype6-dev libcurl4-openssl-dev -y

     ```


2. **Install VSCode Extensions**  
   - Search for and install the following extensions:
     - **C++**
     - **CMake Tools**

---

### **Step 2: Build and Open Projucer**


1. **Build Projucer**  
   Navigate to the JUCE folder and build Projucer:
   ```bash
   cd ~/JUCE/extras/Projucer/Builds/LinuxMakefile
   make
   ```
   This creates an executable in `~/JUCE/extras/Projucer/Builds/LinuxMakefile/build/`.

2. **Open Projucer**  
   Run Projucer:
   ```bash
   ./build/Projucer
   ```

---

### **Step 3: Create a New Project with Projucer**

1. **Create New Project**  
   - In Projucer, click **File > New Project**.
   - Select **Audio Application** (this template supports synthesizers).
   - Choose a project folder and name it (e.g., `SynthProject`).
   - Save the project.

2. **Configure Exporters**  
   - In Projucer, go to **Exporters** and add the exporter for your platform:
     - Linux: Code::Blocks (or Makefile).
   - Configure paths:
     - JUCE Modules Path: Point this to `~/JUCE/modules`.

3. **Save and Export**  
   - Save the project.  
   - Close Projucer; the `.jucer` file you created will manage the project.

---

### **Step 4: Open the Project in VSCode**

1. **Open Folder**  
   - Open VSCode.
   - Click **File > Open Folder**, and select your project folder.

2. **Setup Include Paths**  
   - Open `c_cpp_properties.json` in `.vscode` (create it if it doesn’t exist).  
   - Add paths to the JUCE modules:
     ```json
     {"configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "/usr/include",
                "/usr/local/include",
                "~/projects/JUCE/modules"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/gcc",
            "cStandard": "c11",
            "cppStandard": "c++17",
            "intelliSenseMode": "linux-gcc-x64"
        }],"version": 4}
        ```


3. **Configure Build Tasks**  
   - In `.vscode/tasks.json`, add:
     ```json
     {
       "version": "2.0.0",
       "tasks": [
         {
           "label": "Build SynthProject",
           "type": "shell",
           "command": "make",
           "group": {
             "kind": "build",
             "isDefault": true
           },
           "problemMatcher": []
         }
       ]
     }
     ```

4. **Run CMake Tools**  
   - In VSCode, go to **CMake Tools > Configure**.  
   - Ensure `build/` is selected as the build folder.

---


**Compile the demo project and Run**  
   - Run the `make` command in the terminal inside the LinuxMakefile:
     ```bash
     make
     ```
-  Next  in the same location run the app in terminal
    ```bash
    ./build/AudioSynthesiserDemo 
    ```

    The app will start in a new window .


    * More info will be added soon.


#### Also the project must have a gitignore file
That means no `.vscode` and `/build` folders. In order to run the project as mentioned above you must add the `.jucer` file to Projucer and save it in order to rebuild the `/build` folder and then do the other steps such as configure vscode and build and run it again.
