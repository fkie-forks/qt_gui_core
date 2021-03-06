set(Python_ADDITIONAL_VERSIONS "${PYTHON_VERSION_MAJOR}.${PYTHON_VERSION_MINOR}")
find_package(PythonLibs "${PYTHON_VERSION_MAJOR}.${PYTHON_VERSION_MINOR}" REQUIRED)
find_package(Qt5Widgets REQUIRED)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")

set(qt_gui_cpp_SRCS
  composite_plugin_provider.cpp
  generic_proxy.cpp
  plugin_bridge.cpp
  plugin_context.cpp
  plugin_descriptor.cpp
  plugin_provider.cpp
  recursive_plugin_provider.cpp
  settings.cpp
)

set(qt_gui_cpp_HDRS
  ../../include/qt_gui_cpp/plugin.h
  ../../include/qt_gui_cpp/plugin_bridge.h
  ../../include/qt_gui_cpp/plugin_context.h
)

set(qt_gui_cpp_INCLUDE_DIRECTORIES
  ${PYTHON_INCLUDE_DIR}
  ${PROJECT_SOURCE_DIR}/include/qt_gui_cpp
  ${PROJECT_SOURCE_DIR}/src/qt_gui_cpp
)

set(qt_gui_cpp_LINK_LIBRARIES
  ${QT_QTCORE_LIBRARY}
  ${QT_QTGUI_LIBRARY}
)

qt5_wrap_cpp(qt_gui_cpp_MOCS ${qt_gui_cpp_HDRS})

include_directories(${PROJECT_NAME} ${qt_gui_cpp_INCLUDE_DIRECTORIES})
add_library(${PROJECT_NAME} ${qt_gui_cpp_SRCS} ${qt_gui_cpp_MOCS})
target_link_libraries(${PROJECT_NAME} ${qt_gui_cpp_LINK_LIBRARIES} ${catkin_LIBRARIES} ${Boost_LIBRARIES} Qt5::Widgets)

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
