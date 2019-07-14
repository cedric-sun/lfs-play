GNU toolchain is crazy.

For most application layer developers like me, GNU software source tarballs are bunches of esoteric scripts (autoconf, m4, etc.) and you never figure out how they work. When a option is not recognized by the top level './configure' script (e.g. refuse to work with '--enable-option-checking=fatal') which is supposed to be the user interface to be invoked directly from the cli, it doesn't mean the option is not recognized by those 'subdir/configure' scripts. And yes the top level configure will pass those options to configure(s) in subdirectory. Unless you are the developer of the GNU package yourself or you've read all the README, INSTALL, and 'configure --help' thoroughly in every single directory, you'll never figure out which option is useful for which part of the building process.

Now this is a pain in the ass.

### binutils
../configure --prefix=/tools            \
             --with-sysroot=$LFS        \
             --with-lib-path=/tools/lib \
             --target=$LFS_TGT          \
             --disable-nls              \
             --disable-werror

--with-sysroot=$LFS
	Used by ld etc. Search for usr/lib et al within $LFS.
	Maybe this is useful since this binutils build will later be used for other stuff.
	Will there be $LFS/usr/lib in the future?
	Is this combined with --with-lib-path: $LFS/tools/lib?
	
--with-lib-path=/tools/lib
	set default LIB_PATH. Described in ld/README, this option is useful when making a cross-linker.
