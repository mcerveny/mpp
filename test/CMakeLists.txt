# vim: syntax=cmake
# ----------------------------------------------------------------------------
# mpp built-in unit test case
# ----------------------------------------------------------------------------
# macro for adding mpp sub-module unit test
macro(add_mpp_test module)
    set(test_name ${module}_test)
    string(TOUPPER ${test_name} test_tag)
    #message(STATUS "moduule   : ${module}")
    #message(STATUS "test_name : ${test_name}")
    #message(STATUS "test_tag  : ${test_tag}")

    option(${test_tag} "Build mpp ${module} unit test" ON)
    if(${test_tag})
        add_executable(${test_name} ${test_name}.c)
        # NOTE: use share library on Linux and Android
        #       use static library for window debug
        if(UNIX)
            target_link_libraries(${test_name} mpp_shared utils)
        else()
            target_link_libraries(${test_name} mpp_shared utils)
        endif()
        set_target_properties(${test_name} PROPERTIES FOLDER "test")
        #install(TARGETS ${test_name} RUNTIME DESTINATION ${TEST_INSTALL_DIR})
        #add_test(NAME ${test_name} COMMAND ${test_name})
    endif()
endmacro()

# mpp_buffer unit test
add_mpp_test(mpp_buffer)

# mpp_packet unit test
add_mpp_test(mpp_packet)

# mpi unit test
add_mpp_test(mpi)

# mpi decoder unit test
add_mpp_test(mpi_dec)

# mpi encoder unit test
add_mpp_test(mpi_enc)

# mpi rc unit test
add_mpp_test(mpi_rc)

macro(add_legacy_test module)
    set(test_name ${module}_test)
    string(TOUPPER ${test_name} test_tag)
    #message(STATUS "moduule   : ${module}")
    #message(STATUS "test_name : ${test_name}")
    #message(STATUS "test_tag  : ${test_tag}")

    option(${test_tag} "Build legacy ${module} unit test" ON)
    if(${test_tag})
        add_executable(${test_name} ${test_name}.c)
        target_link_libraries(${test_name} mpp_legacy_shared utils)
        set_target_properties(${test_name} PROPERTIES FOLDER "test")
        #install(TARGETS ${test_name} RUNTIME DESTINATION ${TEST_INSTALL_DIR})
        #add_test(NAME ${test_name} COMMAND ${test_name})
    endif()
endmacro()

# legacy vpu_api unit test
add_legacy_test(vpu_api)
