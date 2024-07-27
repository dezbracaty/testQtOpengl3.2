cmake_minimum_required(VERSION 3.15)
project(multiThreadQmlRenderer)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

find_package(Qt6 COMPONENTS Core Gui Widgets OpenGL Quick REQUIRED)

# file(GLOB_RECURSE SOURCES *.cpp *.h *.qrc ./shared/*.cpp ../shared/*.h *.qrc)
# 添加资源文件
set(RESOURCE_FILES src/resource/multiThreadQmlRenderer.qrc)
qt_add_resources(RCC_SOURCES ${RESOURCE_FILES})

# add_executable(multiThreadQmlRenderer ${SOURCES})
qt_wrap_cpp(MOC_SOURCES src/threadrenderer.h)
add_executable(multiThreadQmlRenderer
    src/main.cpp
    src/threadrenderer.cpp 
    src/threadrenderer.h 
    src/shared/logorenderer.h 
    src/shared/logorenderer.cpp
    # multiThreadQmlRenderer.qrc
    ${RCC_SOURCES}
)
target_sources(multiThreadQmlRenderer PRIVATE ${MOC_SOURCES})

target_link_libraries(multiThreadQmlRenderer
    Qt6::Core
    Qt6::Gui
    Qt6::Widgets
    Qt6::OpenGL
    Qt6::Quick
)