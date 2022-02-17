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
# cmake_policy(VERSION 3.19) ### MIGRATE-ACTION-COMPATIBILITY (migrate-3.05.03) - Uncomment to preseve compatibility with older CMake versions

find_package(cetmodules REQUIRED)
project(larsoftobj VERSION 09.16.01 LANGUAGES NONE)

# cetbuildtools contains our cmake modules

include(CetCMakeEnv)
cet_cmake_env()

# larsoftobj bundle scripts
add_subdirectory(bundle)
# ups - table and config files

# packaging utility
cet_cmake_config()
