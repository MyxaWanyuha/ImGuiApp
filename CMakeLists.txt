cmake_minimum_required(VERSION 3.10)
project(ImGuiApp)

add_subdirectory(glfw)

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

add_executable(${PROJECT_NAME} main.cpp user.cpp user.hpp)

set(IMGUI_SRC
    imgui/imgui.cpp
    imgui/imgui_draw.cpp
    imgui/imgui_widgets.cpp
    imgui/imgui_tables.cpp
    imgui/imgui_demo.cpp
    imgui/backends/imgui_impl_glfw.cpp
    imgui/backends/imgui_impl_opengl3.cpp
)

add_library(imgui STATIC ${IMGUI_SRC})

include_directories(imgui imgui/backends glfw/include)

if(WIN32)
target_link_libraries(${PROJECT_NAME} imgui glfw opengl32)
else()
target_link_libraries(${PROJECT_NAME} imgui glfw GL)
endif()