
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

# define qualifiers
set( BASEQUAL e19 )

create_product_variables( larcoreobj  v09_00_00_rc0 )
create_product_variables( larcorealg  v09_00_00_rc0 )
create_product_variables( lardataobj  v09_00_00_rc0 )
create_product_variables( lardataalg  v09_00_00_rc0 )
create_product_variables( larsoftobj  v09_00_00_rc0 )

create_product_variables( canvas_root_io v1_05_02 )
create_product_variables( gallery     v1_14_02 )
create_product_variables( dk2nudata   v01_08_00g )
create_product_variables( nusimdata   v1_21_02 )
create_product_variables( mrb         v4_01_00 )
create_product_variables( hub         v2_12_4 )

# these files should be copied to scisoft for each release
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/larsoftobj-cfg.in
  ${CMAKE_CURRENT_BINARY_DIR}/larsoftobj-cfg-${LARSOFTOBJ_DOT_VERSION} @ONLY )
CONFIGURE_FILE ( ${CMAKE_CURRENT_SOURCE_DIR}/larsoftobj.html.in
  ${CMAKE_CURRENT_BINARY_DIR}/larsoftobj-${LARSOFTOBJ_VERSION}.html @ONLY )
