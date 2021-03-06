# Installation

Sidef can be installed automatically from the [CPAN](https://metacpan.org/pod/distribution/Sidef/lib/Sidef.pod), by invoking the following command:

```console
$ cpan Sidef
```

When the `cpan` command is not available, try:

```console
$ perl -MCPAN -e "CPAN::Shell->install(q{Sidef})"
```

**IMPORTANT**: Sidef needs the [GMP](https://gmplib.org/), [MPFR](http://www.mpfr.org/) and [MPC](http://www.multiprecision.org/) C libraries.

To install Sidef manually, download the [latest version](https://github.com/trizen/sidef/archive/master.zip), unzip it and follow the installation steps:

```console
$ perl Build.PL
# ./Build installdeps
# ./Build install
```

When [Module::Build](https://metacpan.org/pod/Module::Build) is not installed, try:

```console
$ perl Makefile.PL
$ make test
# make install
```

If the installation succeeded, you should be able to run the `sidef` command:

```console
$ sidef -h
```
