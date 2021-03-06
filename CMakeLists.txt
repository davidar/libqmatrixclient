cmake_minimum_required(VERSION 2.8.11) # Maybe works with even older versions

project(qmatrixclient)
enable_language(CXX)

include(CheckCXXCompilerFlag)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)
# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)


message( STATUS )
message( STATUS "================================================================================" )
message( STATUS "                          libqmatrixclient Build Information                          " )
message( STATUS "================================================================================" )
message( STATUS "Building with: ${CMAKE_CXX_COMPILER_ID} ${CMAKE_CXX_COMPILER_VERSION}" )
message( STATUS "Install Prefix: ${CMAKE_INSTALL_PREFIX}" )
message( STATUS "Path to Qt Core: ${Qt5Core_DIR}" )
message( STATUS "================================================================================" )
message( STATUS )

# Set up source files
set(libqmatrixclient_SRCS
   connectiondata.cpp
   connection.cpp
   connectionprivate.cpp
   room.cpp
   user.cpp
   logmessage.cpp
   state.cpp
   events/event.cpp
   events/roommessageevent.cpp
   events/roomnameevent.cpp
   events/roomaliasesevent.cpp
   events/roomcanonicalaliasevent.cpp
   events/roommemberevent.cpp
   events/roomtopicevent.cpp
   events/typingevent.cpp
   events/receiptevent.cpp
   events/unknownevent.cpp
   jobs/basejob.cpp
   jobs/checkauthmethods.cpp
   jobs/passwordlogin.cpp
   jobs/postmessagejob.cpp
   jobs/postreceiptjob.cpp
   jobs/joinroomjob.cpp
   jobs/leaveroomjob.cpp
   jobs/roommembersjob.cpp
   jobs/roommessagesjob.cpp
   jobs/syncjob.cpp
   jobs/mediathumbnailjob.cpp
   jobs/logoutjob.cpp
    )

add_library(qmatrixclient ${libqmatrixclient_SRCS})

if ( CMAKE_VERSION VERSION_LESS "3.1" )
    CHECK_CXX_COMPILER_FLAG("-std=c++11" STD_FLAG_SUPPORTED)
    if ( STD_FLAG_SUPPORTED )
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
    endif ( STD_FLAG_SUPPORTED )
else ( CMAKE_VERSION VERSION_LESS "3.1" )
    target_compile_features(qmatrixclient PRIVATE cxx_range_for)
    target_compile_features(qmatrixclient PRIVATE cxx_override)
    target_compile_features(qmatrixclient PRIVATE cxx_strong_enums)
    target_compile_features(qmatrixclient PRIVATE cxx_lambdas)
    target_compile_features(qmatrixclient PRIVATE cxx_auto_type)
    target_compile_features(qmatrixclient PRIVATE cxx_generalized_initializers)
    target_compile_features(qmatrixclient PRIVATE cxx_nullptr)
endif ( CMAKE_VERSION VERSION_LESS "3.1" )

target_link_libraries(qmatrixclient Qt5::Core Qt5::Network Qt5::Gui)
