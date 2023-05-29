

file(GLOB_RECURSE FREETYPE_EXTRA_FILES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} 

	"freetype/include/freetype/*.h"
	"freetype/include/freetype/config/*.h"
	"freetype/include/freetype/internal/*.h"
)

add_library(freetype STATIC 

	freetype/include/ft2build.h
	${FREETYPE_EXTRA_FILES}

	freetype/src/autofit/autofit.c
	freetype/src/base/ftbase.c
	freetype/src/base/ftbbox.c
	freetype/src/base/ftbdf.c
	freetype/src/base/ftbitmap.c
	freetype/src/base/ftcid.c
	freetype/src/base/ftdebug.c
	freetype/src/base/ftfstype.c
	freetype/src/base/ftgasp.c
	freetype/src/base/ftglyph.c
	freetype/src/base/ftgxval.c
	freetype/src/base/ftinit.c
	freetype/src/base/ftmm.c
	freetype/src/base/ftotval.c
	freetype/src/base/ftpatent.c
	freetype/src/base/ftpfr.c
	freetype/src/base/ftstroke.c
	freetype/src/base/ftsynth.c
	freetype/src/base/ftsystem.c
	freetype/src/base/fttype1.c
	freetype/src/base/ftwinfnt.c
	freetype/src/bdf/bdf.c
	freetype/src/bzip2/ftbzip2.c
	freetype/src/cache/ftcache.c
	freetype/src/cff/cff.c
	freetype/src/cid/type1cid.c
	freetype/src/gzip/ftgzip.c
	freetype/src/lzw/ftlzw.c
	freetype/src/pcf/pcf.c
	freetype/src/pfr/pfr.c
	freetype/src/psaux/psaux.c
	freetype/src/pshinter/pshinter.c	
	freetype/src/psnames/psnames.c	
	freetype/src/raster/raster.c	
	freetype/src/sdf/sdf.c
	freetype/src/sfnt/sfnt.c
	freetype/src/smooth/smooth.c	
	freetype/src/truetype/truetype.c	
	freetype/src/type1/type1.c
	freetype/src/type42/type42.c	
	freetype/src/winfonts/winfnt.c

	freetype/src/svg/ftsvg.h
	freetype/src/svg/ftsvg.c
	freetype/src/svg/svg.c
	freetype/src/svg/svgtypes.h
)

target_include_directories(freetype PRIVATE 

	"freetype/include"
)

target_compile_definitions(freetype PRIVATE

	FT2_BUILD_LIBRARY
	_CRT_SECURE_NO_WARNINGS
	_CRT_NONSTDC_NO_WARNINGS
)

set_target_properties(freetype PROPERTIES LINKER_LANGUAGE CXX)




file(GLOB_RECURSE MSDF_GEN_HEADERS RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} 

	"core/*.h"
	"core/*.hpp"
	"ext/*.h"
	"ext/*.hpp"
	"include/*.h"
)

file(GLOB_RECURSE MSDF_GEN_SOURCES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} 

	"core/*.cpp"
	"ext/*.cpp"
	"lib/*.cpp"
)

add_library(msdfgen STATIC 

	${MSDF_GEN_HEADERS}
	${MSDF_GEN_SOURCES}
)

target_include_directories(msdfgen PRIVATE 

	"include"
	"freetype/include"
)

target_compile_definitions(msdfgen PRIVATE

	MSDFGEN_USE_CPP11
)

target_link_libraries(msdfgen PRIVATE 

	freetype
)
