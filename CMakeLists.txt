cmake_minimum_required(VERSION 3.9.6)
if(CMAKE_CONFIGURATION_TYPES)
  set(CMAKE_CONFIGURATION_TYPES Debug Release)
  set(CMAKE_CONFIGURATION_TYPES "${CMAKE_CONFIGURATION_TYPES}" CACHE STRING
    "Set the configurations to what we need" FORCE
    )
endif()
project(stropheExamples)
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR}) # Findexternpro.cmake
set(externpro_REV 18.01.1-14-g155a230)
find_package(externpro REQUIRED)
xpCommonFlags()
xpGetExtern(externIncs externLibs PRIVATE libstrophe)
set(examples
  active
  basic
  bot
  component
  roster
  uuid
  )
foreach(exe ${examples})
  add_executable(${exe} ${exe}.c)
  target_link_libraries(${exe} ${externLibs})
  target_include_directories(${exe} ${externIncs})
  set_property(TARGET ${exe} PROPERTY FOLDER examples)
endforeach()
