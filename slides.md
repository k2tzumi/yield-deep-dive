---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: 時間の許す限りyieldの挙動を説明する
info: |
  PHPerKaigi 2025
  https://phperkaigi.jp/2025/
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
addons:
  - '@katzumi/slidev-addon-qrcode'
  - slidev-addon-components
  - slidev-addon-rabbit
---

# 時間の許す限りyieldの挙動を説明する

PHPerKaigi 2025 Mar 23, 2025.  
v0.0.1  
@katzumi(かつみ)

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/k2tzumi/software-design-hierarchy" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
layout: two-cols-header
---

# 自己紹介

katzumi（かつみ）と申します。

「障害のない社会をつくる」をビジョンに掲げている「LITALICO」という会社に所属しています
<a href="https://litalico.co.jp/">
<img src="https://litalico.co.jp/ogp.png" class="w-40" />
</a>

以下のアカウントで活動しています。

::left::

<div class="float-left">
<img src="https://pbs.twimg.com/profile_images/1768978237210935296/idy9J4l6_400x400.jpg" class="rounded-full w-40 mr"/>  
<simple-icons-x /> <a href="https://twitter.com/katzchum">katzchum</a></div>  
<QRCode :width="180" :height="180" value="https://twitter.com/katzchum" color="4329B9" image="Logo_of_X.svg" />

::right::

<img src="https://avatars.githubusercontent.com/u/1182787?v=4" class="rounded-full w-40 mr-12"/>

<logos-github-octocat /> [k2tzumi](https://github.com/k2tzumi)  
<simple-icons-zenn /> [katzumi](https://zenn.dev/katzumi)  

<br />

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
layout: two-cols-header
transition: fade-out
---


# お願い

写真撮影、SNS での実況について

登壇者の励みになるので是非ともご意見やご感想など、フィードバック頂けると助かります mm  
あとでスライドを公開します

::left::

<Transform :scale="2.5">
　　　🙆‍♀📷<ph-projector-screen-chart-light /><br />
　　　🙅‍♂📹💸<br />
　　　🙅📸👨‍👦‍👦<br />
</Transform>

::right::

<br />
<Transform :scale="2">
<fa6-brands-square-x-twitter />
</Transform>
<br />
<a href="https://x.com/search?q=%23phperkaigi%20%23a&f=live">#phperkaigi #a</a>


<!-- 本セッションでは、撮影やSNS拡散を歓迎しています。ご自由に写真を撮影して、XなどのSNSでシェアしてください。 　　
ただし、以下の点にご注意ください。　　

著作権などの法的な問題を避けるために、スライドや登壇者の写真や動画を無断で商用利用しないでください。　　
他の参加者のプライバシーや迷惑にならないように、撮影や投稿する際には配慮してください。　　
SNSでシェアする際には、ハッシュタグ「#phpcon_nagoya #s」をつけてください。　　
これにより、本セッションの関連情報を簡単に検索できるようになります。 -->

---
layout: default
transition: slide-up
---

# Yield is 何？
一言で言うと...

「**データを一つずつ返す仕組み**」

---

# ジェネレータ関数の特徴

- 関数の実行を一時停止できる 🛑
- メモリ効率が良い 💾
- イテレータを簡単に作れる 🔄
- 値を生成しながら処理できる 🏭

---

# 基本的な構文

```php
function myGenerator() {
    yield 1;  // 一時停止して1を返す
    yield 2;  // 再開後、一時停止して2を返す
    yield 3;  // 再開後、一時停止して3を返す
}

foreach (myGenerator() as $value) {
    echo $value;  // 1, 2, 3 と出力
}
```

---

# 他の言語の類似機能

- JavaScript: Generator functions
- Python: Generators
- C#: Iterator methods
- Ruby: Enumerators

---

# イテレータとは？
一言で言うと...

「**コレクションを順番に処理するための仕組み**」

---

# イテレータの特徴

- データを **一つずつ** 取り出せる 🔄
- 内部状態を保持している 📝
- `foreach` で簡単に使える 🔁
- コレクションの実装を隠蔽できる 🧩

---

# PHPのIteratorインターフェース

```php
interface Iterator extends Traversable {
    public function current();  // 現在の要素を返す
    public function key();      // 現在のキーを返す
    public function next();     // 次の要素に進む
    public function rewind();   // 最初に巻き戻す
    public function valid();    // 現在位置が有効か確認
}
```

---

# イテレータの実装例

```php
// カスタムイテレータ
$it = new ArrayIterator([1, 2, 3]);

// foreachで使用
foreach ($it as $key => $value) {
    echo "$key: $value\n";
}

// 手動制御も可能
$it->rewind();
while ($it->valid()) {
    echo $it->current() . "\n";
    $it->next();
}
```

---

# yieldテスト始めるよ

---

# 訓練されたPHPerなら余裕で答えられるよね？

---

# 提示するコードが正常終了するか？お考えください
`assert` 関数が全て `true` になると思ったら、ペンライトを振ってください！

---

# テスト1️⃣ （持ち時間5秒）
変動する変数の値が返却されるよ！

```php {lines:true}
<?php
$simpleGenerator = function(int $i) {
    yield $i++;
    yield ++$i;
    yield $i += 5;
};
$actual = [];
foreach ($simpleGenerator(10) as $value) {
    $actual[] = $value;
}
assert([10, 12, 17] == $actual, var_export($actual, true));
```

[https://3v4l.org/rVs2H](https://3v4l.org/rVs2H)

---

# ✅️ Assert Success!

---

# テスト1️⃣
インクリメントの挙動の確認でした！

---

# テスト2️⃣ （持ち時間10秒）
値だけじゃなくてキーも返せるよ

```php
<?php
$keyValueGenerator = function() {
    yield 3 => '参';
    yield 2 => '弐';
    yield 1 => '壱';
};
$actual = [];
foreach ($keyValueGenerator() as $key => $value) {
    $actual[$key] = $value;
}
$expected = ['壱', '弐', '参'];
assert($expected == $actual, var_export($actual, true));
```

[https://3v4l.org/P4Qag](https://3v4l.org/P4Qag)

---

# ❌️ Assert Fail!

```
Fatal error: Uncaught AssertionError: array (
  3 => '参',
  2 => '弐',
  1 => '壱',
) in php-wasm run script:12
Stack trace:
#0 php-wasm run script(12): assert(false, 'array (\n  3 => ...')
#1 {main}
  thrown in php-wasm run script on line 12
```

---

# テスト2️⃣
ひっかけ問題すみません。

リスト（キー指定していない `$expected`）の配列キーは 0 から始まるよね。  
以下なら Success。  
厳密比較( `===` )すると Fail です。

```php
<?php
$keyValueGenerator = function() {
    yield 2 => '参';
    yield 1 => '弐';
    yield 0 => '壱';
};
$actual = [];
foreach ($keyValueGenerator() as $key => $value) {
    $actual[$key] = $value;
}
$expected = ['壱', '弐', '参'];
assert($expected == $actual, var_export($actual, true));
```

[https://3v4l.org/jE5nc](https://3v4l.org/jE5nc)

---

# テスト3️⃣ （持ち時間5秒）
テスト 1️⃣のケースでもキーをつけるとどうなるのかな？

```php
<?php
$simpleGenerator = function(int $i) {
    yield $i++;
    yield ++$i;
    yield $i += 5;
};
$actual = [];
foreach ($simpleGenerator(10) as $i => $value) {
    $actual[$i] = $value;
}
assert([10, 12, 17] == $actual, var_export($actual, true));
```

[https://3v4l.org/47XGv](https://3v4l.org/47XGv)


---

# ✅️ Assert Success!

---

# テスト3️⃣

いい感じにキーを採番してくれます

----

# テスト4️⃣ （持ち時間5秒）
キーあり、なしの組み合わせ行うとどうなるか？

```php
<?php
$keyValueGenerator = function() {
    yield 'one' => 1;
    yield 2;
    yield 'three' => 3;
    yield 4 => 'four';
    yield 5;
};
$actual = [];
$expected = [
  'one' => 1,
  0 => 2,
  'three' => 3,
  4 => 'four',
  5 => 5
];
foreach ($keyValueGenerator() as $i => $value) {
    $actual[$i] = $value;
}
assert($expected == $actual, var_export($actual, true));
```

[https://3v4l.org/ljfnq](https://3v4l.org/ljfnq)

---

# テスト4️⃣
PHP の配列のキーって文字列と数値が混在させることが出来てアレ

キー指定がない場合、以下のルールで数値キーが自動採番させれます

- キーを指定しない場合、自動的に連番(0 から) が振られる  
`[ 'one' => 1]` の次が `[ 0 => 2 ]`  
`yield 2` のあとに `yield 2.5` を追加した場合は　`[ 1 => 2.5 ]`　が結果に追加となる
- 数値キーがあった場合に、そこからの連番になる  
`[ 4 => 'four']` の次が `[ 5 => 5 ]`

---

# テスト5️⃣ （持ち時間5秒）
値を指定しない場合はどうなるのか？

```php
<?php
function emptyYieldGenerator(int $case): iterable {
    switch ($case) {
      case 1: yield 'not empty'; break;
      case 2: yield; break;
      default: return;
    }
}
function assertGeneratorOutput(int $case, array $expected): void {
    $actual = [];
    foreach (emptyYieldGenerator($case) as $key => $value) $actual[$key] = $value;
    assert($expected == $actual, var_export($actual, true));
}

assertGeneratorOutput(1, [ 0 => 'not empty' ]);
assertGeneratorOutput(2, []);
assertGeneratorOutput(3, []);
```

[https://3v4l.org/9kiQO](https://3v4l.org/9kiQO)


---

# ❌️ Assert Fail!

```
Fatal error: Uncaught AssertionError: array (
  0 => NULL,
) in /in/9kiQO:12
Stack trace:
#0 /in/9kiQO(12): assert(false, 'array (\n  0 => ...')
#1 /in/9kiQO(16): assertGeneratorOutput(2, Array)
#2 {main}
  thrown in /in/9kiQO on line 12

Process exited with code 255.
```

---

# テスト5️⃣
switch 文だと break しないと連続して yield されるので注意

2 回目の assert は　`[ 0 => null ]` になる
- `yield null` する場合と同義  
null が返却される
- `return` はまた挙動が違う  
要素自体が返却されない

---

# テスト6️⃣ （持ち時間10秒）
yield from という書き方もあります

```php
<?php
function innerGenerator(): iterable {
    yield 'a' => 1;
    yield 'b' => 2;
}
function outerGenerator(): iterable {
    yield 'x' => 0;
    yield from innerGenerator();
    yield 'y' => 3;
    yield from ['c' => 4, 'd' => 5];    // 配列からのyield
}
$expected = [
    'x' => 0,
    'a' => 1, 'b' => 2,
    'y' => 3,
    'c' => 4, 'd' => 5
];
$actual = [];
foreach (outerGenerator() as $key => $value) $actual[$key] = $value;
assert($expected === $actual, var_export($actual, true));
```

[https://3v4l.org/mfpRU](https://3v4l.org/mfpRU)


---

# ✅️ Assert Success!
今回は厳密比較でも OK です

---

# テスト6️⃣
まとめて yield させることもできます

yield from キーワードを使ってジェネレータの委譲が出来ます。

 外側のジェネレータは、内側のジェネレータ (あるいはオブジェクトや配列) から受け取れるすべての値を yield し、 何も取得できなくなったら外側のジェネレータの処理を続行します。

---

# テスト7️⃣ （持ち時間10秒）
yield from でキー指定ありなしを混在させるとどうなるか？

```php
<?php
function generatorWithKeys(): iterable {
    yield "a" => 1;
    yield "b" => 2;
}
function generatorWithoutKeys(): iterable {
    yield 3;
    yield 4;
}
function mixedGenerator(): iterable {
    yield from [5, 6];  // 配列（キーなし）からyield from
    yield from generatorWithKeys(); // キーありジェネレータからyield from
    yield from generatorWithoutKeys();  // キーなしジェネレータからyield from
    yield from ["c" => 7, "d" => 8];  // 配列（キーあり）からyield from
}
$expected = [0 => 5, 1 => 6,
    'a' => 1, 'b' => 2,
    2 => 3, 3 => 4,
    'c' => 7, 'd' => 8];
$actual = [];
foreach (mixedGenerator() as $key => $value) $actual[$key] = $value;
assert($expected === $actual, var_export($actual, true));
```

[https://3v4l.org/H0kbG](https://3v4l.org/H0kbG)

---

# ❌️ Assert Fail!

```
Fatal error: Uncaught AssertionError: array (
  0 => 3,
  1 => 4,
  'a' => 1,
  'b' => 2,
  'c' => 7,
  'd' => 8,
) in /in/H0kbG:22
Stack trace:
#0 /in/H0kbG(22): assert(false, 'array (\n  0 => ...')
#1 {main}
  thrown in /in/H0kbG on line 22

Process exited with code 255.
```

---

# テスト7️⃣ 
結果わかりづらいけれど。。

- キーの自動採番ルールはジェネレータ関数毎に適用される  
mixedGenerator と generatorWithoutKeys のキーの採番は独立する
- yield from で委譲した結果のキーは引き継がれる  
generatorWithoutKeys の結果が　`[ 2 => 3, 3 => 4]` ではなく `[ 0 => 3, 1 => 4]`
- ジェネレータのキーの重複は OK  
通常の array では定義出来ないけれど、以下が返却されている  
`[ 0 => 3, 1 => 4, 'a' => 1, 'b' => 2, 0 => 3, 1 => 4, 'c' => 7, 'd' => 8]`  
キーの 0 と 1 が重複して出現している

---

# テスト8️⃣ （持ち時間10秒）
return を組み合わせて利用する

```php
<?php
$generatorWithReturn = function() {
    yield 1;
    yield 2;
    yield 3;
    return ['a' => 4, 'b' => 5];
};
$gen = $generatorWithReturn();
$actual = iterator_to_array($gen);
assert([1, 2, 3] === $actual, var_export($actual, true));
$actual = $gen->getReturn();
assert([ 1, 2 , 3, 'a' => 4, 'b' => 5] == $actual, var_export($actual, true));
```

[https://3v4l.org/4tAN5](https://3v4l.org/4tAN5)

---

# ❌️ Assert Fail!

```
Fatal error: Uncaught AssertionError: array (
  'a' => 4,
  'b' => 5,
) in /in/4tAN5:12
Stack trace:
#0 /in/4tAN5(12): assert(false, 'array (\n  'a' =...')
#1 {main}
  thrown in /in/4tAN5 on line 12

Process exited with code 255.
```

---

# テスト8️⃣
返り値と生成値は独立しています

- ジェネレータの返り値は foreach ループでは取得できない  
return の返り値は無視される
- 専用の `getReturn()` メソッドを使う必要がある  
`['a' => 4, 'b' => 5]` が返り値として取得できる
- `getReturn()` を使うには、ジェネレータを完全に消費（全ての yield を処理）する必要がある  
途中で break した場合は例外が発生する

【実用的な使用例】  
ジェネレータで大量のデータを処理し、最後に集計結果や処理状態を返す
例外処理と組み合わせて、エラー情報や処理結果を返す

---

# テスト9️⃣ （持ち時間5秒）
ジェネレータ関数を連続で呼び出した場合

```php
<?php
$i = 1;
$generator = function() use($i) {
    yield $i++;
    yield $i++;
    yield $i++;
};
$gen = $generator();
$actual = iterator_to_array($gen);
assert([1, 2, 3] === $actual, var_export($actual, true));
assert(1 === $i);
$gen = $generator();
$actual = iterator_to_array($gen);
assert([1, 2, 3] === $actual, var_export($actual, true));
$actual = iterator_to_array($gen);
assert([1, 2, 3] === $actual, var_export($actual, true));
```

[https://3v4l.org/Q2WKQu](https://3v4l.org/Q2WKQu)

---

# ❌️ Assert Fail!

```
Fatal error: Uncaught Exception: Cannot traverse an already closed generator in /in/Q2WKQu:15
Stack trace:
#0 /in/Q2WKQu(15): iterator_to_array(Object(Generator))
#1 {main}
  thrown in /in/Q2WKQu on line 15

Process exited with code 255.
```

---

# テスト9️⃣
use は値渡し

- クロージャで `use($i)` としているため、値渡しでキャプチャされる
- クロージャ内で `$i++` を使っていても、外部の `$i` に影響しない
- 各ジェネレータインスタンスは独自のコピーの `$i` を持つ
- 各インスタンス内での増分は、そのインスタンスにのみ影響する
- 2 回目の assert びジェネレータ関数は再実行。3 回目は連続して呼び出していたのでエラーになった  
`Cannot traverse an already closed generator`

---

# テスト🔟 （持ち時間10秒）
テスト 9️⃣を参照渡しにするとどうなるか？

```php
<?php
$i = 1;
$generator = function() use(&$i) { // 参照渡しに変更
    yield $i++;
    yield $i++;
    yield $i++;
};
$gen = $generator();
$actual = iterator_to_array($gen);
assert([1, 2, 3] === $actual, var_export($actual, true));
assert(4 === $i);
$gen = $generator();
$actual = iterator_to_array($gen);
assert([4, 5, 6] === $actual, var_export($actual, true));
$gen->rewind(); // 最初に巻き戻す
$actual = iterator_to_array($gen);
assert([7, 8, 9] === $actual, var_export($actual, true));
```

[https://3v4l.org/Z2d4A](https://3v4l.org/Z2d4A)


---

# ❌️ Assert Fail!

```
Fatal error: Uncaught Exception: Cannot rewind a generator that was already run in /in/Z2d4A:15
Stack trace:
#0 /in/Z2d4A(15): Generator->rewind()
#1 {main}
  thrown in /in/Z2d4A on line 15

Process exited with code 255.
```

---

# テスト🔟 
途中まで期待通りだったが。。

- use で参照渡しにすると 1 回目と 2 回目のループの結果が変わってくる（期待通り）  
2 回目は別シーケンスとして動作する
- ジェネレータ関数に対して一度使用した後に `rewind()` は呼び出せない  
PHP のジェネレータ関数はシングルパス（一方通行）のイテレータとして実装されている  
[オフィシャルドキュメント](https://www.php.net/manual/ja/generator.rewind.php) で `イテレータを巻き戻す` となっているのが罠  
Generator オブジェクトだったら問題ない！
- 正しい使い方としては、新しいジェネレータインスタンスを作成する必要がある

---

# テスト⑪ （持ち時間10秒）
foreach を使わずに手続き的に書いてみる

```php
<?php
$i = 1;
$generator = function() use(&$i) {
    yield 'key1' => $i++;
    yield 'key2' => $i++;
};
$gen = $generator();
assert($i === 1);
$gen->rewind();
assert($i === 2);
assert($gen->current() === 1 && $gen->key() === 'key1' && $gen->valid());
$gen->next();
assert($i === 3);
assert($gen->current() === 2 && $gen->key() === 'key2' && $gen->valid());
$gen->next();
assert($i === 3);
assert($gen->current() === NULL && $gen->key() === NULL && $gen->valid() === false);
```

[https://3v4l.org/DiC1d](https://3v4l.org/DiC1d)

---

# ✅️ Assert Success!
Iterator インターフェイスの使い方がわかっていいね

---

# テスト⑪
foreach の内部がどうやって動いているか、おわかり頂けただろうか？

- `rewind()` は最初の yield までコードを実行する  
`rewind()` を呼び出さなくて直接　`current()` を呼び出しても問題なし
- 2 回目以降の `rewind()` は実際にジェネレーター関数をリセットしない  
例外が発生する（前述の通り）
- `next()` を呼ぶたびに次の `yield` まで進む
最後の `yield` の後に `next()` を呼ぶと `valid()` が `false` になる
- `current()` と `key()` は現在の要素のものにアクセスできる  
呼び出す前に既に生成自体は完了している

---

# テスト⑪
Iterator インターフェースを利用して for 文で書き直す！

```php
<?php
$generator = function() {
    yield 'key1' => 1;
    yield 'key2' => 2;
    yield from ['key3' => 3, 'key4' => 4];
};
$gen = $generator();
$actual = [];
for ($gen->rewind(); $gen->valid(); $gen->next()) {
    $actual[$gen->key()] = $gen->current(); 
}
$expected = [
    'key1' => 1,
    'key2' => 2,
    'key3' => 3,
    'key4' => 4
];
assert($expected === $actual, var_export($actual, true));
```

[https://3v4l.org/6vco4](https://3v4l.org/6vco4)

---

# テスト⑫ （持ち時間10秒）
参照を返すジェネレータだと。。？

```php
<?php
function &referenceValueGenerator(): iterable {
    list($key, $value) = ['key1', 1];
    yield $key => $value;
    list($key, $value) = [$key.'2', $value + 1];
    yield $key => $value;
    list($key, $value) = [$key.'3', $value + 2];
    yield $key => $value;
}
$actual = [];
foreach (referenceValueGenerator() as $key => &$value ) {
    $actual[$key] = $value;
    $value *= 10;
    $kye = "kee";
}
$expected = [
    'key1' => 1,
    'kee2' => 11,
    'kee3' => 112
];
assert($expected === $actual, var_export($actual, true));
```

[https://3v4l.org/4Hqs8](https://3v4l.org/4Hqs8)

---

# ❌️ Assert Fail!

```
Fatal error: Uncaught AssertionError: array (
  'key1' => 1,
  'key12' => 11,
  'key123' => 112,
) in /in/4Hqs8:21
Stack trace:
#0 /in/4Hqs8(21): assert(false, 'array (\n  'key1...')
#1 {main}
  thrown in /in/4Hqs8 on line 21

Process exited with code 255.
```

---

# テスト⑫
関数からリファレンスを返すのは PHP 標準機能！yield と組み合わせると強力

- 参照を返すジェネレータの定義方法  
関数名と値を参照する変数の前に `&` を付ける
- 参照を返すジェネレータでも、キーは参照として扱われない制限がある  
 `&` を付けちゃうと `Key element cannot be a reference` と怒られる  
- 値を受け取る変数の上書きすると、ジェネレータ内の値も更新される  
10 倍してプラスするという挙動となる
- キー値は値渡しになるので上書きしても変動しない

---

# テスト⑬ （持ち時間10秒）
双方向通信をもっとスマートにやるには？

```php
<?php
function communicatingGenerator(array $data = [1, 2, 3, 4]): Generator {
    $i = 0;
    $mode = null;
    do {
        $received = yield $data[$i];
        switch ($received ?? $mode) {
            case 'rev': $i--; $mode = 'rev'; break;
            case 'skip': $i += ($mode == 'rev' ? -2 : 2); break;
            default: $i++; $mode = 'fwd'; break;
        }
    } while ($i < 4 && $i >= 0);
}
$gen = communicatingGenerator();
$actual = [$gen->current(), // 1件目
  $gen->send("skip"),   // 2件目
  $gen->send("rev")];   // 3件目
$gen->next();
$actual[] = $gen->current();    // 4件目
$expected = [1, 3, 2, 1];
assert($expected === $actual, var_export($actual, true));
```

[https://3v4l.org/grWsu](https://3v4l.org/grWsu)

---

# ✅️ Assert Success!
Genarator::send()を利用して、順（逆）送りと skip を実現

---

# テスト⑬
ジェネレータを単なるデータ生成以上の使い方ができる非常に強力な機能

- 処理の動的な制御  
  - イテレーション中にジェネレータの動作をパラメータで調整できる
  - 条件に基づいて異なるデータセットを生成可能
- ステートマシンの実装  
  - ジェネレータが状態を保持し、外部からの入力に応じて状態遷移できる
  - コールバックやオブザーバーパターンの代替として使える
- 遅延評価と動的計算  
  - 計算の一部を遅延させ、必要なときに外部からパラメータを与えられる  
  - 複雑な計算を段階的に進められる

---

# テスト⑭ （持ち時間10秒）
例外も差し込めたりする

```php
<?php
function exceptionHandlingGenerator(array $data = [1, 2, 3]): Generator {
  $seek = 0;
  try {
    for ($seek = 0; $seek < count($data);) {
      $seek = yield $data[$seek];
    }
  } catch (Throwable $e) {
    return $data;
  }
}
$gen = exceptionHandlingGenerator();
$actual = [$gen->current(), $gen->send(2)];
try {
  $gen->throw(new Exception());
} catch (Throwable $e) {
  assert([1, 2, 3] == $gen->getReturn(), var_export($gen->getReturn(), true));
  assert([1, 3] === $actual, var_export($actual, true));
}
```

[https://3v4l.org/Vg18X](https://3v4l.org/Vg18X)

---

# ✅️ Assert Success!
Genarator::throw()を利用して、例外処理もできる

---

# テスト⑭
throw

- `throw()` メソッドでジェネレータ内に例外を注入します
- 注入された例外は、ジェネレータ内の実行中のコンテキストで発生します
- ジェネレータ内で例外をキャッチしない場合、例外は呼び出し元に伝播します
