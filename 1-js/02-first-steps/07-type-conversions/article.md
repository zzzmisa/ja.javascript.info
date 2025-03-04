# 型変換

多くの場合、演算子と関数は自動的に値を正しい型に変換します。それを "型変換" と呼びます。

たとえば `alert` は、表示のためにどのような値も文字列へと自動的に変換します。数学的な演算では、値は数値に変換されます。

また、物事を正しくするために、ある値を明示的に変換する必要がある場合もあります。

```smart header="まだオブジェクトについては話していません"
このチャプターでは、まだ オブジェクト は説明しません。ここでは最初にプリミティブを学びます。

その後、オブジェクトについて学んだ後、チャプター <info:object-toprimitive> で、どのようにオブジェクト変換が動作するのかを見ていきます。
```

## 文字列変換 

文字列変換は、文字列形式の値が必要なときに発生します。

たとえば、`alert(value)` は値を表示するためにそれを行います。

また、そのために、`String(value)` 関数を使うこともできます:

```js run
let value = true;
alert(typeof value); // boolean

*!*
value = String(value); // 今、値は文字列の "true"
alert(typeof value); // string
*/!*
```

文字列変換はほとんどが明白です。`false` は `"false"` に、 `null` は `"null"` になります。

## 数値変換 

数値変換は数学的関数や表現の中で自動的に起こります。

たとえば、非数値に除算 `/` が適用された場合:

```js run
alert( "6" / "2" ); // 3, 文字列は数値に変換されます
```

また、明示的に `value` を変換するために `Number(value)` を使うことができます。

```js run
let str = "123";
alert(typeof str); // string

let num = Number(str); // 数値の 123 になります

alert(typeof num); // number
```

テキストフォームのような、文字列ベースのソースから値を読むが、数値が入力されることを想定するときには通常明示的な変換が必要になります。

文字列が有効な数値でない場合、このような変換の結果は `NaN` です。たとえば:

```js run
let age = Number("an arbitrary string instead of a number");

alert(age); // NaN, 変換失敗
```

数値変換ルール:

| 値 |  変換後... |
|-------|-------------|
|`undefined`|`NaN`|
|`null`|`0`|
|<code>true&nbsp;と&nbsp;false</code> | `1` and `0` |
| `string` | 最初と最後のスペースは取り除かれます。そして、残った文字列が空の場合は結果は 0 になります。そうでなければ、文字列から "読んだ" 数値です。 エラーでは `NaN` が与えられます。|

例:

```js run
alert( Number("   123   ") ); // 123
alert( Number("123z") );      // NaN ("z" の読み込みでエラー)
alert( Number(true) );        // 1
alert( Number(false) );       // 0
```

`null` と `undefined` はここでは異なる振る舞いをすることに留意してください。: `undefined` が `NaN` になる一方、`null` は 0 になります。

ほとんどの算術演算もこのような変換を行います。次のチャプターでそれらを詳しく見ていきます。

## Boolean変換 

真偽値(Boolean)変換はシンプルです。

論理演算(後ほど条件テストや他の種類を見ます)で起こりますが、`Boolean(value)` を呼ぶことで手動で実行することもできます。

変換ルール:

- `0`, 空文字, `null`, `undefined` や `NaN` のように直感的に "空" の値は `false` になります。
- 他の値は `true` になります。

例:

```js run
alert( Boolean(1) ); // true
alert( Boolean(0) ); // false

alert( Boolean("hello") ); // true
alert( Boolean("") ); // false
```

````warn header="注意してください: ゼロの文字列 `\"0\"` は `true` です"
幾つかの言語(すなわち PHP)は `”0”` を `false` として扱います。しかし、JavaScriptでは、非空文字は常に `true` です。

```js run
alert( Boolean("0") ); // true
alert( Boolean(" ") ); // スペースもまた true です (任意の非空文字は true)
```
````

## サマリ 

3つの最も広く使われている型変換があります: 文字列変換, 数値変換, 真偽値変換です。

**`文字列変換`** -- 何かを出力するときに起こり、`String(value)` で行うことができます。文字列への変換は、通常はプリミティブな値にとって明白です。

**`数値変換`** -- 算術演算で起こり、`Number(value)` で実行できます。

変換は次のルールに従います:

| 値 |  変換後... |
|-------|-------------|
|`undefined`|`NaN`|
|`null`|`0`|
|<code>true&nbsp;と&nbsp;false</code> | `1` and `0` |
| `string` | 前後の連続した空白は取り除かれます。そして、残った文字列が空の場合は結果は 0 になります。そうでなければ、文字列から "読んだ" 数値です。 エラーでは `NaN` が与えられます。|

**`真偽値変換`** -- 論理演算で発生するか、`Boolean(value)` で実行できます。

次のルールに従います:

| 値 |  変換後... |
|-------|-------------|
|`0`, `null`, `undefined`, `NaN`, `""` |`false`|
|それ以外の値| `true` |


ルールのほとんどは理解し覚えるのが簡単です。通常間違える注目すべき例外は:

- `undefined` は文字列としては `NaN` です, `0` ではりません。
- `"0"` と `"   "` のようなスペースだけの文字列は真偽値としては true です。

オブジェクトについてはここでは説明しませんが、JavaScriptについての基本的なことを学んだら、オブジェクトに専念する <info:object-toprimitive> の章の後半に戻ります。
