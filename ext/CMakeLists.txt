if(NOT TARGET klib)
  set(FETCHCONTENT_QUIET OFF)
  include(FetchContent)

  FetchContent_Declare(klib
    GIT_REPOSITORY https://github.com/karnkaul/klib
    GIT_TAG v0.4.1
    SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src/klib"
    GIT_SHALLOW TRUE
  )

  message(STATUS "[klib]")
  FetchContent_MakeAvailable(klib)
endif()
