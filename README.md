# A Secure and Decentralized JavaScript Runtime

- Supports TypeScript 3.0 out of the box. Uses V8 7.0. That is, it's very modern
  JavaScript.

- No `package.json`. No npm. Not explicitly compatible with Node.

- Imports reference source code URLs only.

  ```typescript
  import { test } from "https://unpkg.com/deno_testing@0.0.5/testing.ts";
  import { log } from "./util.ts";
  ```

  Remote code is fetched and cached on first execution, and never updated until
  the code is run with the `--reload` flag. (So, this will still work on an
  airplane. See `~/.deno/src` for details on the cache.)

- File system and network access can be controlled in order to run sandboxed
  code. Defaults to read-only file system access and no network access. Access
  between V8 (unprivileged) and Rust (privileged) is only done via serialized
  messages defined in this
  [flatbuffer](https://github.com/denoland/deno/blob/master/src/msg.fbs). This
  makes it easy to audit. To enable write access explicitly use `--allow-write`
  and `--allow-net` for network access.

- Single executable:

  ```
  > ls -lh out/release/deno
  -rwxr-xr-x  1 rld  staff    48M Aug  2 13:24 out/release/deno
  > otool -L out/release/deno
  out/release/deno:
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1252.50.4)
    /usr/lib/libresolv.9.dylib (compatibility version 1.0.0, current version 1.0.0)
    /System/Library/Frameworks/Security.framework/Versions/A/Security (compatibility version 1.0.0, current version 58286.51.6)
    /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 400.9.0)
  >
  ```

- Always dies on uncaught errors.

- [Aims to support top-level `await`.](https://github.com/denoland/deno/issues/471)

- Aims to be browser compatible.

## Install

With Python:

```
curl -sSf https://raw.githubusercontent.com/denoland/deno_install/master/install.py | python
```

With PowerShell:

```powershell
iex (iwr https://raw.githubusercontent.com/denoland/deno_install/master/install.ps1)
```

_Note: Depending on your security settings, you may have to run
`Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` first to allow downloaded
scripts to be executed._

Try it:

```
> deno http://deno.land/thumb.ts
```

See also [deno_install](https://github.com/denoland/deno_install).

## Status

Under development.

We make binary releases [here](https://github.com/denoland/deno/releases).

Docs are [here](https://github.com/denoland/deno/blob/master/Docs.md).

