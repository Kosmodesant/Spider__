﻿cmake_minimum_required(VERSION 3.19)
project(Diplom VERSION 1.0 LANGUAGES CXX)

set(LIBPQ_ROOT "C:/Users/Robot/Desktop/dev/C++/Diplom_/libpqxx-master")      # Укажите путь к libpq++
SET(CMAKE_INCLUDE_PATH ${CMAKE_INCLUDE_PATH} "C:/Users/Robot/Desktop/dev/C++/Diplom_")
# Boost:
# Компоновщик: доп. каталоги библиотек
link_directories("C:/Users/Robot/Desktop/dev/C++/Diplom_/boost_1_80_0/libs")
find_package(Boost 1.80.0 REQUIRED)
if(NOT Boost_FOUND)
	message(FATAL_ERROR "Could not find Boost")
endif()

# OpenSSL
find_package(OpenSSL REQUIRED)

add_compile_definitions(_WIN32_WINNT=0x0601) # минимальная версия ОС win-7
#add_compile_definitions(_WIN32_WINNT=0x0A01) # минимальная версия ОС win-10
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /std:c++17")
add_compile_options("$<$<C_COMPILER_ID:MSVC>:/utf-8>")
add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>")

# PQXX
#set(PostgreSQL_ADDITIONAL_VERSIONS "15")
set(SKIP_BUILD_TEST ON)
add_subdirectory(${LIBPQ_ROOT} build-pqxx)

add_subdirectory(Spider)
add_subdirectory(Server)