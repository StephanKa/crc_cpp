FIND_PACKAGE(Catch2 REQUIRED)

INCLUDE(CTest)
INCLUDE(Catch)

ADD_EXECUTABLE(tests test.cpp)
TARGET_LINK_LIBRARIES(tests PRIVATE project_warnings project_options Catch2::Catch2WithMain)
TARGET_INCLUDE_DIRECTORIES(tests PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/../include ${Catch2_INCLUDE_DIR})

# automatically discover tests that are defined in catch based test files you can modify the unittests. Set TEST_PREFIX
# to whatever you want, or use different for different binaries
CATCH_DISCOVER_TESTS(
        tests
        TEST_PREFIX
        "unittests."
        REPORTER
        JUnit
        OUTPUT_DIR
        .
        OUTPUT_PREFIX
        "unittests."
        OUTPUT_SUFFIX
        .xml)
