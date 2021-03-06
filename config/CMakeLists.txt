project(lxqt-config-powermanagement)

set(QTX_LIBRARIES Qt5::Widgets Qt5::DBus)

set(config-powermanagement_MOCS
    mainwindow.h
    lidwatchersettings.h
    batterywatchersettings.h
    idlenesswatchersettings.h
    powermanagementsettings.h
)

set(config-powermanagement_SRCS
    main.cpp
    mainwindow.cpp
    lidwatchersettings.cpp
    batterywatchersettings.cpp
    idlenesswatchersettings.cpp
    powermanagementsettings.cpp
    helpers.cpp
)

set(config-powermanagement_UIS
    lidwatchersettings.ui
    batterywatchersettings.ui
    idlenesswatchersettings.ui
)

set(config-powermanagement_RSCS
    config-powermanagement.qrc
)

set(ICON_FILES
    icons/laptop-lid.svg
)

set(DESKTOP_FILES_IN
    lxqt-config-powermanagement.desktop.in
)

# Translations
include(LxQtTranslate)
lxqt_translate_desktop(DESKTOP_FILES SOURCES ${DESKTOP_FILES_IN})


qt5_add_resources(RSCS ${config-powermanagement_RSCS})
qt5_wrap_ui(UIS ${config-powermanagement_UIS})

add_executable(${PROJECT_NAME}
    ${config-powermanagement_SRCS}
    ${UIS}
    ${DESKTOP_FILES}
    ${QM_FILES}
)

target_link_libraries(lxqt-config-powermanagement
    ${LXQT_LIBRARIES}
    ${QTXDG_LIBRARIES}
    ${QTX_LIBRARIES}
)

install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION bin)
install(FILES ${DESKTOP_FILES} DESTINATION share/applications)
install(FILES ${ICON_FILES} DESTINATION share/icons/hicolor/scalable/devices)
