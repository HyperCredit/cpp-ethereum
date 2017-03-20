file(GLOB SRC_LIST "*.cpp")
file(GLOB HEADERS "*.h")

add_library(devcore ${SRC_LIST} ${HEADERS})

add_dependencies(devcore BuildInfo.h)

find_package(LevelDB)
target_include_directories(devcore PRIVATE ..)
# We have to add boost include dir explicitly before leveldb, not to
# include system-level boost if installed.
target_include_directories(devcore SYSTEM PUBLIC ${Boost_INCLUDE_DIRS} ${LEVELDB_INCLUDE_DIRS})
target_link_libraries(devcore Boost::filesystem Boost::system Boost::random Boost::thread ${LEVELDB_LIBRARIES})
