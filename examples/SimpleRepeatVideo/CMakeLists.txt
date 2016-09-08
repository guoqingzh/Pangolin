# Find Pangolin (https://github.com/stevenlovegrove/Pangolin)
<<<<<<< HEAD
include_directories(${PANGOLIN_INCLUDE_DIRS})
=======
find_package(Pangolin 0.4 REQUIRED)
include_directories(${Pangolin_INCLUDE_DIRS})
>>>>>>> stevenlovegrove/master

add_executable(SimpleRepeatVideo main.cpp)
target_link_libraries(SimpleRepeatVideo ${PANGOLIN_LIBRARIES})
