cmake_minimum_required(VERSION 3.10)
project(First LANGUAGES CXX)

find_package(OpenVDB CONFIG REQUIRED)
find_package(VTK REQUIRED)

add_executable(First main.cpp)

if(MSVC)
  target_compile_options(First PRIVATE /bigobj)
endif()

target_include_directories(First PRIVATE ${OPENVDB_INCLUDE_DIRS})
target_include_directories(First PRIVATE ${VTK_INCLUDE_DIRS})

target_link_libraries(First PRIVATE OpenVDB::openvdb)
target_link_libraries(First PRIVATE ${VTK_LIBRARIES})

vtk_module_autoinit(
    TARGETS First
    MODULES ${VTK_LIBRARIES}
)