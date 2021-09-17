```
Sat Feb 27 19:33:07 PST 1993

This directory contains files and patches to apply to the BSD/386 GAMMA.4
(or GAMMA.4.1) kernel to enable a high resolution version of microtime.
This code will probably be integrated into the BSD/386 1.1 Release.
Thanks to Sean Eric Fagan (sef@moria.cygnus.com) for providing patches
for 386BSD.

Since gettimeofday calls microtime, these kernel modifications will
allow user-level access to high resolution time stamps.  This doesn't
mean however that programs that use gettimeofday will report more
significant figures -- you might want to hack ping, traceroute, etc.
to do so.  Although the microtime routine looks somewhat heavy weight,
it runs (about) twice as fast as the current microtime because it avoids
the expensive spl calls.

To install the new microtime:

  1. Copy timerreg.h to /sys/i386/isa.

  2. Copy microtime.s to /sys/i386/i386.

  3. Apply the patches in patch.sys to the kernel, e.g.,

	% cd /sys
	% ci -l i386/i386/machdep.c
	% ci -l i386/isa/clock.c

     Now do this for BSD/386,

	% patch -p1 < /tmp/patch.sys

     Or this for 386BSD,

	% patch -p0 < /tmp/patch.sys.386bsd

  4. Add this line to /sys/i386/conf/files.i386:
	i386/i386/microtime.s   standard

  5. [optional]  Change the reference to "time" in net/bpf.c to a call
	to microtime.

  6. [optional] Hack ping and traceroute to print more digits...

  7. Build new kernel.

Please direct feedback, bug reports, improvements, etc. to mccanne@ee.lbl.gov.

Steve McCanne
```
