# GCMake Emscripten Compatibility

This project creates CMake helper targets which allow [GCMake](https://github.com/scupit/gcmake-rust)
to opt in to certain emscripten functionality
([namely persistent file systems](https://emscripten.org/docs/api_reference/Filesystem-API.html#file-systems))
using the same [gcmake unified dependency interface](https://github.com/scupit/gcmake-dependency-configs).

## Targets

| Name | Defines | Description |
| ---- | ------- | ----------- |
| *emscripten-compat_NODEFS* | `EMSCRIPTEN_NODEFS_ENABLED=1` | Enables Emscripten's [NODEFS](https://emscripten.org/docs/api_reference/Filesystem-API.html#nodefs) functionality. |
| *emscripten-compat_IDBFS* | `EMSCRIPTEN_IDBFS_ENABLED=1` | Enables Emscripten's [IDBFS](https://emscripten.org/docs/api_reference/Filesystem-API.html#filesystem-api-idbfs) functionality. |
| *emscripten-compat_WORKERFS* | `EMSCRIPTEN_WORKERFS_ENABLED=1` | Enables Emscripten's [WORKERFS](https://emscripten.org/docs/api_reference/Filesystem-API.html#workerfs) functionality. |
| *emscripten-compat_PROXYFS* | `EMSCRIPTEN_PROXYFS_ENABLED=1` | Enables Emscripten's [PROXYFS](https://emscripten.org/docs/api_reference/Filesystem-API.html#proxyfs) functionality. |

## Main GCMake Repository Links

- [gcmake-rust](https://github.com/scupit/gcmake-rust)
- [gcmake-dependency-configs](https://github.com/scupit/gcmake-dependency-configs)
- [gcmake-test-project](https://github.com/scupit/gcmake-test-project)
