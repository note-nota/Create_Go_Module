# log package

[log](https://pkg.go.dev/log) より

## 概要

> `log` パッケージは、単純なロギングを実装します。これは、出力をフォーマットするためのメソッドを使用して、タイプLoggerを定義します。
> また、ヘルパー関数 `Print` [f|ln]、`Fatal` [f|ln]、および `Panic` [f|ln]を介してアクセスできる、事前定義された
> 「標準」のロガーがあります。これらは、ロガーを手動で作成するよりも簡単に使用できます。そのロガーは標準エラーに書き込み、ログに記録された
> 各メッセージの日付と時刻を出力します。すべてのログメッセージは個別の行に出力されます。印刷されるメッセージが改行で終わらない場合、ロガーは
> 改行を追加します。`Fatal` 関数は、ログメッセージを書き込んだ後、`os.Exit(1)` を呼び出します。`Panic` 関数は、ログメッセージを
> 書き込んだ後に `panic` を呼び出します。

## 定数

```go
const (
	Ldate         = 1 << iota     // the date in the local time zone: 2009/01/23
	Ltime                         // the time in the local time zone: 01:23:23
	Lmicroseconds                 // microsecond resolution: 01:23:23.123123.  assumes Ltime.
	Llongfile                     // full file name and line number: /a/b/c/d.go:23
	Lshortfile                    // final file name element and line number: d.go:23. overrides Llongfile
	LUTC                          // if Ldate or Ltime is set, use UTC rather than the local time zone
	Lmsgprefix                    // move the "prefix" from the beginning of the line to before the message
	LstdFlags     = Ldate | Ltime // initial values for the standard logger
)
```

> これらのフラグは、ロガーによって生成された各ログエントリのプレフィックスとなるテキストを定義します。ビットによって何を印刷するかを制御します。
> Lmsgprefixフラグを除いて、表示される順序（ここにリストされている順序）または表示される形式（コメントで説明されている）を制御することはできません。
> LlongfileまたはLshortfileが指定されている場合にのみ、プレフィックスの後にコロンが続きます。
> 
> たとえば、フラグ `Ldate | Ltime (またはLstdFlags)` だと、
> > 2009/01/23 01:23:23 message
> 
> `Ldate | Ltime | Lmicroseconds | Llongfile` の場合、
> > 2009/01/23 01:23:23.123123 /a/b/c/d.go:23: message

