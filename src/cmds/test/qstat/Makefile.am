PROG_ROOT = ../..

if USE_TCLQSTAT
TCLQSTATLIBS = $(MY_TCL_LIBS)
TCLQSTATCFLAGS = $(MY_TCL_INCS)
endif

AM_CFLAGS = -g -DTEST_FUNCTION -I${PROG_ROOT}/ -I${PROG_ROOT}/${PBS_MACH} --coverage ${TCLQSTATCFLAGS}

lib_LTLIBRARIES = libqstat.la

AM_LDFLAGS = @CHECK_LIBS@ ${lib_LTLIBRARIES} ${TCLQSTATLIBS}

check_PROGRAMS = test_qstat

libqstat_la_SOURCES = scaffolding.c ${PROG_ROOT}/qstat.c
libqstat_la_LDFLAGS = @CHECK_LIBS@ -shared

test_qstat_SOURCES = test_qstat.c

check_SCRIPTS = coverage_run.sh

TESTS = ${check_PROGRAMS} coverage_run.sh

coverage_run.sh:
	echo 'cp -p .libs/qstat.gc* . >/dev/null 2>&1' > $@
	echo 'RESULTS=($$(gcov qstat.gcda))' >> $@
	echo 'PARSED_RESULT="TOTALCOV -- $${RESULTS[1]}: Lines($${RESULTS[5]})- $${RESULTS[3]}"' >> $@
	echo 'echo -e "\033[40m\033[1;33m$$PARSED_RESULT\033[0m"' >> $@
	chmod +x $@

CLEANFILES = coverage_run.sh *.gcno *.gcda *.gcov core *.lo
