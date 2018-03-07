#Copyright (c) Microsoft. All rights reserved.
#Licensed under the MIT license. See LICENSE file in the project root for full license information.

#this is CMakeLists.txt for iothub_client_sample_mqtt
cmake_minimum_required(VERSION 2.8.11)

if(WIN32)
    message(FATAL_ERROR "This CMake file is only support Linux builds!")
endif()

set(AZUREIOT_INC_FOLDER ".." "/usr/include/azureiot" "/usr/include/azureiot/inc")

include_directories(${AZUREIOT_INC_FOLDER})

set(iothub_c_files
    iothub_ll_telemetry_sample.c
    ${PROJECT_SOURCE_DIR}/certs/certs.c
)

add_executable(iothub_ll_telemetry_sample ${iothub_c_files})

target_link_libraries(iothub_ll_telemetry_sample
    iothub_client_mqtt_transport
    iothub_client_amqp_transport
    iothub_client_http_transport
    iothub_client 
    aziotsharedutil
    umqtt
    pthread
    curl
    ssl
    crypto
    m
)