cmake_minimum_required(VERSION 2.8)
project(armips) 

if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread -std=c++11")
endif()

if(MSVC)
	add_definitions(-DUNICODE -D_UNICODE)
elseif(MINGW)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -municode")
	set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -static")
endif()

include_directories(.)

add_executable(armips
	Main/main.cpp
	Main/Tests.cpp
	Main/Tests.h
	stdafx.cpp
	stdafx.h

	Util/ByteArray.cpp
	Util/ByteArray.h
	Util/CRC.cpp
	Util/CRC.h
	Util/EncodingTable.cpp
	Util/EncodingTable.h
	Util/FileClasses.cpp
	Util/FileClasses.h
	Util/Util.cpp
	Util/Util.h
	
	Core/ELF/ElfTypes.h
	Core/ELF/ElfRelocator.cpp
	Core/ELF/ElfRelocator.h
	Core/ELF/ElfFile.cpp
	Core/ELF/ElfFile.h
	Core/Assembler.cpp
	Core/Assembler.h
	Core/Common.cpp
	Core/Common.h
	Core/Expression.cpp
	Core/Expression.h
	Core/ExpressionFunctions.cpp
	Core/ExpressionFunctions.h
	Core/FileManager.cpp
	Core/FileManager.h
	Core/Misc.cpp
	Core/Misc.h
	Core/SymbolData.cpp
	Core/SymbolData.h
	Core/SymbolTable.cpp
	Core/SymbolTable.h
	
	Commands/CAssemblerCommand.cpp
	Commands/CAssemblerCommand.h
	Commands/CAssemblerLabel.cpp
	Commands/CAssemblerLabel.h
	Commands/CDirectiveArea.cpp
	Commands/CDirectiveArea.h
	Commands/CDirectiveConditional.cpp
	Commands/CDirectiveConditional.h
	Commands/CDirectiveData.cpp
	Commands/CDirectiveData.h
	Commands/CDirectiveFile.cpp
	Commands/CDirectiveFile.h
	Commands/CDirectiveMessage.cpp
	Commands/CDirectiveMessage.h
	Commands/CommandSequence.cpp
	Commands/CommandSequence.h

	Archs/Architecture.h
	Archs/Architecture.cpp

	Archs/ARM/Arm.cpp
	Archs/ARM/Arm.h
	Archs/ARM/ArmOpcodes.cpp
	Archs/ARM/ArmOpcodes.h
	Archs/ARM/ArmParser.cpp
	Archs/ARM/ArmParser.h
	Archs/ARM/ArmRelocator.cpp
	Archs/ARM/ArmRelocator.h
	Archs/ARM/CArmInstruction.cpp
	Archs/ARM/CArmInstruction.h
	Archs/ARM/CThumbInstruction.cpp
	Archs/ARM/CThumbInstruction.h
	Archs/ARM/Pool.cpp
	Archs/ARM/Pool.h
	Archs/ARM/ThumbOpcodes.cpp
	Archs/ARM/ThumbOpcodes.h

	Archs/MIPS/CMipsInstruction.cpp
	Archs/MIPS/CMipsInstruction.h
	Archs/MIPS/Mips.cpp
	Archs/MIPS/Mips.h
	Archs/MIPS/MipsElfFile.cpp
	Archs/MIPS/MipsElfFile.h
	Archs/MIPS/MipsMacros.cpp
	Archs/MIPS/MipsMacros.h
	Archs/MIPS/MipsOpcodes.cpp
	Archs/MIPS/MipsOpcodes.h
	Archs/MIPS/MipsParser.cpp
	Archs/MIPS/MipsParser.h
	Archs/MIPS/PsxRelocator.cpp
	Archs/MIPS/PsxRelocator.h
	
	Parser/DirectivesParser.cpp
	Parser/DirectivesParser.h
	Parser/ExpressionParser.cpp
	Parser/ExpressionParser.h
	Parser/Parser.cpp
	Parser/Parser.h
	Parser/Tokenizer.cpp
	Parser/Tokenizer.h
	
	ext/tinyformat/tinyformat.h
)

if(WIN32)
	target_link_libraries(armips shlwapi)
endif(WIN32)
