find_package(MPI REQUIRED)
include_directories(${MPI_INCLUDE_PATH})
vtk_module_test_executable(ParallelIsoTest ParallelIso.cxx)
if(VTK_MPI_MAX_NUMPROCS GREATER 1)
  ExternalData_add_test(VTKData
     NAME ParallelIso-image
     COMMAND ${MPIEXEC} ${MPIEXEC_NUMPROC_FLAG} 2 ${MPIEXEC_PREFLAGS}
     $<TARGET_FILE:ParallelIsoTest>
     -D ${VTK_TEST_DATA_DIR}
     -T ${VTK_TEST_OUTPUT_DIR}
     -V DATA{../Data/Baseline/ParallelIso.cxx.png,:}
     ${VTK_MPI_POSTFLAGS})
endif()
