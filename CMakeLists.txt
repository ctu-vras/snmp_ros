cmake_minimum_required(VERSION 3.8.0)
project(snmp_ros)

find_package(catkin REQUIRED)

catkin_package()

catkin_install_python(PROGRAMS nodes/snmp_reader DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

install(DIRECTORY config DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
