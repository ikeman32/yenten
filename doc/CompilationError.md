Error: /usr/local/include/boost/thread/pthread/thread_data.hpp:252: undefined reference to `boost::this_thread::hidden::sleep_for(timespec const&)'

Older versions of boost do not appear to be compatible with the bitcoin code base and the newer versions may not be available in some linux distros such as Ubuntu 16.04. The solution is to manually compile and set the boots library path when executing ./configure.

Procedure:
1) Download boost 1_64_0 from here: https://www.boost.org/users/history/version_1_64_0.html
2) Extract the archive and open a terminal from withing the boost folder.
3) Type ./bootstrap.sh
4) Type ./b2
5) Type sudo ./bjam  install

Note: Step 5 may not be neccessary but it doesn't really hurt to do it.

6) Check test_bitcoin.cpp

test_bitcoin.cpp can be found in /src/test This source code has an #include declaration that is incompatable with bost 1_64_0. The old include is: #include <boost/test/unit_test.hpp>. Change it to #include <boost/test/included/unit_test.hpp>

7) Navigate to the yenten folder and open a terminal from there Type ./autogen.sh
8) Type ./configure --with-boost-libdir=/pathto/boost_1_64_0/stage/lib
9) Type make

