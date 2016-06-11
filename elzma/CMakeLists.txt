# Written in 2009 by Lloyd Hilaiel
#
# License
# 
# All the cruft you find here is public domain.  You don't have to credit
# anyone to use this code, but my personal request is that you mention
# Igor Pavlov for his hard, high quality work.
#

IF (WIN32)
  ADD_DEFINITIONS(-DWIN32)
ENDIF (WIN32)

# set up some paths
SET (binDir ${CMAKE_CURRENT_BINARY_DIR}/../${EASYLZMA_DIST_NAME}/bin)

# create some directories
FILE(MAKE_DIRECTORY ${binDir})

SET (SRCS elzma.c util.c)
SET (HDRS util.h)

# use the library we built
INCLUDE_DIRECTORIES(
    ${CMAKE_CURRENT_BINARY_DIR}/../${EASYLZMA_DIST_NAME}/include
)
LINK_DIRECTORIES(
    ${CMAKE_CURRENT_BINARY_DIR}/../${EASYLZMA_DIST_NAME}/lib
)

ADD_EXECUTABLE(elzma ${SRCS})

TARGET_LINK_LIBRARIES(elzma easylzma_s)

# Add binary installation for the "install" target
install (TARGETS elzma
    DESTINATION bin
    PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE
        WORLD_READ WORLD_EXECUTE
)
