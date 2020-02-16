cmake_minimum_required(VERSION 3.10)

set(CMAKE_C_STANDARD 11)

# adding pre-compiled static library
message(STATUS "Library ligeasylogs located in: ${CMAKE_SOURCE_DIR}/Libraries/libeasylogs.a")
add_library(libeasylogs STATIC IMPORTED)
set_property(TARGET libeasylogs PROPERTY IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/Libraries/libeasylogs.a)
include_directories(${CMAKE_SOURCE_DIR}/Headers)

set(SOURCES Sources/main.c Headers/chess.h)

set(C_FILES ${SOURCES} Headers/easylogs.h) # well im gonna leave it there
message(STATUS "Creating sources from: ${C_FILES}")
add_executable(chessplate ${C_FILES})

if (UNIX)
    set(LIBS libeasylogs ncurses)
    target_compile_options(chessplate PRIVATE -Wall -Wextra -g -O0)
    target_link_libraries(chessplate ${LIBS})
endif (UNIX)
