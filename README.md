# kpti_bench

So this is just doing a read from /dev/zero to /dev/null with varying
buffer size.

Run this on linux kernel 4.14.12.
```
./bench |tee log_kpti_on.txt
```

Then reboot and add "pti=off" to the kernel. check in
/proc/cmdline after boot that it is really there.

Then run this
```
./bench |tee log_kpti_off.txt
```

To see how much of a hit the KPTI is run.
```
./result log_kpti_off.txt log_kpti_on.txt
```

On a i7-6700
```
vendor_id	: GenuineIntel
cpu family	: 6
model		: 94
model name	: Intel(R) Core(TM) i7-6700K CPU @ 4.00GHz
stepping	: 3
microcode	: 0xba
cpu MHz		: 4000.000
cache size	: 8192 KB
```

this is the rather sad result.

block size     1 155.18 % slower with kpti
block size     2 155.99 % slower with kpti
block size     4 155.57 % slower with kpti
block size     8 156.15 % slower with kpti
block size    16 158.80 % slower with kpti
block size    32 151.52 % slower with kpti
block size    64 156.24 % slower with kpti
block size   128 155.39 % slower with kpti
block size   256 150.74 % slower with kpti
block size   512 140.65 % slower with kpti
block size  1024 125.05 % slower with kpti
block size  2048 97.616 % slower with kpti
block size  4096 71.413 % slower with kpti
block size  8192 42.875 % slower with kpti
block size 16384 19.138 % slower with kpti
block size 32768 9.4661 % slower with kpti
block size 65536 3.0003 % slower with kpti
block size 131072 -.8671 % slower with kpti


