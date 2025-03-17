# Depending on the platform, the aescrypt binary is expected to be in /usr/bin
# or /usr/local/bin; set the aescrypt.desktop file accordingly
if(BSD)
    set(INSTALL_PATH "/usr/local")
else()
    set(INSTALL_PATH "/usr")
endif()

# Create the aescrypt.desktop file with expected install paths
configure_file(aescrypt.desktop.in aescrypt.desktop @ONLY)

if(aescrypt_linux_INSTALL AND (LINUX OR BSD))
    include(GNUInstallDirs)
    install(PROGRAMS aescrypt-gui DESTINATION ${CMAKE_INSTALL_BINDIR})
    install(FILES ${CMAKE_CURRENT_BINARY_DIR}/aescrypt.desktop DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/applications/)
    install(FILES aescrypt.svg DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/icons/hicolor/scalable/apps/)
    install(FILES aescrypt_paper.png DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/icons/hicolor/256x256/apps/)
    install(FILES aescrypt.xml DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/mime/packages/)
endif()
