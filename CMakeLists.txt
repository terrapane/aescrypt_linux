cmake_minimum_required(VERSION 3.21)

# Define the AES Crypt GUI project
project(aescrypt_linux
        VERSION 4.0.3.0
        DESCRIPTION "AES Crypt Graphical User Interface (GUI) for Linux"
        HOMEPAGE_URL "https://www.aescrypt.com")

set(COPYRIGHT_TEXT  "Copyright (C) 2024")
set(AUTHOR_TEXT     "Terrapane Corporation")

# Option to control ability to install the program
option(aescrypt_linux_INSTALL "Install the AES Crypt Linux GUI Program" ON)

add_subdirectory(dependencies)
add_subdirectory(src)

# Include packaging only if this is the top-level project
if(PROJECT_IS_TOP_LEVEL)
    add_subdirectory(packaging)
endif()
