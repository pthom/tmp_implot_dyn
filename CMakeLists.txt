project(imgui_implot_dyn)
cmake_minimum_required(VERSION 3.0)

find_package(OpenGL REQUIRED)

set(CMAKE_CXX_STANDARD 17)
set(BUILD_SHARED_LIBS ON)

add_subdirectory(external/glfw)

set(imgui_sources 
    external/imgui/imconfig.h
    external/imgui/imgui.cpp
    external/imgui/imgui.h
    external/imgui/imgui_demo.cpp
    external/imgui/imgui_draw.cpp
    external/imgui/imgui_internal.h
    external/imgui/imgui_tables.cpp
    external/imgui/imgui_widgets.cpp
    external/imgui/imstb_rectpack.h
    external/imgui/imstb_textedit.h
    external/imgui/imstb_truetype.h
    external/imgui/backends/imgui_impl_glfw.cpp
    external/imgui/backends/imgui_impl_glfw.h
    external/imgui/backends/imgui_impl_opengl3.cpp
    external/imgui/backends/imgui_impl_opengl3.h
    )
add_library(imgui ${imgui_sources})
target_include_directories(imgui PUBLIC external/imgui external/imgui/backends)
target_link_libraries(imgui PUBLIC glfw OpenGL::GL)

set(implot_sources 
    external/implot/implot.cpp
    external/implot/implot.h
    external/implot/implot_demo.cpp
    external/implot/implot_internal.h
    external/implot/implot_items.cpp
    )
add_library(implot ${implot_sources})
target_include_directories(implot PUBLIC external/implot)
target_link_libraries(implot PUBLIC imgui)

add_executable(sample_implot_imgui sample_implot_imgui.cpp)
target_link_libraries(sample_implot_imgui PRIVATE imgui implot)

