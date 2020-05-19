cmake_minimum_required(VERSION 3.1)
project(NumCore)


set(SOURCE_FILES
    BIPNSolver.cpp
    BlockMatrix.cpp
    BlockSolver.cpp
    CG_Stokes_Solver.cpp
    CompactMatrix.cpp
    CompactSymmMatrix.cpp
    CompactUnSymmMatrix.cpp
    ConjGradIterSolver.cpp
    CSRMatrix.cpp
    DenseMatrix.cpp
    FGMRES_ILU0_Solver.cpp
    FGMRES_ILUT_Solver.cpp
    FGMRESSolver.cpp
    HypreGMRESsolver.cpp
    LUSolver.cpp
    NumCore.cpp
    PardisoSolver.cpp
    PardisoSolverDL.cpp
    Preconditioner.cpp
    PSLDLTSolver.cpp
    RCICGSolver.cpp
    SchurComplement.cpp
    SchurSolver.cpp
    SkylineMatrix.cpp
    SkylineSolver.cpp
    stdafx.cpp
    StokesPreconditioner.cpp
    StokesSolver.cpp
    SuperLU_MT_Solver.cpp
    SuperLUSolver.cpp
    WSMPSolver.cpp
)

find_package(MKL)
find_package(Eigen3)

if (MKL_FOUND)
    OPTION(FEBIO_WITH_MKL "Use MKL support" ON)
else()
    OPTION(FEBIO_WITH_MKL "Use MKL support" OFF)
endif()

if (NOT PARDISO_LIB)
    option(FEBIO_WITH_PARDISO "Enables Pardiso solver." OFF)
else()
    option(FEBIO_WITH_PARDISO "Enables Pardiso solver." ON)
endif()

if (Eigen3_FOUND)
    OPTION(FEBIO_WITH_EIGEN "Use MKL support" ON)
else()
    OPTION(FEBIO_WITH_EIGEN "Use MKL support" OFF)
endif()

if (FEBIO_WITH_EIGEN_MKL)
    find_package(MKL REQUIRED)
endif()

if (FEBIO_WITH_EIGEN)
    find_package(Eigen3 REQUIRED)
endif()


add_library(${PROJECT_NAME} SHARED ${SOURCE_FILES})
target_link_libraries(${PROJECT_NAME} PUBLIC FECore)

if (FEBIO_WITH_PARDISO)
    if (NOT PARDISO_LIB)
        message(FATAL_ERROR "PARDISO_LIB must be set with the path to the pardiso shared library.")
    else()
        target_link_libraries(${PROJECT_NAME} PUBLIC ${PARDISO_LIB})
        target_compile_definitions(${PROJECT_NAME} PUBLIC PARDISODL)
    endif()
endif()

if (FEBIO_WITH_MKL)
    target_include_directories(${PROJECT_NAME} PUBLIC ${MKL_INCLUDE_DIRS})
    target_link_libraries(${PROJECT_NAME} PUBLIC ${MKL_LIBRARIES})
    target_compile_definitions(${PROJECT_NAME} PUBLIC FEBIO_WITH_MKL)
endif()

if (FEBIO_WITH_EIGEN)
    target_link_libraries(${PROJECT_NAME} PUBLIC Eigen3::Eigen)
    target_compile_definitions(${PROJECT_NAME} PUBLIC FEBIO_WITH_EIGEN)
endif()

target_include_directories(${PROJECT_NAME} PUBLIC "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/>")
target_include_directories(${PROJECT_NAME} PUBLIC "$<INSTALL_INTERFACE:include>")