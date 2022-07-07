# go mod コマンド

[Go Modules Reference](https://go.dev/ref/mod) より

## [init](https://go.dev/ref/mod#go-mod-init)
```shell
go mod init
  or
go mod init [module-path]
```

path を省略した場合
> init will attempt to infer the module path using import comments in .go files, vendoring tool configuration files, and
> the current directory (if in GOPATH).
> > .go ファイル内のインポートコメント、ベンダーツール構成ファイル、および現在のディレクトリ（GOPATHの場合）を使用して、initはモジュールパスを推測しようとします。

[module-path] : モジュールを公開する場合、これはGoツールでモジュールをダウンロードできるパスである必要があります。（ex, `github.com/<project-name>/`）

### Reserved module path prefixes

次の文字列はパッケージ名として使用されないことを保証します。

- [test] : 別のモジュールの機能をローカルでテストするように設計されているモジュールのモジュールパスプレフィックスとして使用できます。
- [example] : 依存関係を追跡するためだけにモジュールを作成するチュートリアルなど、一部のGoドキュメントでモジュールパスプレフィックスとして使用されます。


## redirect

[edit](https://go.dev/ref/mod#go-mod-edit)

```shell
go mod edit -replace example.com/greetings=../greetings
```

## synchronize module's dependencies

[tidy](https://go.dev/ref/mod#go-mod-tidy)

```shell
go mod tidy [-e] [-v] [-go=version] [-compat=version]
```

> `go.mod`ファイルがモジュールのソースコードと一致することを確認します。現在のモジュールのパッケージと依存関係を構築するために、必要な不足して
> いるモジュール要件を追加し、関連するパッケージを提供しないモジュールの要件を削除します。また、不足しているエントリを `go.sum` に追加し、不要な
> エントリを削除します。
>
> - [-e] : パッケージのローディング中にエラーが起きても継続
> - [-v] : 削除されたモジュールの情報を標準出力に表示
>
> すべてのビルドタグが有効であるとして振る舞うため、プラットフォーム依存のソースファイルやカスタムビルドのタグなど通常はビルドされないような物も
> 含みます。例外として `ignore build tag` は無効になります。また、メインモジュール内の `testdata` ディレクトリや、 `.` または `_` で始まる
> パッケージについても、他のパッケージから明示的にインポートされない限り考慮されません。
>
> `go mod tidy` を実行することで、`go.mod` に `require` が追加されます。また、見つからなかったモジュールの最新バージョンを要件に追加します。
> `//indirect` コメントは、メインモジュールのパッケージから提供されていないことを示しています。
>
> [-go=version] ： goを指定されたバージョンに更新し、そのバージョンに応じてモジュールグラフのプルーニングとレイジーモジュールのロードを有効
> または無効にします。
>
> [-compat=version] : デフォルトでは、モジュールグラフがgoディレクティブで示されたバージョンの直前のGoバージョンによってロードされたときに、
> 選択されたバージョンのモジュールが変更されないことを確認します。互換性についてチェックされたバージョン管理は、`-compat` フラグによって明示的に
> 指定することもできます。
