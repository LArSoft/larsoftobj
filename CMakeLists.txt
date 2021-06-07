# ======================================================================
#  larsoftobj main build file
#
#  cd .../path/to/build/directory
#  source .../path/to/larsoftobj/ups/setup_for_development <-d|-p>
#  buildtool [-I /install/path] -bt[i] -jN
# ======================================================================
# LArSoftObj is an empty product
# It sets up the larsoftobj ups products (lardataobj, larcoreobj)
# ======================================================================

cmake_minimum_required (VERSION 3.19 FATAL_ERROR)

project(larsoftobj VERSION 09.05.04 LANGUAGES NONE)

find_package(cetmodules REQUIRED)
find_package(canvas_root_io)
find_package(art)

include(CetCMakeEnv)
cet_cmake_env()

# larsoftobj bundle scripts
add_subdirectory(bundle)
# ups - table and config files
if(WANT_UPS)
add_subdirectory(ups)
endif()

# packaging utility
include(UseCPack)
