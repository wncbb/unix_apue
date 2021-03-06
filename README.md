# APUE

#

```
cd apue.3e
make
cp ./include/apue.h /usr/local/include/  
cp ./lib/libapue.a  /usr/local/lib/
Ctrl+Shift+P  (input C/C++ Edit Configurations)
```
run "gcc -v -E -x c++ -"
copy those below to includePath
```
                "/usr/local/include",
                "/Library/Developer/CommandLineTools/usr/bin/../include/c++/v1",
                "/Library/Developer/CommandLineTools/usr/lib/clang/12.0.0/include",
                "/Library/Developer/CommandLineTools/SDKs/MacOSX10.15.sdk/usr/include",
                "/Library/Developer/CommandLineTools/usr/include",
                "/Library/Developer/CommandLineTools/SDKs/MacOSX10.15.sdk/System/Library/Frameworks"
```

add a file 
cat /usr/local/include/apueerror.h
```
#include "apue.h"
#include <errno.h>      /* for definition of errno */
#include <stdarg.h>     /* ISO C variable aruments */

static void err_doit(int, int, const char *, va_list);

/*
* Nonfatal error related to a system call.
* Print a message and return.
*/
void
err_ret(const char *fmt, ...)
{
    va_list     ap;

    va_start(ap, fmt);
    err_doit(1, errno, fmt, ap);
    va_end(ap);
}

/*
* Fatal error related to a system call.
* Print a message and terminate.
*/
void
err_sys(const char *fmt, ...)
{
    va_list     ap;

    va_start(ap, fmt);
    err_doit(1, errno, fmt, ap);
    va_end(ap);
    exit(1);
}

/*
* Fatal error unrelated to a system call.
* Error code passed as explict parameter.
* Print a message and terminate.
*/
void
err_exit(int error, const char *fmt, ...)
{
    va_list     ap;

    va_start(ap, fmt);
    err_doit(1, error, fmt, ap);
    va_end(ap);
    exit(1);
}

/*
* Fatal error related to a system call.
* Print a message, dump core, and terminate.
*/
void
err_dump(const char *fmt, ...)
{
    va_list     ap;

    va_start(ap, fmt);
    err_doit(1, errno, fmt, ap);
    va_end(ap);
    abort();        /* dump core and terminate */
    exit(1);        /* shouldn't get here */
}

/*
* Nonfatal error unrelated to a system call.
* Print a message and return.
*/
void
err_msg(const char *fmt, ...)
{
    va_list     ap;

    va_start(ap, fmt);
    err_doit(0, 0, fmt, ap);
    va_end(ap);
}

/*
* Fatal error unrelated to a system call.
* Print a message and terminate.
*/
void
err_quit(const char *fmt, ...)
{
    va_list     ap;

    va_start(ap, fmt);
    err_doit(0, 0, fmt, ap);
    va_end(ap);
    exit(1);
}

/*
* Print a message and return to caller.
* Caller specifies "errnoflag".
*/
static void
err_doit(int errnoflag, int error, const char *fmt, va_list ap)
{
    char    buf[MAXLINE];
   vsnprintf(buf, MAXLINE, fmt, ap);
   if (errnoflag)
       snprintf(buf+strlen(buf), MAXLINE-strlen(buf), ": %s",
         strerror(error));
   strcat(buf, " ");
   fflush(stdout);     /* in case stdout and stderr are the same */
   fputs(buf, stderr);
   fflush(NULL);       /* flushes all stdio output streams */
}

```

put include "apueerror.h" to every c file containing main function.

## ??????

* [????????????](apue.3e/)
* [Chapter 1: UNIX ????????????](Chapter-01/)
* [Chapter 2: UNIX ???????????????](Chapter-02/)
* [Chapter 3: ?????? I/O](Chapter-03/)
* [Chapter 4: ???????????????](Chapter-04/)
* [Chapter 5: ?????? I/O ???](Chapter-05/)
* [Chapter 6: ???????????????????????????](Chapter-06/)
* [Chapter 7: ????????????](Chapter-07/)
* [Chapter 8: ????????????](Chapter-08/)
* [Chapter 9: ????????????](Chapter-09/)
* [Chapter 10: ??????](Chapter-10/)
* [Chapter 11: ??????](Chapter-11/)
* [Chapter 12: ????????????](Chapter-12/)
* [Chapter 13: ????????????](Chapter-13/)
* [Chapter 14: ?????? I/O](Chapter-14/)
* [Chapter 15: ???????????????](Chapter-15/)
* [Chapter 16: ?????? IPC: ?????????](Chapter-16/)
* [Chapter 17: ?????????????????????](Chapter-17/)