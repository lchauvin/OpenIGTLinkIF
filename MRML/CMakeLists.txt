project(vtkSlicer${MODULE_NAME}ModuleMRML)

#
# See CMake/SlicerMacroBuildModuleLogic.cmake for details
#


set(module_mrml_name "${PROJECT_NAME}")

# The header '${PROJECT_NAME}Export.h' will be automatically configured.
set(module_mrml_export_directive "VTK_SLICER_OPENIGTLINKIF_MODULE_MRML_EXPORT")

# Additional directories to include
set(module_mrml_include_directories
  ${Slicer_Base_INCLUDE_DIRS}
  ${CMAKE_CURRENT_SOURCE_DIR}/../Logic
  ${CMAKE_CURRENT_BINARY_DIR}/../Logic
  )

# Source files
set(module_mrml_SRCS
  vtkIGTLCircularBuffer.cxx
  vtkIGTLToMRMLBase.cxx
  vtkIGTLToMRMLImage.cxx
  vtkIGTLToMRMLLinearTransform.cxx
  vtkIGTLToMRMLPosition.cxx
  vtkMRMLIGTLConnectorNode.cxx
  )

if(OpenIGTLink_PROTOCOL_VERSION EQUAL 2)
  list(APPEND module_mrml_SRCS
    vtkMRMLIGTLQueryNode.cxx
    vtkMRMLImageMetaListNode.cxx
    vtkMRMLLabelMetaListNode.cxx
    vtkMRMLPointMetaListNode.cxx
    vtkIGTLToMRMLPointMetaList.cxx
    vtkIGTLToMRMLImageMetaList.cxx
    vtkIGTLToMRMLLabelMetaList.cxx
    vtkIGTLToMRMLTrackingData.cxx
    vtkMRMLIGTLTrackingDataQueryNode.cxx
    vtkMRMLIGTLTrackingDataBundleNode.cxx
    )
endif()

# Additional Target libraries
set(module_mrml_target_libraries
  ${OpenIGTLink_LIBRARIES}
  ${MRML_LIBRARIES}
  SlicerBaseLogic
  )

SlicerMacroBuildModuleMRML(
  NAME ${module_mrml_name}
  EXPORT_DIRECTIVE ${module_mrml_export_directive}
  INCLUDE_DIRECTORIES ${module_mrml_include_directories}
  SRCS ${module_mrml_SRCS}
  TARGET_LIBRARIES ${module_mrml_target_libraries}
  )
