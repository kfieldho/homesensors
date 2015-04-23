cmake_minimum_required(VERSION 2.8)
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/arduino-cmake/cmake/ArduinoToolchain.cmake)
project(FIELDHOUSEIOT)

# These work for my Mac and Chromebook and are reasonable guesses elsewhere
if (${CMAKE_HOST_SYSTEM_NAME} MATCHES "Darwin")
	set(TTY /dev/tty.usbmodem1411)
elseif (${CMAKE_HOST_SYSTEM_NAME} MATCHES "Linux")
	set(TTY /dev/ttyACM0)
else()
	set(TTY /dev/TTY0)
endif()

link_directories(${PROJECT_SOURCE_DIR}/mysensorsorg/libraries)
set(MySensor_RECURSE true)

set(SerialGateway_SKETCH ${PROJECT_SOURCE_DIR}/mysensorsorg/libraries/MySensor/examples/SerialGateway)
set(SerialGateway_BOARD "uno")
set(SerialGateway_PORT ${TTY})

generate_arduino_firmware(SerialGateway)

set(HumiditySensor_SKETCH ${PROJECT_SOURCE_DIR}/mysensorsorg/libraries/MySensor/examples/HumiditySensor)
set(HumiditySensor_BOARD "uno")
set(HumiditySensor_PORT ${TTY})

generate_arduino_firmware(HumiditySensor)

set(HumiditySensorNano_SKETCH ${PROJECT_SOURCE_DIR}/mysensorsorg/libraries/MySensor/examples/HumiditySensor)
set(HumiditySensorNano_BOARD "nano")
set(HumiditySensorNano_PORT ${TTY})

generate_arduino_firmware(HumiditySensorNano)





