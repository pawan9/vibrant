# Tests that don't require any arguments at runtime
#
set( no_argument_test_sources
  test_adaboost_learner.cxx
)

create_test_sourcelist( test_sources
  test_driver.cxx

  # List of source files
  ${no_argument_test_sources}
)

add_executable( vidtk_test_learning
   ${test_sources}
)
target_link_libraries( vidtk_test_learning vidtk_learning testlib vul vpl )

# Create ADD_TEST lines for some tests automatically.  Tests taking
# special arguments will be specified manually later.

foreach( filename ${no_argument_test_sources} )
  string( REPLACE ".cxx" "" filebase ${filename} )
  string( REPLACE "test_" "" testname ${filebase} )
  add_test( NAME vidtk_learning_${testname}
            COMMAND $<TARGET_FILE:vidtk_test_learning> ${filebase} )
endforeach( filename )

