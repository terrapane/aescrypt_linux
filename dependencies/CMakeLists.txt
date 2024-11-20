# Enable fetching content
include(FetchContent)

# Set the root of the Terrapane source repositories
if(DEFINED ENV{TERRAPANE_SOURCE_URI})
    set(TERRAPANE_SOURCE_URI "$ENV{TERRAPANE_SOURCE_URI}")
else()
    set(TERRAPANE_SOURCE_URI "https://github.com/terrapane")
endif()

# Fetch the AES Crypt CLI Project
FetchContent_Declare(aescrypt_cli
    GIT_REPOSITORY ${TERRAPANE_SOURCE_URI}/aescrypt_cli.git
    GIT_TAG        v4.1.0
    GIT_SHALLOW    true)

# Enable CLI tests if GUI tests are enabled
if(aescrypt_gui_BUILD_TESTS)
    set(aescrypt_cli_BUILD_TESTS ON)
endif()

# Make dependencies available
FetchContent_MakeAvailable(aescrypt_cli)
