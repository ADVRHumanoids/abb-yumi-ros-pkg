cmake_minimum_required(VERSION 2.8)
PROJECT(abb-yumi-ros-pkg)

add_custom_target(  acm
                    COMMAND ${CMAKE_SOURCE_DIR}/yumi_urdf/script/create_acm.sh yumi)

add_custom_target(	remove_old_yumi_urdf_gazebo ALL
    				COMMAND ${CMAKE_COMMAND} -E remove_directory 
        			"~/.gazebo/models/yumi_urdf/")

add_custom_target(  remove_old_yumi_gazebo ALL
                    COMMAND ${CMAKE_COMMAND} -E remove_directory 
                    "~/.gazebo/models/yumi/")

add_custom_target(  compile_urdf_sdf ALL
                    COMMAND ${CMAKE_SOURCE_DIR}/yumi_urdf/script/create_urdf_srdf_sdf.sh yumi)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
    add_custom_target(	copy_yumi_gazebo ALL
        				COMMAND ${CMAKE_COMMAND} -E copy_directory 
            			"${PROJECT_SOURCE_DIR}/yumi_gazebo/sdf/" 
            			"~/.gazebo/models/yumi/"
            			DEPENDS remove_old_yumi_gazebo)
endif()
