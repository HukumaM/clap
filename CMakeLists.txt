cmake_minimum_required (VERSION 3.8)

# Enabling hot reboot for MSVC compilers, if supported.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project (clap
	VERSION 0.0.1
	LANGUAGES CXX
)

set(CLAP_SOURCE_DIR ${CMAKE_CURRENT_LIST_DIR}/source CACHE STRING "" FORCE)
set(CLAP_INCLUDE_DIR ${CMAKE_CURRENT_LIST_DIR}/include CACHE STRING "" FORCE)

add_executable (clap 
	${CLAP_SOURCE_DIR}/clap.cpp
	${CLAP_INCLUDE_DIR}/clap.hpp
)

target_include_directories(clap 
	PRIVATE ${CLAP_INCLUDE_DIR}
)

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET clap PROPERTY CXX_STANDARD 20)
endif()
