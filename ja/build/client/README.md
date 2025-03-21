# クライアント

## JavaScript

<https://github.com/sunriselayer/sunrise-client-js>

```shell
npm i @sunriselayer/client
```

## Rust

現在クライアントライブラリのサポートはありませんが、protobuf の型定義ファイルを簡単に生成できます。

[Buf CLI](https://buf.build/docs/installation/)のインストールが必要です。

以下のようなディレクトリ構造になるように 2 つの YAML ファイルを作成します。

- `[project]`
  - `src`
    - `main.rs`
  - `buf.gen.yaml`
  - `buf.yaml`

{% code title="buf.yaml", overflow="wrap", lineNumbers="true" %}

```yaml
version: v2

deps:
  - buf.build/cosmos/cosmos-sdk
  - buf.build/cosmos/cosmos-proto
  - buf.build/cosmos/gogo-proto
  - buf.build/protocolbuffers/wellknowntypes
```

{% endcode %}

{% code title="buf.gen.yaml", overflow="wrap", lineNumbers="true" %}

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

`[project]`ディレクトリにて以下のコマンドを実行します。

```shell
buf dep update
buf generate
```
