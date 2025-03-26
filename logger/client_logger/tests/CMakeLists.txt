add_executable(
        mp_os_lggr_clnt_lggr_tests
        client_logger_tests.cpp)

target_link_libraries(
        mp_os_lggr_clnt_lggr_tests
        PRIVATE
        GTest::gtest

)
target_link_libraries(
        mp_os_lggr_clnt_lggr_tests
        PUBLIC
        mp_os_lggr_clnt_lggr)