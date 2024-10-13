AC_INIT([ceferino], [0.97.8])
AC_PREREQ([2.69])  # Ensure a modern version of Autoconf is used
AM_INIT_AUTOMAKE([-Wall -Werror foreign])

AC_CONFIG_HEADERS([config.h])

AC_USE_SYSTEM_EXTENSIONS

AC_PROG_CXX

# Initialize gettext support with version
AM_GNU_GETTEXT([external])
AM_GNU_GETTEXT_VERSION([0.21])  # Specify the minimum required gettext version
AC_SUBST(localedir)
ALL_LINGUAS="es fr ca"

GETTEXT_PACKAGE="ceferino"
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED([GETTEXT_PACKAGE], ["${GETTEXT_PACKAGE}"], [gettext domain])

# Detect SDL using sdl-config
AC_PATH_PROG([SDL_CONFIG], [sdl-config], [no])
if test "$SDL_CONFIG" = "no"; then
    AC_MSG_ERROR([sdl-config not found! Make sure SDL 1.2 is installed.])
fi

# Extract SDL compiler and linker flags
SDL_CFLAGS=`$SDL_CONFIG --cflags`
SDL_LIBS=`$SDL_CONFIG --libs`

AC_SUBST(SDL_CFLAGS)
AC_SUBST(SDL_LIBS)

# Check for SDL_image library
AC_CHECK_LIB([SDL_image], [IMG_Load], [], [
    AC_MSG_ERROR([SDL_image library not found! Install libsdl-image1.2-dev.])
])

# Check for SDL_mixer library
AC_CHECK_LIB([SDL_mixer], [Mix_OpenAudio], [], [
    AC_MSG_ERROR([SDL_mixer library not found! Install libsdl-mixer1.2-dev.])
])

# Append SDL_image and SDL_mixer to SDL_LIBS
SDL_LIBS="$SDL_LIBS -lSDL_image -lSDL_mixer"
AC_SUBST(SDL_LIBS)

# Specify configuration files to generate (removed intl/Makefile)
AC_CONFIG_FILES([
    Makefile
    src/Makefile
    data/Makefile
    po/Makefile.in
    data/ima/Makefile
    data/levels/Makefile
    data/music/Makefile
    data/sounds/Makefile
])
AC_OUTPUT
