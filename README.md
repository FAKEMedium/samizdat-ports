# samizdat-ports

A FreeBSD **ports overlay** for [Samizdat](https://github.com/FAKEMedium/Samizdat) —
the core application and the `Samizdat-Plugin-*` distributions, packaged as FreeBSD
ports. Build `.pkg` packages from these with **poudriere** (or `make package`).

> Starter scaffold. The port Makefiles follow the standard pattern but **must be
> validated on a FreeBSD box** — `portlint -AC`, then a poudriere test build — to
> confirm dependency origins, generate `distinfo` (`make makesum`) and `pkg-plist`
> (`make makeplist`).

## Layout

    www/samizdat/                      core app port (installs code + the rc.d scripts)
      Makefile  pkg-descr
      files/samizdat.in                rc.d service script (was samizdat.rc in core)
      files/minion.in                  rc.d service script (was minion.rc in core)
    www/p5-Samizdat-Plugin-Fortnox/    a template plugin port
      Makefile  pkg-descr

## Where the rc scripts live

The service scripts belong **here**, not in the application/CPAN dist: the core port
installs `files/{samizdat,minion}.in` to `${PREFIX}/etc/rc.d/` via `USE_RC_SUBR`.
Enable in `/etc/rc.conf`:

    samizdat_enable="YES"
    minion_enable="YES"

## Adding a port for another plugin

Each plugin port is mechanical — copy `www/p5-Samizdat-Plugin-Fortnox/` and change:

1. `PORTNAME` / `GH_PROJECT` / `COMMENT` / `WWW` / `DISTVERSION`.
2. `RUN_DEPENDS` = that dist's `Makefile.PL` `PREREQ_PM`, each CPAN module mapped to
   its FreeBSD `p5-` port origin (`cd /usr/ports && make search name=p5-<Module>`),
   plus `samizdat>=1.0.0:www/samizdat`.

## Fetching: GitHub now, CPAN later

The ports fetch from GitHub (`USE_GITHUB`) so you can build before publishing to CPAN.
Once the dists are on CPAN under **ALIPANG**, switch each to:

    MASTER_SITES=	CPAN
    DISTNAME=	Samizdat-Plugin-Fortnox-${DISTVERSION}
    # (drop the USE_GITHUB / GH_* lines)

## Build (poudriere, on FreeBSD)

    # one-time: jail + this overlay
    poudriere ports -c -p samizdat -m null -M /path/to/samizdat-ports
    poudriere bulk -j <jail> -p samizdat www/samizdat www/p5-Samizdat-Plugin-Fortnox
