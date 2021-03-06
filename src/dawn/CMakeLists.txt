# Copyright 2018 The Amber Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

set(DAWN_ENGINE_SOURCES
    engine_dawn.cc
)

set(AMBER_EXTRA_LIBS "")
if(APPLE)
  add_definitions(-DAMBER_DAWN_METAL=1)
  list(APPEND DAWN_ENGINE_SOURCES device_metal.mm)
  find_library(METAL_LIB Metal)
  list(APPEND AMBER_EXTRA_LIBS ${METAL_LIB})
else()
  add_definitions(-DAMBER_DAWN_METAL=0)
endif(APPLE)

add_library(libamberenginedawn ${DAWN_ENGINE_SOURCES})
amber_default_compile_options(libamberenginedawn)
set_target_properties(libamberenginedawn PROPERTIES
    OUTPUT_NAME "amberenginedawn"
)
target_link_libraries(libamberenginedawn libamber Dawn::dawn_native Dawn::dawn
  ${AMBER_EXTRA_LIBS})
