project( TVDMFFDVFR )

include(CTest)
enable_testing()

cmake_minimum_required(VERSION 2.8.2)
set(CMAKE_BUILD_TYPE "Release")

#Change PROJECT_NAME to the name of your project

option(USE_ITK "Use ITK Libraries" ON)

set (CMAKE_INCLUDE_DIRECTORIES_BEFORE ON)


# Set up ITK
if(USE_ITK)
  find_package(ITK)
  if(ITK_FOUND)
    include(${ITK_USE_FILE})
  else(ITK_FOUND)
    message(FATAL_ERROR
      "Cannot build without ITK.  Please set ITK_DIR.")
  endif(ITK_FOUND)
endif(USE_ITK)

set(DART_TESTING_TIMEOUT 1500)

link_directories( ${ITK_LIBRARY_PATH} )

# non-templated class -- this should be stored in a library and linked in...
set( UI_SOURCES "antsCommandLineParser" "antsCommandLineOption" )

add_executable(antsApplyTransforms antsApplyTransforms.cxx ${UI_SOURCES})
target_link_libraries(antsApplyTransforms ${ITK_LIBRARIES} )

add_executable(antsRegistration antsRegistration.cxx ${UI_SOURCES})
target_link_libraries(antsRegistration ${ITK_LIBRARIES} )

