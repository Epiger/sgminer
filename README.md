# sgminer

This is a fork of the Original sgminer for all who ran into 
problems at installing sgminer on Windows. 
For all who have still Problems please open an Issue

## Installing on Windows

#### Install MinGW
First of all you need to install MinGW "is a minimalist development environment 
for native Microsoft Windows applications" 
**Go to**: http://www.mingw.org/wiki/Getting_Started <br>
and Click on the Link _mingw-get-setup.exe_ to Download the Installer.
If you will be asked what packages you want to install just select all of them.
<br>


#### Install Msys
Open the MinGW Installation Manager and install the Msys package
after the installation is done open the Msys shell its located at
the installation path of MinGW mostly _C:\MinGW\msys\1.0\msys.bat_
<br>

#### Install Some other Packages
Make sure you installed:
* **automake**
* **autoconf**
* **gcc**
* **libtool**
* **make**
* **mingw-get**
The packages should look like **msys-XXXX** or **mingw32-XXXX**
if the exits both msys-packagename and mingw32-packagename install both
to be safe. _To install click on the top left corner on Installation and Apply Changes._

#### Installing more Packages
Open the Msys-shell mostly _C:\MinGW\msys\1.0\msys.bat_ and type
```
mingw-get install mingw32-libpdcurses
mingw-get install mingw32-pdcurses

mingw-get upgrade 'gcc=6.3.*'
```
to get the right gcc compiler you can use newer versions too but 
I only tested it with version 6.3.0
<br>

#### Download sgminer version 4.2.2
**Go to this link:** https://github.com/Epiger/sgminer/releases/tag/4.2.2 <br>
and click on _Source code (zip)_. You can Download other version too but I
modified at this point in time only the version 4.2.2
<br>

#### Download AMD APP SDK
**Go to this link:** http://developer.amd.com/amd-accelerated-parallel-processing-app-sdk/ <br>
and Download the AMD APP SDK and install it.
Go to the AMD APP SDK installation folder and copy the **entry of the include** folder
into the **C:/MinGW/include folder** and **C:\Program Files (x86)\AMD APP\lib\x86\libOpenCL.a** to **C:\MinGW\lib**
<br>

#### And Maybe Download AMD ADL SDK (optional)
**Go to this link:** http://developer.amd.com/display-library-adl-sdk/ <br>
and Download the AMD ADL SDK. You dont need to install it but you should copy
the files: **adl\_defines.h**, **adl\_sdk.h**, **adl\_structures.h** into the 
**ADL\_SDK** folder in your sgminer directory.
<br>

#### Install GTK-WIN
Install GTK-WIN **from this url**: http://sourceforge.net/projects/gtk-win/ <br>
and copy **libglib-2.0-0.dll** and **intl.dll** from _C:\Program Files\gtk2-runtime\bin_
to _C:\MinGW\bin_
<br>

#### Download PKG-config
**Go to this url**: http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/ <br>
and download _pkg-config\_0.26-1\_win32.zip_ also download
_pkg-config-dev\_0.26-1\_win32.zip_.
Copy **pkg-config.exe** from the normal pkg-config to _C:\MinGW\bin_
and Copy **pkg.m4** from the dev pkg-config from _share/aclocal_ to
C:\MinGW\share\aclocal
<br>

#### Install libcurl
**Go to this URL**: https://curl.haxx.se/download/ <br>
and download **curl-7.25.0.zip** you can also download other
versions but i tested it only with this version.
Extract the zip file into your msys working directory
mostly _C:\MinGW\msys\1.0\home\[USERNAME]\\_ then open the
msys shell and type:
```
export "PKG\_CONFIG\_PATH=/usr/local/lib/pkgconfig"
cd [CURL DIRECTORY probably curl-7.25.0]
export "CFLAGS=-I/usr/local/include"
export "LDFLAGS=-L/usr/local/lib"
./configure
make
make install-strip
```
now libcurl should be installed if the compiler throws issues
please repeat this process or report this in the issues.
<br>

#### Finally make sgminer
Go inside your sgminer download folder by typing:
```
cd [FOLDERNAME]
# and run:
autoreconf -fvi
CFLAGS="-O2 -msse2" ./configure
# after this command it should show you a overview about the packages you installed earlier
make
```

#### Make a standalone sgminer Directory
Make a new Folder and copy this files into it:
* **kernel folder**       _from sgminer directory_
* **sgminer.exe**         _from sgminer directory_
* **libcurl-4.dll**       _from C:\MinGW\msys\1.0\local\bin_
* **libeay32.dll**        _from C:\MinGW\msys\1.0\local\bin_
* **ssleay32.dll**        _from C:\MinGW\msys\1.0\local\bin_
* **libgcc_s_dw2-1.dll**  _from C:\MinGW\bin_
* **libpdcurses.dll**     _from C:\MinGW\bin_
* **pthreadGC-3.dll**     _from C:\MinGW\bin_

but before you can run sgminer you have to make a **start.bat** file
Open an editor and type:
```
setx GPU_MAX_ALLOC_PERCENT 100
setx GPU_USE_SYNC_OBJECTS 1
sgminer.exe -o [STRATUM POOL URL] -u [USERNAME].[WORKERID] -p [PASSWORD] -I 13 -g 1 --thread-concurrency 10000
PAUSE
```
and save it as **start.bat**. <br>
Now you can copy the folder you maked everywere you want and run sgminer by running **start.bat**.

<br>

#### Want to Know more about sgminer checkout the doc folder

<br>

### Credits

**here is my Litecoin address if you want to donate** <br>
LTC: LhWTXmdU8nLAdZLSVxoirQpBDXWj88fMqR

> Found some spelling mistakes please contact me.

**And Check out the Original Repository**: https://github.com/sgminer-dev/sgminer <br>
_Here starts the Original Readme.md_

## Introduction

This is a multi-threaded multi-pool GPU miner with ATI GPU monitoring,
(over)clocking and fanspeed support for scrypt-based cryptocurrency. It is
based on cgminer by Con Kolivas (ckolivas), which is in turn based on
cpuminer by Jeff Garzik (jgarzik).

**releases**: https://github.com/sgminer-dev/sgminer/releases

**git tree**: https://github.com/sgminer-dev/sgminer

**bugtracker**: https://github.com/sgminer-dev/sgminer/issues

**irc**: `#sgminer` and `#sgminer-dev` on freenode

**mailing lists**: https://sourceforge.net/p/sgminer/mailman/

License: GPLv3.  See `COPYING` for details.


## Documentation

Documentation is available in directory `doc`. It is organised by topics:

* `API` for the RPC API specification;
* `configuration.md` for (largely incomplete) detailed information on all
  configuration options;
* `FAQ.md` for frequently asked questions;
* `GPU` for semi-obsolete information on GPU configuration options and mining
  SHA256d-based coins;
* `kernel.md` for OpenCL kernel-related information, including development
  procedure;
* `MINING.md` for how to find the right balance in GPU configuration to mine
  Scrypt-based coins efficiently;
* `windows-build.txt` for information on how to build on Windows.

Note that **most of the documentation is outdated or incomplete**. If
you want to contribute, fork this repository, update as needed, and
submit a pull request.


## Building

### Dependencies

Mandatory:

* [curl dev library](http://curl.haxx.se/libcurl/) - `libcurl4-openssl-dev` on Debian
* [pkg-config](http://www.freedesktop.org/wiki/Software/pkg-config)
* [libtool](http://www.gnu.org/software/libtool/)
* [AMD APP SDK](http://developer.amd.com/tools-and-sdks/heterogeneous-computing/amd-accelerated-parallel-processing-app-sdk/downloads/)	- available under various names as a package on different GNU/Linux distributions

Optional:

* curses dev library - `libncurses5-dev` on Debian or `libpdcurses` on WIN32, for text user interface
* [AMD ADL SDK](http://developer.amd.com/tools-and-sdks/graphics-development/display-library-adl-sdk/) - version 6, required for ATI GPU monitoring & clocking

If building from git:

* autoconf
* automake

sgminer-specific configuration options:

    --disable-adl           Override detection and disable building with adl
	--disable-adl-checks
    --without-curses        Do not compile support for curses TUI

#### Debian Example

    apt-get install libcurl4-openssl-dev pkg-config libtool libncurses5-dev
AMD APP SDK and AMD ADL SDK must be downloaded from the amd websites.

### *nix build instructions

If needed, place include headers (`*.h` files) from `ADL_SDK_*<VERSION>*.zip` in `sgminer/ADL_SDK`.

Then:

    git submodule init
    git submodule update
    autoreconf -i
    CFLAGS="-O2 -Wall -march=native -std=gnu99" ./configure <options>
    make

To compile a version that can be used accross machines, remove
`-march=native`.

To compile a debug version, replace `-O2` with `-ggdb`.

Depending on your environment, replace `-std=gnu99` with `-std=c99`.

Systemwide installation is optional. You may run `sgminer` from the build
directory directly, or `make install` if you wish to install
`sgminer` to a system location or a location you specified with `--prefix`.

### Windows build instructions

See `doc/windows-build.txt` for MinGW compilation and cross-compiation,
`doc/cygwin-build.txt` for building using Cygwin, or use the provided
`winbuild` Microsoft Visual Studio project (tested on MSVS2010), with
instructions in `winbuild/README.txt`.


## Basic Usage

**WARNING**: documentation below this point has not been updated since the
fork.

After saving configuration from the menu, you do not need to give sgminer
any arguments and it will load your configuration.

Any configuration file may also contain a single

    "include" : "filename"

to recursively include another configuration file.

Writing the configuration will save all settings from all files in the
output.

Single pool:

sgminer -o http://pool:port -u username -p password

Multiple pools:

sgminer -o http://pool1:port -u pool1username -p pool1password -o http://pool2:port -u pool2usernmae -p pool2password

Single pool with a standard http proxy, regular desktop:

sgminer -o "http:proxy:port|http://pool:port" -u username -p password

Single pool with a socks5 proxy, regular desktop:

sgminer -o "socks5:proxy:port|http://pool:port" -u username -p password

Single pool with stratum protocol support:

sgminer -o stratum+tcp://pool:port -u username -p password

The list of proxy types are:
 http:    standard http 1.1 proxy
 http0:   http 1.0 proxy
 socks4:  socks4 proxy
 socks5:  socks5 proxy
 socks4a: socks4a proxy
 socks5h: socks5 proxy using a hostname

If you compile sgminer with a version of CURL before 7.19.4 then some of
the above will not be available. All are available since CURL version
7.19.4.

If you specify the --socks-proxy option to sgminer, it will only be
applied to all pools that don't specify their own proxy setting like
above.

For more advanced usage , run `sgminer --help`.

See `doc/GPU` for more information regarding GPU mining and
`doc/SCRYPT` for more information regarding Scrypt mining.


## Runtime usage

The following options are available while running with a single keypress:

[P]ool management [G]PU management [S]ettings [D]isplay options [Q]uit

P gives you:

Current pool management strategy: Failover
[F]ailover only disabled
[A]dd pool [R]emove pool [D]isable pool [E]nable pool
[C]hange management strategy [S]witch pool [I]nformation


S gives you:

[Q]ueue: 1
[S]cantime: 60
[E]xpiry: 120
[W]rite config file
[C]gminer restart


D gives you:

[N]ormal [C]lear [S]ilent mode (disable all output)
[D]ebug:off
[P]er-device:off
[Q]uiet:off
[V]erbose:off
[R]PC debug:off
[W]orkTime details:off
co[M]pact: off
[L]og interval:5


Q quits the application.


G gives you something like:

GPU 0: [124.2 / 191.3 Mh/s] [A:77  R:33  HW:0  U:1.73/m  WU 1.73/m]
Temp: 67.0 C
Fan Speed: 35% (2500 RPM)
Engine Clock: 960 MHz
Memory Clock: 480 Mhz
Vddc: 1.200 V
Activity: 93%
Powertune: 0%
Last initialised: [2011-09-06 12:03:56]
Thread 0: 62.4 Mh/s Enabled ALIVE
Thread 1: 60.2 Mh/s Enabled ALIVE

[E]nable [D]isable [R]estart GPU [C]hange settings
Or press any other key to continue


The running log shows output like this:

 [2012-10-12 18:02:20] Accepted f0c05469 Diff 1/1 GPU 0 pool 1
 [2012-10-12 18:02:22] Accepted 218ac982 Diff 7/1 GPU 1 pool 1
 [2012-10-12 18:02:23] Accepted d8300795 Diff 1/1 GPU 3 pool 1
 [2012-10-12 18:02:24] Accepted 122c1ff1 Diff 14/1 GPU 1 pool 1

The 8 byte hex value are the 2nd 8 bytes of the share being submitted to the
pool. The 2 diff values are the actual difficulty target that share reached
followed by the difficulty target the pool is currently asking for.

The output line shows the following:
(5s):1713.6 (avg):1707.8 Mh/s | A:729  R:8  HW:0  WU:22.53/m

Each column is as follows:
5s:  A 5 second exponentially decaying average hash rate
avg: An all time average hash rate
A:  The total difficulty of Accepted shares
R:  The total difficulty of Rejected shares
HW:  The number of HardWare errors
WU:  The Work Utility defined as the number of diff1 shares work / minute
     (accepted or rejected).

 GPU 1: 73.5C 2551RPM | 427.3/443.0Mh/s | A:8 R:0 HW:0 WU:4.39/m

Each column is as follows:
Temperature (if supported)
Fanspeed (if supported)
A 5 second exponentially decaying average hash rate
An all time average hash rate
The total difficulty of accepted shares
The total difficulty of rejected shares
The number of hardware erorrs
The work utility defined as the number of diff1 shares work / minute

The sgminer status line shows:
 ST: 1  SS: 0  NB: 1  LW: 8  GF: 1  RF: 1

ST is STaged work items (ready to use).
SS is Stale Shares discarded (detected and not submitted so don't count as rejects)
NB is New Blocks detected on the network
LW is Locally generated Work items
GF is Getwork Fail Occasions (server slow to provide work)
RF is Remote Fail occasions (server slow to accept work)

The block display shows:
Block: 0074c5e482e34a506d2a051a...  Started: [17:17:22]  Best share: 2.71K

This shows a short stretch of the current block, when the new block started,
and the all time best difficulty share you've found since starting sgminer
this time.


## Multipool

### Failover strategies

A number of different strategies for dealing with multipool setups are
available. Each has their advantages and disadvantages so multiple strategies
are available by user choice, as per the following list:

#### Failover

The default strategy is failover. This means that if you input a number of
pools, it will try to use them as a priority list, moving away from the 1st
to the 2nd, 2nd to 3rd and so on. If any of the earlier pools recover, it will
move back to the higher priority ones.

#### Round robin

This strategy only moves from one pool to the next when the current one falls
idle and makes no attempt to move otherwise.

#### Rotate

This strategy moves at user-defined intervals from one active pool to the next,
skipping pools that are idle.

#### Load balance

This strategy sends work to all the pools on a quota basis. By default, all
pools are allocated equal quotas unless specified with --quota. This
apportioning of work is based on work handed out, not shares returned so is
independent of difficulty targets or rejected shares. While a pool is disabled
or dead, its quota is dropped until it is re-enabled. Quotas are forward
looking, so if the quota is changed on the fly, it only affects future work.
If all pools are set to zero quota or all pools with quota are dead, it will
fall back to a failover mode. See quota below for more information.

The failover-only flag has special meaning in combination with load-balance
mode and it will distribute quota back to priority pool 0 from any pools that
are unable to provide work for any reason so as to maintain quota ratios
between the rest of the pools.

#### Balance

This strategy monitors the amount of difficulty 1 shares solved for each pool
and uses it to try to end up doing the same amount of work for all pools.


### Quotas

The load-balance multipool strategy works off a quota based scheduler. The
quotas handed out by default are equal, but the user is allowed to specify any
arbitrary ratio of quotas. For example, if all the quota values add up to 100,
each quota value will be a percentage, but if 2 pools are specified and pool0
is given a quota of 1 and pool1 is given a quota of 9, pool0 will get 10% of
the work and pool1 will get 90%. Quotas can be changed on the fly by the API,
and do not act retrospectively. Setting a quota to zero will effectively
disable that pool unless all other pools are disabled or dead. In that
scenario, load-balance falls back to regular failover priority-based strategy.
While a pool is dead, it loses its quota and no attempt is made to catch up
when it comes back to life.

To specify quotas on the command line, pools should be specified with a
semicolon separated --quota(or -U) entry instead of --url. Pools specified with
--url are given a nominal quota value of 1 and entries can be mixed.

For example:
--url poola:porta -u usernamea -p passa --quota "2;poolb:portb" -u usernameb -p passb
Will give poola 1/3 of the work and poolb 2/3 of the work.

Writing configuration files with quotas is likewise supported. To use
the above quotas in a configuration file they would be specified thus:

    "pools" : [
        {
                "url" : "poola:porta",
                "user" : "usernamea",
                "pass" : "passa"
        },
        {
                "quota" : "2;poolb:portb",
                "user" : "usernameb",
                "pass" : "passb"
        }
    ]


### Extra File Configuration

If you want to store a number of pools in your configuration file, but
don't always want them automatically enabled at start up (or restart),
then the "state" option with a value of "disabled" can be used:

    "pools" : [
        {
                "url" : "poola:porta",
                "user" : "usernamea",
                "pass" : "passa"
        },
        {
                "quota" : "2;poolb:portb",
                "user" : "usernameb",
                "pass" : "passb",
                "state" : "disabled"
        }
    ]

It is then trivial to change the "state" setting to "enabled" in the
configuration file at anytime and then restart the miner (see below).
You can enable the pool whilst the miner is still running ('p' followed
by 'e' followed by pool number) - but the pool will still be disabled on
restart if the config file is not changed.

"state" can also be set to "hidden". This allows the json file to
contain a large number of pools, of which some could be automatically
culled at start up. This makes it easy to swap pools in and out of the
runtime selection, without having a large list of pools cluttering up
the display.

    "pools" : [
        {
                "poolname" : "Main Pool",
                "url" : "poola:porta",
                "user" : "usernamea",
                "pass" : "passa",
                "state" : "disabled"
        },
        {
                "poolname" : "Joe's Weekend Pool",
                "quota" : "2;poolb:portb",
                "user" : "usernameb",
                "pass" : "passb",
                "state" : "hidden"
        }
    ]

These options are considered experimental and therefore will NOT be
created when the 'Write config file' option is used ('s' followed by
'w').

A restart of the miner ('s' followed by 'c') will reload the config
file and any changes that may have been made.


## Logging

sgminer will log to stderr if it detects stderr is being redirected to a
file. To enable logging simply append `2>logfile.txt` to your command line
and `logfile.txt` will contain all debug output unless you set `debug-log`
to `false`, in which case it will only contain output at the log level you
specified (notice by default).

There is also the -m option on Linux which will spawn a command of your choice
and pipe the output directly to that command.

The WorkTime details 'debug' option adds details on the end of each line
displayed for Accepted or Rejected work done. An example would be:

 <-00000059.ed4834a3 M:X D:1.0 G:17:02:38:0.405 C:1.855 (2.995) W:3.440 (0.000) S:0.461 R:17:02:47

The first 2 hex codes are the previous block hash, the rest are reported in
seconds unless stated otherwise:
The previous hash is followed by the getwork mode used M:X where X is one of
P:Pool, T:Test Pool, L:LP or B:Benchmark,
then D:d.ddd is the difficulty required to get a share from the work,
then G:hh:mm:ss:n.nnn, which is when the getwork or LP was sent to the pool and
the n.nnn is how long it took to reply,
followed by 'O' on it's own if it is an original getwork, or 'C:n.nnn' if it was
a clone with n.nnn stating how long after the work was recieved that it was cloned,
(m.mmm) is how long from when the original work was received until work started,
W:n.nnn is how long the work took to process until it was ready to submit,
(m.mmm) is how long from ready to submit to actually doing the submit, this is
usually 0.000 unless there was a problem with submitting the work,
S:n.nnn is how long it took to submit the completed work and await the reply,
R:hh:mm:ss is the actual time the work submit reply was received

If you start sgminer with the --sharelog option, you can get detailed
information for each share found. The argument to the option may be "-" for
standard output (not advisable with the ncurses UI), any valid positive number
for that file descriptor, or a filename.

To log share data to a file named "share.log", you can use either:
./sgminer --sharelog 50 -o xxx -u yyy -p zzz 50>share.log
./sgminer --sharelog share.log -o xxx -u yyy -p zzz

For every share found, data will be logged in a CSV (Comma Separated Value)
format:
    timestamp,disposition,target,pool,dev,thr,sharehash,sharedata
For example (this is wrapped, but it's all on one line for real):
    1335313090,reject,
    ffffffffffffffffffffffffffffffffffffffffffffffffffffffff00000000,
    http://localhost:8337,GPU0,0,
    6f983c918f3299b58febf95ec4d0c7094ed634bc13754553ec34fc3800000000,
    00000001a0980aff4ce4a96d53f4b89a2d5f0e765c978640fe24372a000001c5
    000000004a4366808f81d44f26df3d69d7dc4b3473385930462d9ab707b50498
    f681634a4f1f63d01a0cd43fb338000000000080000000000000000000000000
    0000000000000000000000000000000000000000000000000000000080020000
