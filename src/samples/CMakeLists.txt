# CMakeLists.txt
#
# CMake file for the Paho C++ sample applications.
#
#*******************************************************************************
# This is part of the Paho MQTT C++ client library.
#
# Copyright (c) 2016-2019
# 
# All rights reserved. This program and the accompanying materials
# are made available under the terms of the Eclipse Public License v1.0
# and Eclipse Distribution License v1.0 which accompany this distribution.
# 
# The Eclipse Public License is available at
#   http://www.eclipse.org/legal/epl-v10.html
# and the Eclipse Distribution License is available at
#   http://www.eclipse.org/org/documents/edl-v10.php.
# 
# Contributors:
#   Guilherme Maciel Ferreira - initial version
#   Frank Pagliughi - Updates for new samples
#*******************************************************************************/

## Note: on OS X you should install XCode and the associated command-line tools

## --- Library dependencies ---

set (THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

## include directories
#include_directories(${CMAKE_CURRENT_SOURCE_DIR})

## binary files
add_executable(async_publish async_publish.cpp)
add_executable(async_subscribe async_subscribe.cpp)

## link binaries
target_link_libraries(async_publish ${PAHO_CPP_LIB})
target_link_libraries(async_subscribe ${PAHO_CPP_LIB})

set(INSTALL_TARGETS
	async_publish
	async_subscribe
)

if(PAHO_WITH_SSL)
	## SSL binary files
	add_executable(ssl_publish ssl_publish.cpp)

	## link SSL binaries
	target_link_libraries(ssl_publish ${PAHO_CPP_LIB})

	set(INSTALL_TARGETS
		${INSTALL_TARGETS}
		ssl_publish
	)

	add_definitions(-DOPENSSL)
endif()

## install binaries
install(TARGETS ${INSTALL_TARGETS} EXPORT PahoMqttCppSamples
	RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib
)

