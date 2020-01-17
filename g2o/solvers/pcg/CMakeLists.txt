add_library(solver_pcg ${G2O_LIB_TYPE}
  solver_pcg.cpp
  linear_solver_pcg.h  
  linear_solver_pcg.hpp
)

target_include_directories(solver_pcg
                PUBLIC
                    $<INSTALL_INTERFACE:${INCLUDES_INSTALL_DIR}/solvers/pcg>
                    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
                PRIVATE
                    ${CMAKE_CURRENT_SOURCE_DIR})

set_target_properties(solver_pcg PROPERTIES OUTPUT_NAME ${LIB_PREFIX}solver_pcg)
if (APPLE)
  set_target_properties(solver_pcg PROPERTIES INSTALL_NAME_DIR "${CMAKE_INSTALL_PREFIX}/lib")
endif()

target_link_libraries(solver_pcg core)

install(TARGETS solver_pcg
  EXPORT ${G2O_TARGETS_EXPORT_NAME}
  RUNTIME DESTINATION ${RUNTIME_DESTINATION}
  LIBRARY DESTINATION ${LIBRARY_DESTINATION}
  ARCHIVE DESTINATION ${ARCHIVE_DESTINATION}
  INCLUDES DESTINATION ${INCLUDES_DESTINATION}
)

file(GLOB headers "${CMAKE_CURRENT_SOURCE_DIR}/*.h" "${CMAKE_CURRENT_SOURCE_DIR}/*.hpp")

install(FILES ${headers} DESTINATION ${INCLUDES_INSTALL_DIR}/solvers/pcg)
