cmake_minimum_required(VERSION 3.18)
project(PySide6QCustomPlot2)

find_package(Python3 REQUIRED COMPONENTS Interpreter Development)
find_package(Qt6 REQUIRED COMPONENTS Core Widgets PrintSupport)
find_package(Shiboken6 QUIET)
find_package(PySide6 QUIET)

execute_process(
  COMMAND "${Python3_EXECUTABLE}" -c "import sysconfig; print(sysconfig.get_paths()['purelib'])"
  OUTPUT_VARIABLE SITE_PACKAGES_PATH
  OUTPUT_STRIP_TRAILING_WHITESPACE
)

message(STATUS "Found Python3:
	Executable: ${Python3_EXECUTABLE}
	Version: ${Python3_VERSION}
	site-packages Path: ${SITE_PACKAGES_PATH}")

execute_process(
  COMMAND cygpath.exe -w "$ENV{MINGW_PREFIX}"
  OUTPUT_VARIABLE MINGW_PREFIX
  OUTPUT_STRIP_TRAILING_WHITESPACE
  COMMAND_ERROR_IS_FATAL ANY
)

message(STATUS "MINGW_PREFIX: ${MINGW_PREFIX}")

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_PREFIX_PATH ${MINGW_PREFIX})
set(CMAKE_BUILD_TYPE Release)

qt_standard_project_setup()

set(SHIBOKEN_OUTPUT_FOLDER "${CMAKE_CURRENT_BINARY_DIR}/OUTPUTDIR")

# Do not use a GLOB here, to allow for usage as OUTPUT in custom command
set(SHIBOKEN_GENERATED_SOURCES
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/pyside6qcustomplot2_module_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/pyside6qcustomplot2_python.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcp_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcp_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpabstractplottable_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpabstractplottable_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxis_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxis_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxisrect_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxisrect_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxisticker_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxisticker_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpdataselection_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpdataselection_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpgraph_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpgraph_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpgraphdata_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpgraphdata_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpgrid_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpgrid_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayer_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayer_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayerable_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayerable_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayout_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayout_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayoutelement_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayoutelement_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayoutgrid_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayoutgrid_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplegend_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplegend_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplineending_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplineending_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcppainter_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcppainter_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpplottableinterface1d_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpplottableinterface1d_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcprange_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcprange_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpscatterstyle_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpscatterstyle_wrapper.h"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcustomplot_wrapper.cpp"
    "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcustomplot_wrapper.h"

     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpselectiondecorator_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpselectiondecorator_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickerlog_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickerlog_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpdatarange_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpdatarange_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpgraphdatacontainer_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpgraphdatacontainer_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpcurvedatacontainer_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpcurvedatacontainer_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpvector2d_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpvector2d_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpabstractitem_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpabstractitem_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpitemtracer_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpitemtracer_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpitemposition_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpitemposition_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpitemanchor_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpitemanchor_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxispainterprivate_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxispainterprivate_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpselectionrect_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpselectionrect_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpcurve_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpcurve_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpcurvedata_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpcurvedata_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpitemtext_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpitemtext_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpitemstraightline_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpitemstraightline_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickerdatetime_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickerdatetime_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpabstractlegenditem_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpabstractlegenditem_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpplottablelegenditem_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpplottablelegenditem_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qsharedpointer_qcpaxisticker_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qsharedpointer_qcpaxisticker_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qsharedpointer_qcpgraphdatacontainer_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qsharedpointer_qcpgraphdatacontainer_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qsharedpointer_qcpcurvedatacontainer_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qsharedpointer_qcpcurvedatacontainer_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/keyvalues_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/keyvalues_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayoutinset_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcplayoutinset_wrapper.h"

     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickertime_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickertime_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickertext_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickertext_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickerpi_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickerpi_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickerfixed_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpaxistickerfixed_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpabstractpaintbuffer_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpabstractpaintbuffer_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcppaintbufferpixmap_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcppaintbufferpixmap_wrapper.h"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpmargingroup_wrapper.cpp"
     "${SHIBOKEN_OUTPUT_FOLDER}/PySide6QCustomPlot2/qcpmargingroup_wrapper.h"
)

add_custom_command(
    COMMAND shiboken6
        --generator-set=shiboken
        --output-directory=OUTPUTDIR
		-I${MINGW_PREFIX}/include/qt6 -I${MINGW_PREFIX}/include/qt6/QtCore
		--typesystem-paths=${MINGW_PREFIX}/share/PySide6/typesystems
        --enable-pyside-extensions
        --avoid-protected-hack
        ${CMAKE_CURRENT_SOURCE_DIR}/src/wrapper.hpp
        ${CMAKE_CURRENT_SOURCE_DIR}/src/bindings.xml
    DEPENDS src/bindings.xml src/wrapper.hpp
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    OUTPUT ${SHIBOKEN_GENERATED_SOURCES}
    COMMENT "Running shiboken6 generator for src/bindings.xml"
)

add_custom_target(run_shiboken
    DEPENDS ${SHIBOKEN_GENERATED_SOURCES}
)

add_library(
    PySide6QCustomPlot2
    SHARED
    src/wrapper.hpp
    src/qcustomplot.cpp
    src/qcustomplot.h
    ${SHIBOKEN_GENERATED_SOURCES}
)

# A bit ugly:
# - include paths to python installation
# - include paths to pyside and shiboken6_generator in .venv
target_include_directories(
    PySide6QCustomPlot2
    PRIVATE
    "src"
	"${MINGW_PREFIX}/include"
	${Python3_INCLUDE_DIRS}
	"${MINGW_PREFIX}/include/PySide6"
	"${MINGW_PREFIX}/include/PySide6/QtWidgets"
	"${MINGW_PREFIX}/include/PySide6/QtGui"
	"${MINGW_PREFIX}/include/PySide6/QtCore"
	"${MINGW_PREFIX}/include/PySide6/QtPrintSupport"
	"${MINGW_PREFIX}/include/shiboken6"
)

# Use the python stable ABI3:
# See also https://docs.python.org/3/c-api/stable.html
target_compile_definitions(
    PySide6QCustomPlot2
    PRIVATE
)

set_target_properties(
    PySide6QCustomPlot2
    PROPERTIES
    SUFFIX ".pyd"
	PREFIX ""
)

target_link_directories(
    PySide6QCustomPlot2
    PRIVATE
	"${MINGW_PREFIX}/lib"
	${SITE_PACKAGES_PATH}/shiboken6
	${SITE_PACKAGES_PATH}/PySide6
)

target_link_libraries(
    PySide6QCustomPlot2
    PRIVATE
    Qt6::Widgets
    Qt6::Core
    Qt6::PrintSupport
	Python3::Python
)

if(TARGET Shiboken6::libshiboken)
  target_link_libraries(PySide6QCustomPlot2 PRIVATE Shiboken6::libshiboken)
endif()

if(TARGET PySide6::pyside6)
  target_link_libraries(PySide6QCustomPlot2 PRIVATE PySide6::pyside6)
endif()

install(
    TARGETS PySide6QCustomPlot2
    DESTINATION ${PY_BUILD_CMAKE_MODULE_NAME}
)
