#
# Copyright (c) 2019 Nordic Semiconductor
#
# SPDX-License-Identifier: LicenseRef-BSD-5-Clause-Nordic
#

cmake_minimum_required(VERSION 3.13.1)

include($ENV{ZEPHYR_BASE}/../nrf/cmake/boilerplate.cmake)
include($ENV{ZEPHYR_BASE}/cmake/app/boilerplate.cmake NO_POLICY_SCOPE)
project(json)

FILE(GLOB app_sources src/*.c)
target_sources(app PRIVATE ${app_sources})

target_sources(app
  PRIVATE
  ${ZEPHYR_BASE}/../nrf/subsys/dfu/src/dfu_target_mcuboot.c
  )

target_include_directories(app
  PRIVATE
  ${ZEPHYR_BASE}/../nrf/subsys/dfu/include
  . # To get 'pm_config.h'
  )

target_compile_options(app
  PRIVATE
  -DCONFIG_IMG_BLOCK_BUF_SIZE=4096
  -DCONFIG_DFU_TARGET_LOG_LEVEL=2
  -DCONFIG_AWS_FOTA_FILE_PATH_MAX_LEN=1024
  )
