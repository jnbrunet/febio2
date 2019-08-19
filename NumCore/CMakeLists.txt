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

add_library(${PROJECT_NAME} STATIC ${SOURCE_FILES})

target_include_directories(${PROJECT_NAME} PUBLIC "$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/>")
target_include_directories(${PROJECT_NAME} PUBLIC "$<INSTALL_INTERFACE:include>")