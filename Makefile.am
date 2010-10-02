bin_PROGRAMS = gpicker gpicker-simple
gpicker_SOURCES = main.c scorer.c filtration.c vector.c gpicker_xmalloc.c \
 refcounted_str.c refcounted_str.h compiler.h \
 do_with_main_loop.h do_with_main_loop.c \
 loading.h loading.c \
 simple_main.c  gpicker.h \
 filtration.h vector.h scorer.h gpicker_xmalloc.h timing.h inline_qsort.h
gpicker_LDADD = @gtk2_LIBS@ @gthread_LIBS@
AM_CFLAGS = @gtk2_CFLAGS@ @gthread_CFLAGS@
AM_CPPFLAGS = @EXTRA_CPPFLAGS@

# almost NOP. need to avoid error when the same sources are build both
# with libtool and without
gpicker_CFLAGS = $(AM_CFLAGS)

man_MANS = gpicker.1 gpicker-simple.1

EXTRA_DIST = gpicker.el gpicker.vim IDEAS CodingStyle README.osx \
 Makefile.simple debian gpicker.1 gpicker-simple.1

# _SOURCES is only to fool automake not to search for gpicker-simple.c
# Real build rule is simple 'ln'
gpicker_simple_SOURCES = simple_main.c
gpicker-simple: gpicker
	ln -f gpicker gpicker-simple

lib_LTLIBRARIES = libgpicker.la
libgpicker_la_SOURCES = filtration.c filtration.h scorer.c scorer.h \
			vector.h vector.c refcounted_str.c \
			refcounted_str.h inline_qsort.h compiler.h \
			gpicker.h gpicker_xmalloc.h gpicker_xmalloc.c
library_includedir = $(includedir)/gpicker
library_include_HEADERS = gpicker_xmalloc.h filtration.h vector.h \
			  inline_qsort.h gpicker.h compiler.h scorer.h \
			  loading.h
pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = gpicker.pc

if HAVE_CHECK

TESTS = scorer-tests
check_PROGRAMS = scorer-tests
scorer_tests_SOURCES = scorer-tests.c scorer.c
scorer_tests_LDADD = @check_LIBS@
scorer_tests_CFLAGS = $(AM_CFLAGS)

endif # HAVE_CHECK

check-syntax:
	$(COMPILE) -o /dev/null -S ${CHK_SOURCES}
