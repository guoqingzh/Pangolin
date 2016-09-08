# Find Pangolin (https://github.com/stevenlovegrove/Pangolin)
<<<<<<< HEAD
include_directories(${PANGOLIN_INCLUDE_DIRS})

add_executable(SimpleDisplay main.cpp)
target_link_libraries(SimpleDisplay ${PANGOLIN_LIBRARIES})
=======
find_package(Pangolin 0.4 REQUIRED)
include_directories(${Pangolin_INCLUDE_DIRS})

add_executable(SimpleDisplay main.cpp)
target_link_libraries(SimpleDisplay ${Pangolin_LIBRARIES} )

>>>>>>> stevenlovegrove/master
