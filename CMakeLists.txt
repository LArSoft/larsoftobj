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

cmake_minimum_required(VERSION 3.20 FATAL_ERROR)

find_package(cetmodules REQUIRED)
project(larsoftobj LANGUAGES NONE)

# cetbuildtools contains our cmake modules

include(CetCMakeEnv)
set(${PROJECT_NAME}_CMAKE_PROJECT_VERSION_STRING 09.80.00-rc0)
cet_cmake_env()

# larsoftobj bundle scripts
add_subdirectory(bundle)

# packaging utility
cet_cmake_config()
