cmake_minimum_required(VERSION 3.10)

project(dns)

if ("${CMAKE_SOURCE_DIR}" STREQUAL "${CMAKE_BINARY_DIR}")
  message(SEND_ERROR "In-source builds are not allowed.")
endif ()

set(dns_SRCS
    ${CMAKE_CURRENT_SOURCE_DIR}/src/dns.c
)
add_library(dns ${dns_SRCS})
target_compile_options(dns PRIVATE -std=gnu99 -Wall -Wextra -O2 -g -fstack-protector)
target_include_directories(dns PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src/)
install(TARGETS dns DESTINATION lib)
install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/dns.h DESTINATION include)

add_executable(dnsc ${dns_SRCS})
target_compile_options(dnsc PRIVATE -DDNS_DEBUG -DDNS_MAIN -std=gnu99 -Wall -Wextra -O2 -g -fstack-protector)
target_include_directories(dnsc PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src/)
install(TARGETS dnsc DESTINATION bin)
