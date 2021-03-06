# Copyright 2013 Matt Mason
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

if (MSVC)
  # VS2012 faux-variadic template need to be bumped to 10 args
  # to support GoogleTest tuple requirements.
  # GoogleTest also (by default) wants us to use static runtime -
  # change this according to your needs.
  add_definitions("-D_VARIADIC_MAX=10" "/MTd")
endif (MSVC)

file(GLOB_RECURSE sources *.cpp)
include_directories(${stateless++_SOURCE_DIR} . ./gtest-1.6.0)
add_executable(test_stateless++ ${sources} ./gtest-1.6.0/gtest/gtest-all.cc)
if (NOT MSVC)
  target_link_libraries(test_stateless++ pthread)
endif (NOT MSVC)
add_test("unit_test" test_stateless++)

