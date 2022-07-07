# Create_Go_Module
[Tutorial: Create a Go module](https://go.dev/doc/tutorial/create-module)

## イントロダクジョン
このチュートリアルでは、2つのモジュールを作成します。1つ目は、他のライブラリまたはアプリケーションによってインポートされることを目的としたライブラリです。
2つ目は、1つ目を使用する呼び出し元アプリケーションです。

## モジュールの作成

### exported name

> In Go, a function whose name starts with a capital letter can be called by a function not in the same package.
> This is known in Go as an exported name.
> > Goでは、名前が大文字で始まる関数は、同じパッケージに含まれていない関数から呼び出すことができます。これは、Goではエクスポートされた名前として知られています。

## モジュールの呼び出し

- `example.com/hello` の作成
- `hello/hello.go` の作成

`import`文からモジュールパスに従って公開されたモジュールをダウンロードする。が、このチュートリアルで作成したモジュールは公開したものではないため、
ローカル環境での `example.com/greetings` のコードを探して適応する必要がある。(cf. [go_mod#redirect](./doc/go_mod.md#redirect))

## エラーハンドリング

- Go標準ライブラリパッケージ `error` の利用
- 関数から2つめの返り値としてエラーを出力
- ログメッセージの記述（cf. [log](./doc/log_pkg.md)）

## ランダム

- 小文字で始まるメソッドはパッケージ内でしか利用できない（exported name ではない）
- `init` 関数による初期化（cf. [init](#init)）

### [init](https://go.dev/doc/effective_go#init)

> 最後に、各ソースファイルは引数を持たない独自の `init` 関数を定義し、必要な状態を設定できます。（各ファイルは複数のinit関数を持つことができます。）
> 「最後に」とは、文字通り「最後」を意味します。`init` 関数は、パッケージ内のすべての変数宣言が初期化子を評価した後に呼び出され、インポートされた
> すべてのパッケージが初期化された後にのみ評価されます。
> 
> 宣言として表現できない初期化に加えて、`init` 関数の一般的な使用法は、実際の実行が開始される前に、プログラムの状態が正しいかどうかを検証または
> 修復することが挙げられます。

## 複数人に挨拶を返す

「コメントなし」

## Test

> ファイル名を_test.goで終了すると、`go test` コマンドにこのファイルにテスト関数が含まれていることが通知されます。

(cf. [go_test](./doc/go_test.md) )

## コンパイル＆インストール

- `go build` : パッケージと依存関係のコンパイル
- `go install` : パッケージのコンパイルとインストール
- `go list -f '{{.Target}}'` : インストールパスの確認

