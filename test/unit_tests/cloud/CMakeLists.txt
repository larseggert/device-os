# Global defines
add_definitions(-DLOG_DISABLE)

# Generate include path
include_directories(
  ${THIRD_PARTY_DIR}/fakeit/fakeit/single_header/catch/
  ${DEVICE_OS_DIR}/communication/src/
  ${DEVICE_OS_DIR}/hal/inc/
  ${DEVICE_OS_DIR}/hal/shared/
  ${DEVICE_OS_DIR}/hal/src/stm32/
  ${DEVICE_OS_DIR}/services/inc/
  ${DEVICE_OS_DIR}/system/inc/
  ${DEVICE_OS_DIR}/system/src/
  ${TEST_DIR}/
  ${TEST_DIR}/unit_tests/
  ${DEVICE_OS_DIR}/wiring/inc/
)

# Create test executable
add_executable( publish_vitals
  ${DEVICE_OS_DIR}/system/src/system_publish_vitals.cpp
  publish_vitals.cpp
)

# Set compiler flags specific to target
target_compile_options( publish_vitals
  PRIVATE -fno-inline -fprofile-arcs -ftest-coverage -O0 -g
)

# Link against dependencies specific to target

# Add tests to `test` target
catch_discover_tests( publish_vitals
  TEST_PREFIX cloud_publish_vitals_
)
