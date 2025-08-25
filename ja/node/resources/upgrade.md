# アップグレード

Sunriseはオンチェーンガバナンスによってアップグレードされます。

## ソフトフォーク

ソフトフォークの場合、チェーンIDは変更されず、バイナリのバージョンが変更されます。また、アップグレードハンドラがプロセスを処理します。詳細は各アップグレード提案で説明されます。

Cosmovisorを実行している場合、自動アップグレードが利用可能です。
設定方法については、[Cosmovisorチュートリアル](../types/consensus/setup-cosmovisor.md)を参照してください。

CosmoVisorを使用しない場合は、バイナリを自分で変更してください。

## ハードフォーク

ソフトフォークでは対応できない変更を適用するために、ハードフォークが実行される場合があります。

`genesis.json`が変更され、新しいブロックは高さ1から始まります。
多くの場合、チェーンIDが変更されます。

## テストネット

ジェネシスからチェーンを同期する場合、このガイドに従い、ジェネシス時点で最新のバイナリバージョンを使用してください。
<https://github.com/sunriselayer/network/tree/main/dawn-1>

{% hint style="warning" %}
dawn-1テストネットでのみ、チェーンの状態によりv1.1.0バイナリの変更が必要です。
自動アップグレードなどで問題が発生した場合は、バイナリを置き換えてください。
<https://github.com/sunriselayer/sunrise/releases/download/v1.1.0/sunrised-linux-arm64-dawn-1-testnet>
{% endhint %}

## メインネット

ジェネシスからチェーンを同期する場合、このガイドに従い、ジェネシス時点で最新のバイナリバージョンを使用してください。
<https://github.com/sunriselayer/network/tree/main/sunrise-1>

現在使用されているバイナリのバージョンについては、[GitHub](https://github.com/sunriselayer/sunrise/releases)の最新リリースを参照してください。
