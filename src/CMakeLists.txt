set(LIB fortran_tester)
add_library(${LIB} tester.f90)
add_library(${NAMESPACE}${LIB} ALIAS ${LIB})

target_include_directories(${LIB}
    INTERFACE
        $<BUILD_INTERFACE:${CMAKE_Fortran_MODULE_DIRECTORY}>
)

# installation and export of targets
include(GNUInstallDirs)

install(DIRECTORY ${CMAKE_Fortran_MODULE_DIRECTORY}/
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME}
    COMPONENT Developement
)

install(TARGETS ${LIB} EXPORT ${TARGETS_EXPORT_NAME}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} COMPONENT Development
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} COMPONENT RuntimeLibraries
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} COMPONENT RuntimeLibraries
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME}
)
