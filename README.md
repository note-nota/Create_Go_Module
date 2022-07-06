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


