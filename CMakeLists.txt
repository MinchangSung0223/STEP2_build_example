#############################################################
# Minimum required version                                  #
#############################################################
cmake_minimum_required(VERSION 3.0)


#############################################################
# Toolchains                                                #
#############################################################
set(ENV{CC} "$ENV{NRMK_TOOLCHAIN_PC2}/i686-unknown-linux-gnu-gcc")
set(ENV{CXX} "$ENV{NRMK_TOOLCHAIN_PC2}/i686-unknown-linux-gnu-g++")


#############################################################
# Project name                                              #
#############################################################
project(HYU_SPA)


#############################################################
# C, CPP Standard                                           #
#############################################################
# C standard
set(CMAKE_C_STANDARD 11)

# CPP standard
set(CMAKE_CXX_STANDARD 11)


#############################################################
# Build type                                                #
#############################################################
SET(CMAKE_BUILD_TYPE 
	Release
#	Debug	
	)


#############################################################
# Includes                                                  #
#############################################################
include_directories(
	"$ENV{NRMK_XENO_PATH}/include"
	"$ENV{NRMK_ECAT_PATH}/include"
	"$ENV{NRMK_CORE_INC_PATH}"
	"$ENV{NRMK_HELPER_INC_PATH}"
	"$ENV{NRMK_EIGEN_INC_PATH}"
	"$ENV{NRMK_POCO_INC_PATH}"
	"$ENV{NRMK_HELPER_INC_PATH}/hw"
	"$ENV{NRMK_HELPER_INC_PATH}/hw/nrmk_ecat"
	"${CMAKE_CURRENT_SOURCE_DIR}/lib/KDL"
	"${CMAKE_CURRENT_SOURCE_DIR}/lib/RoboLimb"
	"${CMAKE_CURRENT_SOURCE_DIR}/lib/EcatSystem"
	"${CMAKE_CURRENT_SOURCE_DIR}/lib/Control"
	"${CMAKE_CURRENT_SOURCE_DIR}/lib/MR"
	"${CMAKE_CURRENT_SOURCE_DIR}"
	"${CMAKE_CURRENT_SOURCE_DIR}/lib"
	"${CMAKE_CURRENT_SOURCE_DIR}/include"
	"${CMAKE_CURRENT_SOURCE_DIR}/lib/EcatDataSocket"
	
	
	)


#############################################################
# Definitions                                               #
#############################################################
#add_definitions(
#	-D__XENO__
#	)


#############################################################
# Libraries                                                 #
#############################################################
# Define LIBS
if (CMAKE_BUILD_TYPE MATCHES Release)
set( LIBS 
	xenomai 
	native
	NRMKhw_tpd
	rt
	rtdm
	ethercat_rtdm
	NRMKHelperi686
	PocoNet
	PocoFoundation
	pthread
	)
else()
set( LIBS 
	xenomai 
	native
	rt
	rtdm
	ethercat_rtdm
	NRMKHelperi686d
	PocoNetd
	PocoFoundationd
	pthread
	)



endif()
	
# Library search path
link_directories(
	"$ENV{NRMK_XENO_PATH}/lib"
	"$ENV{NRMK_ECAT_PATH}/lib"
	"$ENV{NRMK_LIB_PATH}"
	"$ENV{NRMK_POCO_LIB_PATH}/i686"
	)


#############################################################
# Compiler & Linker flags                                   #
#############################################################
# C compiler flag
#SET(CMAKE_C_FLAGS
#	-fPIC
#	)
	
# CPP Compiler flag	
#SET(CMAKE_CXX_FLAGS
#	-fPIC
#	)

# Release flags
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3")

# Debug flags
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -Wall -O0")

# Linker flags
#SET(CMAKE_CXX_LINK_EXECUTABLE "${CMAKE_CXX_LINK_EXECUTABLE} -pie")
#SET(CMAKE_C_LINK_EXECUTABLE   "${CMAKE_C_LINK_EXECUTABLE}   -pie")
		
#############################################################
# Sources                                                   #
#############################################################
file(GLOB_RECURSE MR lib/MR/modern_robotics.h lib/MR/modern_robotics.cpp)
file(GLOB_RECURSE KDL  "lib/KDL/*.h" "lib/KDL/*.cpp")
file(GLOB_RECURSE PDO lib/EcatSystem/PDOConfig.c lib/EcatSystem/PDOConfig.h)
file(GLOB_RECURSE EcatSystem lib/EcatSystem/Ecat_Master.cpp lib/EcatSystem/Ecat_Master.h lib/EcatSystem/Ecat_Slave.h lib/EcatSystem/Ecat_Robotus.h lib/EcatSystem/Ecat_Elmo.h)

file(GLOB_RECURSE Control lib/Control/*.h lib/Control/*.cpp lib/Control/*.c)

file(GLOB_RECURSE EcatDataSocket lib/EcatDataSocket/EcatDataSocket.cpp lib/EcatDataSocket/EcatDataSocket.h lib/EcatDataSocket/EcatControlSocket.h) 

file(GLOB_RECURSE SOURCES "src/RTRArmClient.cpp")



#############################################################
# Executable                                                #
#############################################################
set(EXE ${PROJECT_NAME})
add_executable(${EXE} ${SOURCES} ${PDO} ${EcatDataSocket} ${KDL} ${Control} ${EcatSystem} )
set_target_properties(${PROJECT_NAME} PROPERTIES SUFFIX  "")

#############################################################
# Libraries linking                                         #
#############################################################
target_link_libraries(${EXE} ${LIBS} )

