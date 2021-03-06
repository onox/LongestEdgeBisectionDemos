cmake_minimum_required (VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug)
endif()

if(CMAKE_COMPILER_IS_GNUCC OR CMAKE_COMPILER_IS_GNUCXX)
  # Update if necessary
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall  -Wextra")
  set(CMAKE_CXX_FLAGS_DEBUG "-g")
endif()

set(CMAKE_CXX_FLAGS_RELEASE "-O3")

# disable GLFW docs, examples and tests
# see http://www.glfw.org/docs/latest/build_guide.html
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

# set path to dependencies
add_subdirectory(submodules/glfw)
include_directories(submodules/glfw/include)
include_directories(submodules/imgui)
include_directories(submodules/stb)
include_directories(submodules/dj_opengl)
include_directories(submodules/dj_algebra)
include_directories(submodules/LongestEdgeBisection)
# imgui source files
set(IMGUI_SRC_DIR submodules/imgui)
aux_source_directory(${IMGUI_SRC_DIR} IMGUI_SRC_FILES)

project (LongestEdgeBisectionDemos)

# ------------------------------------------------------------------------------
set(DEMO ApiDebug)
set(SRC_DIR ApiDebug)
include_directories(${SRC_DIR})
aux_source_directory(${SRC_DIR} SRC_FILES)
add_executable(${DEMO} ${IMGUI_SRC_FILES} ${SRC_FILES} ${SRC_DIR}/glad/glad.c)
target_link_libraries(${DEMO} glfw)
target_compile_definitions(
    ${DEMO} PUBLIC
    -DPATH_TO_SRC_DIRECTORY="${CMAKE_SOURCE_DIR}/${SRC_DIR}/"
    -DPATH_TO_ASSET_DIRECTORY="${CMAKE_SOURCE_DIR}/assets/"
    -DPATH_TO_LEB_GLSL_LIBRARY="${CMAKE_SOURCE_DIR}/submodules/LongestEdgeBisection/GLSL/"
)
unset(SRC_FILES)
unset(DEMO)

# ------------------------------------------------------------------------------
set(DEMO Terrain)
set(SRC_DIR Terrain)
include_directories(${SRC_DIR})
aux_source_directory(${SRC_DIR} SRC_FILES)
add_executable(${DEMO} ${IMGUI_SRC_FILES} ${SRC_FILES} ${SRC_DIR}/glad/glad.c)
target_link_libraries(${DEMO} glfw)
target_compile_definitions(
    ${DEMO} PUBLIC
    -DPATH_TO_SRC_DIRECTORY="${CMAKE_SOURCE_DIR}/${SRC_DIR}/"
    -DPATH_TO_ASSET_DIRECTORY="${CMAKE_SOURCE_DIR}/assets/"
    -DPATH_TO_LEB_GLSL_LIBRARY="${CMAKE_SOURCE_DIR}/submodules/LongestEdgeBisection/GLSL/"
)
unset(SRC_FILES)
unset(DEMO)


