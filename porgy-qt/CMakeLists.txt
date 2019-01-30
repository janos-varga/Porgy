INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/include ${TULIP_INCLUDE_DIR} ${CMAKE_CURRENT_BINARY_DIR} ${PORTGRAPH_INCLUDE_DIR})

IF(WIN32)
   SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DDLL_PORGY")
ENDIF(WIN32)

SET(LIB_SRCS
    elementinformationinteractorcomponent.cpp
    GraphElementValueModel.cpp
    graphsnapshotmanager.cpp
    GraphVisualProperties.cpp
    MetaNodeZoomInteractorComponent.cpp
    ModelElementValueModel.cpp
    pluginparametersconfigurationdialog.cpp
    pluginselectionwizard.cpp
    porgymimedata.cpp
    porgypersistentsettings.cpp
    porgysettings.cpp
    PortNodeQt.cpp
    PortNodeQtModel.cpp
    PortQt.cpp
    PropertyValueToQVariantConverter.cpp
    PropertyValueToQVariantManager.cpp
    RuleElementValueModel.cpp
    SelectPortNodeInteractorComponent.cpp
    Strategy.cpp
    TraceElementValueModel.cpp
    porgyitemdelegate.cpp)

SET(LIB_UI
    designer/pluginparametersconfigurationdialog.ui
    designer/pluginselectionwizard.ui)

SET(LIB_MOC
    include/porgy/graphsnapshotmanager.h
    include/porgy/pluginparametersconfigurationdialog.h
    include/porgy/pluginselectionwizard.h
    include/porgy/porgypersistentsettings.h
    include/porgy/porgysettings.h)

#FILE(GLOB LIB_RCC "designer/*.qrc")

QTX_WRAP_UI(LIB_UI_SRCS ${LIB_UI})
QTX_WRAP_CPP(LIB_MOC_SRCS ${LIB_MOC})
#QTX_ADD_RESOURCES(LIB_RCC_SRCS ${LIB_RCC})

ADD_LIBRARY(${PORGY_LIB} SHARED ${LIB_SRCS} ${LIB_UI_SRCS} ${LIB_MOC_SRCS}  )
TARGET_LINK_LIBRARIES(${PORGY_LIB} ${PORTGRAPH_LIBS} ${QT_LIBRARIES})
INSTALL(TARGETS ${PORGY_LIB}
  RUNTIME DESTINATION ${TULIP_LIBRARIES_DIR} COMPONENT PorgyLib
  LIBRARY DESTINATION ${TULIP_LIBRARIES_DIR} COMPONENT PorgyLib
  ARCHIVE DESTINATION ${TULIP_LIBRARIES_DIR} COMPONENT PorgyLib)