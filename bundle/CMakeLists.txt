# variables to be used in cmake templates
macro( create_product_variables productname productversion )
   string(TOUPPER ${productname} PRODUCTNAME_UC )
   string(TOLOWER ${productname} PRODUCTNAME_LC )

   # require ${PRODUCTNAME_UC}_VERSION
   set( ${PRODUCTNAME_UC}_VERSION "${productversion}" )
   if ( NOT ${PRODUCTNAME_UC}_VERSION )
     message(FATAL_ERROR "product version is not defined")
   endif ()
   STRING( REGEX REPLACE "_" "." VDOT "${productversion}"  )
   STRING( REGEX REPLACE "^[v]" "" ${PRODUCTNAME_UC}_DOT_VERSION "${VDOT}" )
   set( ${PRODUCTNAME_UC}_STRING ${PRODUCTNAME_LC}.${${PRODUCTNAME_UC}_DOT_VERSION} )
   #message(STATUS "${PRODUCTNAME_UC} version is ${${PRODUCTNAME_UC}_VERSION}")
endmacro( create_product_variables)

function(create_version_variables VAR_STEM)
  cmake_parse_arguments(CVV "LIST" "NAME" "QUALIFIERS" ${ARGN})
  if (NOT VAR_STEM)
    message(FATAL_ERROR "vacuous VAR_STEM")
  elseif (NOT CVV_UNPARSED_ARGUMENTS)
    message(FATAL_ERROR "No versions specified")
  endif()
  string(TOUPPER ${VAR_STEM} VAR_STEM_UC)
  list(LENGTH CVV_UNPARSED_ARGUMENTS num_versions)
  if (CVV_LIST OR num_versions GREATER 1)
    set(list_suffix _LIST)
  else()
    set(list_suffix)
  endif()
  string(REPLACE ";" " " versions "${CVV_UNPARSED_ARGUMENTS}")
  set(${VAR_STEM_UC}_VERSION${list_suffix} "${versions}" PARENT_SCOPE)
  set(dot_versions)
  foreach(VERSION ${CVV_UNPARSED_ARGUMENTS})
    string(REPLACE "_" "." VDOT "${VERSION}")
    string(REGEX REPLACE "^v" "" VDOT "${VDOT}")
    list(APPEND dot_versions ${VDOT})
  endforeach()
  string(REPLACE ";" " " dot_versions "${dot_versions}")
  set(${VAR_STEM_UC}_DOT_VERSION${list_suffix}
    "${dot_versions}" PARENT_SCOPE)
  if (NOT CVV_NAME)
    set(CVV_NAME "${VAR_STEM}")
  endif()
  set(${VAR_STEM_UC}_NAME "${CVV_NAME}" PARENT_SCOPE)
  if (CVV_QUALIFIERS)
    set(${VAR_STEM_UC}_QUAL "${CVV_QUALIFIERS}" PARENT_SCOPE)
  endif()
endfunction()

# define qualifiers
set( BASEQUAL e26 )

create_product_variables( larcoreobj v10_00_00rc1 )
create_product_variables( larcorealg v10_00_00rc1 )
create_product_variables( lardataobj v10_00_00rc1 )
create_product_variables( lardataalg v10_00_00rc1 )
create_product_variables( larvecutils v09_04_01 )
create_product_variables( larsoftobj v10_00_00rc1 )

create_product_variables( canvas_root_io v1_13_05 )
create_product_variables( gallery v1_22_05 )
create_product_variables( dk2nudata v01_10_01g )
create_product_variables( nusimdata v1_28_03 )
create_product_variables( mrb v6_09_05 )
create_product_variables( hub         v2_14_2 )
create_product_variables( gh v2_25_1 )

# CMake and cetmodules are special:
#  define as many versions as necessary.
create_version_variables(cmake LIST v3_20_0 v3_21_4 v3_22_0 v3_22_2 v3_24_1 v3_25_2 v3_27_4)
create_version_variables(cetmodules LIST v3_16_00 v3_20_00 v3_22_02 v3_24_01)

create_version_variables(ups v6_1_1)

# these files should be copied to scisoft for each release
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/larsoftobj-cfg.in
  ${CMAKE_CURRENT_BINARY_DIR}/larsoftobj-cfg-${LARSOFTOBJ_DOT_VERSION} @ONLY )
CONFIGURE_FILE ( ${CMAKE_CURRENT_SOURCE_DIR}/larsoftobj.html.in
  ${CMAKE_CURRENT_BINARY_DIR}/larsoftobj-${LARSOFTOBJ_VERSION}.html @ONLY )
