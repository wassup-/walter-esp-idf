message(STATUS "WalterModem:")

foreach(feature IN ITEMS SOCKETS COAP MQTT HTTP MOTA OTA)
    if(CONFIG_WALTER_MODEM_ENABLE_${feature} STREQUAL "y")
        message(STATUS "${feature} enabled: true")
    else()
        message(STATUS "${feature} enabled: false")
    endif()
endforeach()

cmake_minimum_required(VERSION 3.20)
set (CMAKE_CXX_STANDARD 23)

idf_component_register(
    SRCS "src/WalterModem.cpp"
         "src/proto/WalterCoAP.cpp"
         "src/proto/WalterBlueCherry.cpp"
         "src/proto/WalterGNSS.cpp"
         "src/proto/WalterHTTP.cpp"
         "src/proto/WalterMQTT.cpp"
         "src/proto/WalterSocket.cpp"
    INCLUDE_DIRS "src"
    REQUIRES fatfs esp_partition app_update spi_flash driver vfs
)

add_compile_options(-Wno-error)
