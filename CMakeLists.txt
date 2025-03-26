cmake_minimum_required(VERSION 3.25 FATAL_ERROR)

project(mp_os LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Установка путей vcpkg
set(VCPKG_ROOT "/Users/vladimirbugrenkov/.vcpkg-clion/vcpkg")
set(VCPKG_INCLUDE_DIR "${VCPKG_ROOT}/installed/arm64-osx/include")
set(CMAKE_TOOLCHAIN_FILE "${VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake")



message(STATUS "=== Начало конфигурации ===")
message(STATUS "VCPKG root: ${VCPKG_ROOT}")
message(STATUS "VCPKG include dir: ${VCPKG_INCLUDE_DIR}")
find_package(Boost CONFIG REQUIRED COMPONENTS system container)
find_package(OpenSSL CONFIG REQUIRED)
find_package(nlohmann_json CONFIG REQUIRED)
find_package(GTest CONFIG REQUIRED)

# 3. Поиск Asio и Crow (должны быть установлены через vcpkg)
find_package(Asio CONFIG REQUIRED)
find_package(Crow CONFIG REQUIRED)

message(STATUS "Boost: ${Boost_FOUND} (${Boost_VERSION})")
message(STATUS "OpenSSL: ${OPENSSL_FOUND} (${OPENSSL_VERSION})")
message(STATUS "nlohmann_json: ${nlohmann_json_FOUND}")
message(STATUS "GTest: ${GTest_FOUND}")
message(STATUS "Asio: ${Asio_FOUND}")
message(STATUS "Crow: ${Crow_FOUND}")

message(STATUS "=== Добавление подпроектов ===")
add_subdirectory(allocator)
add_subdirectory(arithmetic)
add_subdirectory(associative_container)
add_subdirectory(common)
add_subdirectory(logger)

message(STATUS "=== Конфигурация завершена ===")




## Пример создания исполняемого файла
#add_executable(main_app main.cpp)
#target_link_libraries(main_app PRIVATE
#        Boost::boost
#        Boost::system
#        Boost::container
#        nlohmann_json::nlohmann_json
#        OpenSSL::SSL
#        OpenSSL::Crypto
#        Crow::Crow
#)