AC_INIT(MotIV,1.20.0)

# determine RHOME
: ${R_HOME=`R RHOME`}
if test -z "${R_HOME}"; then
  echo "could not determine R_HOME"
  exit 1
fi

## pick up compiler as will be used by R CMD INSTALL/SHLIB
if test -n "${R_HOME}"; then
  CC=`${R_HOME}/bin/R CMD config CC`
  CFLAGS=`${R_HOME}/bin/R CMD config CFLAGS`
fi

## BLAS.
AC_ARG_WITH([blas],
[AC_HELP_STRING([--with-blas],
                [use system gsl BLAS library (if available)])],
[BLAS_LIBS=$with_blas],
[BLAS_LIBS="-lgslcblas"]) # no BLAS libraries found
AC_SUBST([BLAS_LIBS])

PKG_CHECK_MODULES([GSL], [gsl >= 1.6], [HAVEGSL="yes"], [HAVEGSL="no"])
if test "$HAVEGSL" = "no"; then
  AM_PATH_GSL(1.6,[LIBS="${LIBS} -lgsl ${BLAS_LIBS} -lm"],[AC_MSG_ERROR([Cannot find Gnu Scientific Library >=1.6])])
fi

AC_CONFIG_FILES([src/Makevars])
AC_OUTPUT()
