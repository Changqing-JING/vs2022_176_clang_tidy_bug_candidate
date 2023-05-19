project(C1)

aux_source_directory(${CMAKE_CURRENT_LIST_DIR} sourceFiles)

add_library(${PROJECT_NAME} ${sourceFiles})

set_target_properties(${PROJECT_NAME} PROPERTIES
        VS_GLOBAL_RunCodeAnalysis true
        VS_GLOBAL_EnableMicrosoftCodeAnalysis false
        VS_GLOBAL_EnableClangTidyCodeAnalysis true
)