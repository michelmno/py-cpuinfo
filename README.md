py-cpuinfo
==========

[![Downloads](https://img.shields.io/pypi/dm/py-cpuinfo.svg)](https://pypi.python.org/pypi/py-cpuinfo/)
[![Latest Version](https://img.shields.io/pypi/v/py-cpuinfo.svg)](https://pypi.python.org/pypi/py-cpuinfo/)
[![License](https://img.shields.io/pypi/l/py-cpuinfo.svg)](https://pypi.python.org/pypi/py-cpuinfo/)
[![License](https://img.shields.io/pypi/pyversions/py-cpuinfo.svg)](https://pypi.python.org/pypi/py-cpuinfo/)

Py-cpuinfo gets CPU info with pure Python. Py-cpuinfo should work without any
extra programs or libraries, beyond what your OS provides. It does not require
any compilation(C/C++, assembly, et cetera) to use. It works with Python 2
and 3.

OS Support
-----
| OS            | Tested and works                                       | Untested        |
| :------------ | :----------------------------------------------------- | :-------------- |
| Android       |                                                        | Everything      |
| BSD           | FreeBSD, PC-BSD                                        | OpenBSD, NetBSD |
| Cygwin        | Windows                                                |                 |
| Haiku         | Haiku Nightly                                          | BeOS            |
| Linux         | Arch, Centos, Debian, Fedora, Gentoo, OpenSuse, Ubuntu |                 |
| OS X          | 10.8, 10.9, 10.10                                      | 10.11           |
| Solaris       | Oracle Solaris, OpenIndiana                            |                 |
| Windows       | XP, Vista, 7, 8, 10                                    | RT              |


CPU Support
-----
* X86 32bit and 64bit
* Some ARM CPUs (tested on BeagleBone armv7l)


API
-----
~~~python
get_cpu_info()
'''
Returns the CPU info by using the best source of information for your OS.
This is the recommended function for getting CPU info.
Returns None if nothing is found.
'''
~~~

~~~python
get_cpu_info_from_registry()
'''
Returns the CPU info gathered from the Windows Registry.
Returns None if not on Windows.
'''
~~~

~~~python
get_cpu_info_from_proc_cpuinfo()
'''
Returns the CPU info gathered from /proc/cpuinfo.
Returns None if /proc/cpuinfo is not found.
'''
~~~

~~~python
get_cpu_info_from_sysctl()
'''
Returns the CPU info gathered from sysctl.
Returns None if sysctl is not found.
'''
~~~

~~~python
get_cpu_info_from_kstat()
'''
Returns the CPU info gathered from isainfo and kstat.
Returns None if isainfo or kstat are not found.
'''
~~~

~~~python
get_cpu_info_from_dmesg()
'''
Returns the CPU info gathered from dmesg.
Returns None if dmesg is not found or does not have the desired info.
'''
~~~

~~~python
get_cpu_info_from_sysinfo()
'''
Returns the CPU info gathered from sysinfo.
Returns None if sysinfo is not found.
'''
~~~

~~~python
get_cpu_info_from_cpuid()
'''
Returns the CPU info gathered by querying the X86 cpuid register in a new process.
Returns None on non X86 cpus.
Returns None if SELinux is in enforcing mode.
'''
~~~


Output
-----
| key                    | Example value   |
| :--------------------- | :-------------- |
| vendor_id              | "GenuineIntel"    |
| hardware               | "BCM2708" |
| brand                  | "Intel(R) Core(TM) i7 CPU         870  @ 2.93GHz" |
| hz_advertised          | "2.9300 GHz" |
| hz_actual              | "1.7330 GHz" |
| hz_advertised_raw      | (2930000000, 0)|
| hz_actual_raw          | (1733000000, 0) |
| arch                   | "X86_64" |
| bits                   | 64 |
| count                  | 4 |
| raw_arch_string        | "x86_64" |
| l2_cache_size          | "8192 KB" |
| l2_cache_line_size     | 0 |
| l2_cache_associativity | 0  |
| stepping               | 5 |
| model                  | 30 |
| family                 | 6 |
| processor_type         | 0 |
| extended_model         | 0 |
| extended_family        | 0 |
| flags                  | ['acpi', 'aperfmperf', 'apic', 'arch_perfmon', 'bts', 'clflush', 'cmov', 'constant_tsc', 'cx16', 'cx8', 'de', 'ds_cpl', 'dtes64', 'dtherm', 'dts', 'ept', 'est', 'flexpriority', 'fpu', 'fxsr', 'ht', 'ida', 'lahf_lm', 'lm', 'mca', 'mce', 'mmx', 'monitor', 'msr', 'mtrr', 'nonstop_tsc', 'nopl', 'nx', 'pae', 'pat', 'pbe', 'pdcm', 'pebs', 'pge', 'pni', 'popcnt', 'pse', 'pse36', 'rdtscp', 'rep_good', 'sep', 'smx', 'ss', 'sse', 'sse2', 'sse4_1', 'sse4_2', 'ssse3', 'syscall', 'tm', 'tm2', 'tpr_shadow', 'tsc', 'vme', 'vmx', 'vnmi', 'vpid', 'xtopology', 'xtpr'] |


These approaches are used for getting info:
-----
1. Windows Registry (Windows)
2. /proc/cpuinfo (Linux)
3. sysctl (OS X)
4. dmesg (Unix/Linux)
5. isainfo and kstat (Solaris)
6. cpufreq-info (BeagleBone)
7. lscpu (Unix/Linux)
8. sysinfo (Haiku)
9. Querying the CPUID register (Intel X86 CPUs)


Run as a script
-----
~~~bash
$ python cpuinfo/cpuinfo.py
~~~

Run as a module
-----
~~~bash
$ python -m cpuinfo
~~~

Run as a library
-----
~~~python
import cpuinfo
info = cpuinfo.get_cpu_info()
print(info)
~~~

Bugs and Corrections
-----

Please report a Bug if you suspect any of this information is wrong.

If py-cpuinfo does not work on your machine, run the script:

~~~bash
python tools/get_system_info.py
~~~

and create bug report with the generated "system_info.txt" file.
