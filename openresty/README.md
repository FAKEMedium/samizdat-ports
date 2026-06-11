# OpenResty edge config for Samizdat

Production edge / reverse-proxy configuration for running Samizdat behind
[OpenResty](https://openresty.org/) (nginx + LuaJIT). This is **deployment** infrastructure —
it is not part of the Perl distribution and is not loaded by the application.

## Layout

- `lua/redisauth.lua` — authorize requests against a session stored in Redis/Valkey
  (`samizdat:<cookie>`), for offloading auth to the edge.
- `lua/csp.lua` — apply Content-Security-Policy headers from the companion `.csp` files
  Samizdat generates next to its static output.
- `nginx/conf/nginx.conf` — reference `nginx.conf` (sets `lua_package_path`, includes
  `sites-enabled/*`).
- `nginx/conf/sites-available/example.com.conf` — example per-site server block.

## Install

Copy the Lua modules where `lua_package_path` can find them (e.g.
`/usr/local/openresty/site/lualib/`) and the nginx confs under
`/usr/local/openresty/nginx/conf/`. On FreeBSD the `www/samizdat` port can install these;
see that port's `Makefile`.

The `csp.lua` module expects Samizdat to emit `.csp` sidecar files (see
`Samizdat::Command::makestatic` / `makeswcache` in core). `redisauth.lua` expects the same
Redis/Valkey instance Samizdat uses for sessions (`manager.cache.redis`).
