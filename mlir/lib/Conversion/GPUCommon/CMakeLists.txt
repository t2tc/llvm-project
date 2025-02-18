if (MLIR_ENABLE_CUDA_CONVERSIONS)
  set(NVPTX_LIBS
    NVPTXCodeGen
    NVPTXDesc
    NVPTXInfo
  )
endif()

if (MLIR_ENABLE_ROCM_CONVERSIONS)
  set(AMDGPU_LIBS
    AMDGPUCodeGen
    AMDGPUDesc
    AMDGPUInfo
  )
endif()

add_mlir_conversion_library(MLIRGPUToGPURuntimeTransforms
  GPUToLLVMConversion.cpp
  GPUOpsLowering.cpp

  DEPENDS
  MLIRConversionPassIncGen
  intrinsics_gen

  LINK_COMPONENTS
  Core
  MC
  ${AMDGPU_LIBS}
  ${NVPTX_LIBS}

  LINK_LIBS PUBLIC
  MLIRArithmeticToLLVM
  MLIRAsyncToLLVM
  MLIRControlFlowToLLVM
  MLIRGPUTransforms
  MLIRIR
  MLIRLLVMCommonConversion
  MLIRLLVMIR
  MLIRMemRefToLLVM
  MLIRPass
  MLIRSupport
  MLIRStandardToLLVM
  MLIRVectorToLLVM
)
