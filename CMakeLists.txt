cmake_minimum_required(VERSION 2.8.3)

project(jumping_robot_ry)

find_package(catkin REQUIRED)

catkin_package()

find_package(roslaunch)

# Configure the module file first
configure_file(module/module.yaml "${CMAKE_CURRENT_BINARY_DIR}/module/module.yaml")
# Now configure the alias in the HOME directory at a location where mc_rtc looks for aliases
configure_file(module/alias.yaml $ENV{HOME}/.config/mc_rtc/aliases/JumpingRobotRy.yaml)

configure_file(mujoco/jumping_robot_ry.yaml $ENV{HOME}/.config/mc_rtc/mc_mujoco/jumping_robot_ry.yaml)

foreach(dir meshes urdf)
	install(DIRECTORY ${dir}/
		DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/${dir})
endforeach(dir)
