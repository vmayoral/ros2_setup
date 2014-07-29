ROS 2.0 Setup
==========

The following instructions describe how to setup the environment to start working with ROS 2.0.

###Debian dependencies:
* Python 3
* `libopensplice63` from packages.osrfoundation.org

###Creating the virtual environment and setting it up:
For creating the python virtual environment:
```bash
virtualenv --python /usr/bin/python3 python3_venv
source python3_venv/bin/activate
```

Install empy:
```bash
pip3 install empy
```

Fetch and install some packages:
```bash
git clone https://github.com/ament/ament_package
cd ament_package
python3 setup.py install
git clone https://github.com/ament/ament_tools
cd ament_tools
git checkout simple
python3 setup.py install
```

Packages should be deployed in your virtual environment.

###Workspace setup
```bash
mkdir ros2_workspace
git clone https://github.com/ament/ament_cmake
git clone https://github.com/ament/ament_lint
git clone https://github.com/ros2/rosidl
git clone https://github.com/dirk-thomas/ament_examples
git clone https://github.com/dirk-thomas/rosidl_examples
git clone https://github.com/dirk-thomas/ros2_examples
```

###Invoke `amend build`

---

Before invoking `amend build` (and temporarily) the following fix should be applied:

```bash
(python3_venv)victor@frcsim:~/Dropbox/OSRF/ros2_worspace/ament_cmake$ git diff
diff --git a/ament_cmake_environment/ament_cmake_environment-extras.cmake b/ament_cmake_environment/ament_cmake_environment-extras.cmake
index ba194e0..e2733b5 100644
--- a/ament_cmake_environment/ament_cmake_environment-extras.cmake
+++ b/ament_cmake_environment/ament_cmake_environment-extras.cmake
@@ -1,7 +1,7 @@
 # copied from ament_cmake_environment/ament_cmake_environment-extras.cmake
 
 option(AMENT_CMAKE_ENVIRONMENT_GENERATION
-  "Generate environment files in the CMAKE_INSTALL_PREFIX" OFF)
+  "Generate environment files in the CMAKE_INSTALL_PREFIX" ON)
 option(AMENT_CMAKE_ENVIRONMENT_PARENT_PREFIX_PATH_GENERATION
   "Generate marker file containing the parent prefix path" ON)
 

```

---
Setup the DDS vendor:

```bash
export ROS_DDS_IMPLEMENTATION="opensplice"
```

Invoke `amend build`. The process will begin and the output goes to "/tmp/ament_build_pkg/install".

---

At the time of writing the package `ros2_examples/foo` doesn't compile. In order to procees a file called `ros2_examples/foo/AMENT_IGNORE` can be created.

---

After sourcing the `setup.bash` (should be located now at `/tmp/ament_build_pkg/install`) file you should have an extended PATH,
PYTHONPATH etc. and the OSPL environment variable.
