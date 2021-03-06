set(cocoa_SOURCES
    CocoaAppDelegate.h
    CocoaAppDelegate.mm
    English.lproj
    Info.plist
    main.mm
    views

    # These need to be included so they can be copied to the bundle
    ${axr_icon_SOURCES}
    ${hss_SOURCES}
)

source_group(Resources FILES English.lproj views)
source_group("Resources\\HSS Framework" FILES ${hss_SOURCES})

if(APPLE)
    qt_transform_sources(cocoa_SOURCES "${cocoa_SOURCES}")

    add_executable("${TARGET_NAME_APP_COCOA}" MACOSX_BUNDLE ${cocoa_SOURCES})
    target_link_libraries("${TARGET_NAME_APP_COCOA}" "${TARGET_NAME_LIB_COCOA}")

    set(MACOSX_BUNDLE_ICON_FILE prototype.icns)

    set_source_files_properties(${axr_icon_SOURCES} PROPERTIES MACOSX_PACKAGE_LOCATION Resources)
    set_source_files_properties(English.lproj PROPERTIES MACOSX_PACKAGE_LOCATION Resources)
    set_source_files_properties(${hss_SOURCES} PROPERTIES MACOSX_PACKAGE_LOCATION Resources/framework)
    set_source_files_properties(views PROPERTIES MACOSX_PACKAGE_LOCATION Resources)

    set(TARGET_NAME_APP_COCOA_OUTPUT_NAME "Cocoa Example")

    set_target_properties("${TARGET_NAME_APP_COCOA}" PROPERTIES
        MACOSX_BUNDLE_INFO_PLIST ${CMAKE_CURRENT_SOURCE_DIR}/Info.plist
        OUTPUT_NAME "${TARGET_NAME_APP_COCOA_OUTPUT_NAME}"
        FOLDER Examples
    )

    install(TARGETS "${TARGET_NAME_APP_COCOA}"
        BUNDLE DESTINATION Examples COMPONENT examples
        RUNTIME DESTINATION ${CMAKE_RUNTIME_OUTPUT_DIRECTORY_REL}/examples COMPONENT examples
    )

    if(APPLE)
        set(app_path Examples)
    else()
        set(app_path ${CMAKE_RUNTIME_OUTPUT_DIRECTORY_REL}/examples)
    endif()

    install_qt4_executable("${app_path}/${TARGET_NAME_APP_COCOA_OUTPUT_NAME}${CMAKE_USER_EXECUTABLE_SUFFIX}" "qtaccessiblewidgets qcncodecs qjpcodecs qkrcodecs qtwcodecs qsvgicon qgif qico qjpeg qmng qsvg qtiff" "" "${ALL_LIBRARY_DIRS}" "" "" examples)
    empty_lproj(${app_path}/${TARGET_NAME_APP_COCOA_OUTPUT_NAME})
else()
    add_custom_target("${TARGET_NAME_APP_COCOA}" SOURCES ${cocoa_SOURCES})
endif()
