ACLOCAL_AMFLAGS = -I m4
AM_DISTCHECK_CONFIGURE_FLAGS = --enable-relocatable

SUBDIRS = lib src providers tests

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = enchant.pc

EXTRA_DIST =		\
	enchant.pc.in	\
	README 		\
	HACKING 	\
	NEWS 		\
	ChangeLog 	\
	AUTHORS 	\
	COPYING.LIB	\
	m4/gnulib-cache.m4

ALL_SOURCE_FILES = \
	bootstrap.conf \
	configure.ac \
	Makefile.am \
	src/Makefile.am \
	src/*.[chi] \
	providers/Makefile.am \
	providers/*.[ch] \
	providers/*.cpp \
	providers/*.mm

loc:
	cloc --force-lang="Bourne Shell",conf $(ALL_SOURCE_FILES)

release: distcheck
	echo $(VERSION) | grep -v -e - || ( echo "Current commit $(VERSION) is not at a release tag"; exit 1 )
	git diff --exit-code && \
	git tag -a -m "Release tag" "v$(VERSION)" && \
	git push && git push --tags && \
	woger github \
		github_user=AbiWord \
		github_dist_type=source \
		package=$(PACKAGE) \
		version=$(VERSION) \
		dist_type=tar.gz
