cmake_minimum_required(VERSION 3.2)
project( client )
 
# 设置用debug还是release模式。debug允许断点，而release更快
#set( CMAKE_BUILD_TYPE Debug )
set( CMAKE_BUILD_TYPE Release )
 
# 设置编译选项
# 允许c++11标准、O3优化、多线程。match选项可避免一些cpu上的问题
set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -march=native -O3 -pthread" )
 
# 常见依赖库
#find_package( OpenCV REQUIRED )

# 添加子项目
# git submodule add <submodule_url>  
add_subdirectory(3rdparty/glog)
add_subdirectory(3rdparty/handy)

option(BUILD_CLIENT_SHARED_LIBRARY "Build CLIENT Shared Library" OFF)
option(BUILD_CLIENT_STATIC_LIBRARY "Build CLIENT Shared Library" ON)
option(BUILD_CLIENT_EXAMPLES "Build CLIENT Examples" OFF)

list(APPEND CLIENT_SRCS
    ${PROJECT_SOURCE_DIR}/src/main.cc)

# 二进制文件输出到bin
#set( EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin )

# 库输出到lib
#set( LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib )
 
# 库文件目录
link_directories(
    ${PROJECT_SOURCE_DIR}/build/3rdparty/glog
    ${PROJECT_SOURCE_DIR}/build/3rdparty/handy
    /usr/local/lib
)

# 头文件目录
include_directories (
    ${PROJECT_SOURCE_DIR}/build/3rdparty/glog
    ${PROJECT_SOURCE_DIR}/3rdparty/handy/

    /usr/local/include
)

# #CLIENT Static library
# if(BUILD_CLIENT_STATIC_LIBRARY)
#     add_executable(isCLIENT STATIC ${CLIENT_SRCS})
# endif(BUILD_CLIENT_STATIC_LIBRARY)

# #CLIENT Static library
# if(BUILD_CLIENT_SHARED_LIBRARY)
#     add_executable(isCLIENT SHARED ${CLIENT_SRCS})
# endif(BUILD_CLIENT_SHARED_LIBRARY)


add_executable(client ${CLIENT_SRCS})
target_link_libraries(client glog handy_s)