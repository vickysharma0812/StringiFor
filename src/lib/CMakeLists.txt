SET(SRC_PATH "${CMAKE_CURRENT_LIST_DIR}/")
TARGET_SOURCES(
    ${PROJECT_NAME} PRIVATE
    ${SRC_PATH}/stringifor_string_t.F90
    ${SRC_PATH}/stringifor.F90
)

# set variables used for compile definitions of targets after support check
include(CheckFortranSourceRuns)
check_fortran_source_runs(
    "program r16p_support;
         integer, parameter :: r16p = selected_real_kind(33, 4931);
         if(r16p < 0) stop 1;
     end program r16p_support"
     R16P_SUPPORTED
     SRC_EXT f90)
if(R16P_SUPPORTED)
    set(r16p_supported "-D_R16P")
endif()

LIST( APPEND TARGET_COMPILE_DEF ${r16p_supported} )