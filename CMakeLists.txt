cmake_minimum_required(VERSION 3.10)

project(LearningCFD)
file(GLOB SOURCES "src/*")
file(GLOB HEADERS "include/*")
# Set the C++ standard to use
set(CMAKE_CXX_STANDARD 11)

# Find GSL package
find_package(GSL REQUIRED)

# Add your source files here
set(SOURCES
    src/main.cpp
    # Add other source files if any
)

# Create an executable from the source files
add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

set_target_properties(${PROJECT_NAME} PROPERTIES 
	RUNTIME_OUTPUT_DIRECTORY ../bin
	)

# Link GSL library to the executable
target_link_libraries(${PROJECT_NAME} GSL::gsl GSL::gslcblas)

# Set the CMake generator to Ninja
set(CMAKE_GENERATOR "Ninja")

add_custom_target(run
	COMMAND ninja && ../bin/${PROJECT_NAME}
	DEPENDS ${PROJECT_NAME}
	WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
	)

