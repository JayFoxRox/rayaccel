cmake_minimum_required(VERSION 3.13)

set(RENDERER_SOURCES
  Renderer/Camera.cpp
  Renderer/Camera.h
  Renderer/DisplayBuffer.cpp
  Renderer/DisplayBuffer.h
  Renderer/LightPath.cpp
  Renderer/LightPath.h
  Renderer/main.cpp
  Renderer/Materials.cpp
  Renderer/Materials.h
  Renderer/PathTracingRenderer.cpp
  Renderer/PathTracingRenderer.h
  Renderer/Renderer.h
  Renderer/SceneData.h
  Renderer/SimdRandom.h
  Renderer/TiledRenderer.cpp
  Renderer/TiledRenderer.h
  Renderer/VectorMath.h
  Renderer/WhittedRenderer.cpp
  Renderer/WhittedRenderer.h
)
include_directories(Renderer)

set(RAYACCELERATOR_SOURCES
  RayAccelerator/Bvh2.cpp
  RayAccelerator/Bvh2.h
  RayAccelerator/Context.h
  RayAccelerator/Environment.cpp
  RayAccelerator/Environment.h
  RayAccelerator/GroupAllocation.h
  RayAccelerator/Kernels.h
  RayAccelerator/RayAccelerator.cpp
  RayAccelerator/RayAccelerator.h
  RayAccelerator/Scene.cpp
  RayAccelerator/Scene.h
  RayAccelerator/Threading.cpp
  RayAccelerator/Threading.h
  RayAccelerator/ThreadPool.cpp
  RayAccelerator/ThreadPool.h
)
include_directories(RayAccelerator)

find_package(OpenCL REQUIRED)
include_directories(${OpenCL_INCLUDE_DIRS})

find_package(GLUT REQUIRED)
include_directories(${GLUT_INCLUDE_DIR})

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -mavx2 -mfma")
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -march=native")

add_executable(rayaccel ${RENDERER_SOURCES} ${RAYACCELERATOR_SOURCES})
target_link_libraries(rayaccel ${OpenCL_LIBRARIES} ${GLUT_LIBRARIES} -lGL -lpthread -lGLEW -lembree3)
