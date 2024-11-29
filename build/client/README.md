# Client

## JavaScript

<https://github.com/sunriselayer/sunrise-client-js>

```shell
npm i @sunriselayer/client
```

## Rust

Currently there is no support for client library, but you can easily generate the protobuf type definition files.

Installing [Buf CLI](https://buf.build/docs/installation/) is required.

{% code title="./buf.yaml" overflow="wrap" lineNumbers="true" %}

```yaml
version: v2

deps:
  - buf.build/cosmos/cosmos-sdk
  - buf.build/cosmos/cosmos-proto
  - buf.build/cosmos/gogo-proto
  - buf.build/protocolbuffers/wellknowntypes
```

{% endcode %}

{% code title="./buf.gen.yaml" overflow="wrap" lineNumbers="true" %}

```yaml
version: v2
managed:
  enabled: true

plugins:
  - remote: buf.build/community/neoeinstein-prost:v0.4.0
    out: src
    opt:
      - compile_well_known_types
      - extern_path=.google.protobuf=::pbjson_types
  - remote: buf.build/community/neoeinstein-prost-serde:v0.3.1
    out: src
  - remote: buf.build/community/neoeinstein-tonic:v0.4.1
    out: src
    opt:
      - compile_well_known_types
      - extern_path=.google.protobuf=::pbjson_types

inputs:
  - git_repo: https://github.com/sunriselayer/sunrise.git
    branch: main
    subdir: proto
```

{% endcode %}

```shell
buf dep update
buf generate
```
