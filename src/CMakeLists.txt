# CMake最低版本要求
cmake_minimum_required(VERSION 3.10)

# 设置项目名称，版本号
project(navisechPE VERSION 1.0)

#设置cmake编译模式，省缺为release模式
set(CMAKE_BUILD_TYPE "Debug")

# 设置可执行程序输出目录
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/../bin)

# 设置库输出目录
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/../bin)

# 增加宏
add_definitions(-DWIN32 -D_CRT_SECURE_NO_WARNINGS -D_WINSOCK_DEPRECATED_NO_WARNINGS -DDLL)

# 添加lib路径
link_directories(../lib)

# 添加依赖库
link_libraries(winmm.lib ws2_32.lib)

# 设置源文件路径到变量中
aux_source_directory(${CMAKE_SOURCE_DIR}/nav DIR_NAV_SOURCE)
aux_source_directory(${CMAKE_SOURCE_DIR}/rcv DIR_RCV_SOURCE)

# 包含头文件
include_directories(../include)

# 生成可执行程序
add_executable(navisechPE ${DIR_NAV_SOURCE} ${DIR_RCV_SOURCE})

# 编译静态库
add_library(staticNavisechPE ${DIR_NAV_SOURCE} ${DIR_RCV_SOURCE})

# 编译动态库
add_library(dynamicNavisechPE SHARED ${DIR_NAV_SOURCE} ${DIR_RCV_SOURCE})

message(STATUS "DIR_NAV_SOURCE:${DIR_NAV_SOURCE}")
message(STATUS "DIR_RCV_SOURCE:${DIR_RCV_SOURCE}")