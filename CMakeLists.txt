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

cmake_minimum_required(VERSION 3.19 FATAL_ERROR)

project(larsoftobj LANGUAGES NONE)

# cetbuildtools contains our cmake modules
find_package(cetbuildtools REQUIRED)

include(CetCMakeEnv)
set(${PROJECT}_CMAKE_PROJECT_VERSION_STRING 09.16.00-rc0)
cet_cmake_env()

# larsoftobj bundle scripts
add_subdirectory(bundle)
# ups - table and config files
add_subdirectory(ups)

# packaging utility
include(UseCPack)
