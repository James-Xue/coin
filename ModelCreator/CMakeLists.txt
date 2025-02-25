# Set module name
set(MODULE_NAME ModelCreator)

# Add source files
set(${MODULE_NAME}_SRCS
    MainGui.cpp
    MainGui.h
)

# Add executable or library
add_executable(
    ${MODULE_NAME}
    ${${MODULE_NAME}_SRCS}
)

# Link dependencies (if any)
target_link_libraries(
    ${MODULE_NAME}
    Coin
    ${COIN_TARGET_LINK_LIBRARIES}
)

# Set include directories (if any)
target_include_directories(
    ${MODULE_NAME} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_SOURCE_DIR}/include
    ${CMAKE_SOURCE_DIR}/include/Inventor/annex
    ${CMAKE_BINARY_DIR}/include
    ${COIN_TARGET_INCLUDE_DIRECTORIES}
)

# Set compile options
# Add the highest standard warning level option for MSVC
if (CMAKE_CXX_COMPILER_ID MATCHES "GNU" OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    target_compile_options(
        CoinTests PRIVATE
        -Wall         # Add the highest standard warning level option
        -Wextra       # Enable additional compiler warnings
        -Wpedantic    # Enable warnings for strict adherence to standard C++
        -Werror       # Treat all warnings as errors
    )
    target_compile_options(
        ${MODULE_NAME} PRIVATE
        -Wall         # Add the highest standard warning level option
        -Wextra       # Enable additional compiler warnings
        -Wpedantic    # Enable warnings for strict adherence to standard C++
        -Werror       # Treat all warnings as errors
    )
elseif (CMAKE_CXX_COMPILER_ID MATCHES "MSVC")
    target_compile_options(
        ${MODULE_NAME} PRIVATE
         # /W4 # Maximum warning level for MSVC
         /Wall # Enable all warnings
    )
    target_compile_options(
        CoinTests PRIVATE
         # /W4 # Maximum warning level for MSVC
         /Wall # Enable all warnings
    )
endif()
