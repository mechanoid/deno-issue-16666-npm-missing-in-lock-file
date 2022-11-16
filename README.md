Minimal Test Case to showcase an Issue around Lock-File Generation and npm:

See https://github.com/denoland/deno/issues/16666 for more information

## Issues

1. `deno cache --lock --reload deps.ts` creates a lock file, that contains `npm` dependencies,
same command with `--lock-write` does not!

## Tests


```
rm deno.lock # make sure the file is not created yet
deno task deps:load # should not create a lock file?!
# => ✅ deno.lock is created (because of auto discovery)
# => ✅ deno.lock contains `npm` deps
```

```
rm deno.lock # make sure the file is not created yet
deno task deps:update # should create a lock file
# => ✅ deno.json is created
# => ⚡️ deno.lock does not contain `npm` deps
```

## Tested Version

```
deno --version
# deno 1.28.0 (release, aarch64-apple-darwin)
# v8 10.9.194.1
# typescript 4.8.3
```
