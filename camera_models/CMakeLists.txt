cmake_minimum_required(VERSION 3.0.0)
project(camera_models)

set(CMAKE_BUILD_TYPE "Release")
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -fPIC")

find_package(catkin REQUIRED COMPONENTS
    roscpp
    std_msgs
)

find_package(Boost REQUIRED COMPONENTS filesystem program_options system)
include_directories(${Boost_INCLUDE_DIRS})


#SET("OpenCV_DIR"  "/usr/local/share/OpenCV/")
#SET("OpenCV_DIR" "/home/pi/source/opencv-3.4.10/release/share/OpenCV")
SET("OpenCV_DIR"  "/usr/local/share/OpenCV/")
find_package(OpenCV REQUIRED)

# set(EIGEN_INCLUDE_DIR "/usr/local/include/eigen3")
find_package(Ceres REQUIRED)
include_directories(${CERES_INCLUDE_DIRS})


catkin_package(
    INCLUDE_DIRS include
    LIBRARIES camera_models
    CATKIN_DEPENDS roscpp std_msgs
#    DEPENDS system_lib
)

include_directories(
    ${catkin_INCLUDE_DIRS}
)

include_directories("include")

# add_executable(Calibrations
#     src/intrinsic_calib.cc
#     src/chessboard/Chessboard.cc
#     src/calib/CameraCalibration.cc
#     src/camera_models/Camera.cc
#     src/camera_models/CameraFactory.cc
#     src/camera_models/CostFunctionFactory.cc
#     src/camera_models/PinholeCamera.cc
#     src/camera_models/PinholeFullCamera.cc
#     src/camera_models/CataCamera.cc
#     src/camera_models/EquidistantCamera.cc
#     src/camera_models/ScaramuzzaCamera.cc
#     src/camera_models/PolyFisheyeCamera.cc
#     src/sparse_graph/Transform.cc
#     src/code_utils/math_utils/Polynomial.cpp
#     src/gpl/gpl.cc
#     src/gpl/EigenQuaternionParameterization.cc)

add_library(camera_models
    #src/calib/CameraCalibration.cc
    src/camera_models/Camera.cc
    src/camera_models/CameraFactory.cc
    #src/camera_models/CostFunctionFactory.cc
    src/camera_models/PinholeCamera.cc
    src/camera_models/PinholeFullCamera.cc
    src/camera_models/CataCamera.cc
    src/camera_models/EquidistantCamera.cc
    src/camera_models/ScaramuzzaCamera.cc
    src/camera_models/PolyFisheyeCamera.cc
    src/camera_models/CylindricalCamera.cc
    #src/sparse_graph/Transform.cc
    src/gpl/gpl.cc
    src/code_utils/math_utils/Polynomial.cpp
    #src/gpl/EigenQuaternionParameterization.cc
    )

#target_link_libraries(Calibrations ${Boost_LIBRARIES} ${OpenCV_LIBS} ${CERES_LIBRARIES})
target_link_libraries(camera_models ${Boost_LIBRARIES} ${OpenCV_LIBS} ${CERES_LIBRARIES})
