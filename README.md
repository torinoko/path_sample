# これなに

ファイルのパスを説明するためのリポジトリです。

# 前提

以下のようなディレクトリ構成になっています。
```
+ path_sample/
  ├ sample_absolute_path.rb
  ├ sample_relative_path.rb
  ├ foo/
  │  └ bar/
  │    └ baz.txt
  └ hoge/
      └ sample.rb
```

# 確認手順

このリポジトリを clone して移動します。
```
$ git clone https://github.com/torinoko/path_sample.git
$ cd path_sample
```
以降、path_sample ディレクトリ以下で実行します。

## 読み込むファイル

以下のコマンドでファイルの中身を確認してみてください。
```
$ cat foo/bar/baz.txt
```

Hello! という文字列が表示されるはずです。  
これが baz.txt に書かれている内容です。

## 相対パスでファイルを開くプログラムを実行してみる

ファイルの中身を確認してみます。  
1行目、 path が相対パスで書かれていることを確認してください。
```
$ cat sample_relative_path.rb
```

Ruby のファイルを実行します。
```
$ ruby sample_relative_path.rb
```

以下のような表示があれば OK です！
```
path: foo/bar/baz.txt
Hello!
```

## 絶対パスでファイルを開くプログラムを実行してみる

ファイルの中身を確認してみます。  
1行目、 path が絶対パスで書かれていることを確認してください。  
`__dir__` で現在のファイルパスを取得できます。  
これに相対パスを合わせると絶対パスを作れます。
```
$ cat sample_absolute_path.rb
```

Ruby のファイルを実行します。
```
$ ruby sample_absolute_path.rb
```

以下のような表示があれば OK です！  
path の一部は実行環境により異なります。
```
path: /Users/user/path_sample/foo/bar/baz.txt
Hello!
```

## 相対パスでファイルを開くプログラムを実行してみる（再）

ファイルの中身を確認してみます。  
1行目、 path が相対パスで書かれていることを確認してください。
```
$ cat hoge/sample.rb
```

Ruby のファイルを実行します。
```
$ ruby hoge/sample.rb
```

以下のような表示があれば OK です！  
hoge ディレクトリの下にファイルが置かれていますが、実行しているのは sample_path 直下のため、相対パスでもファイルを読み込むことができます。
```
path: foo/bar/baz.txt
Hello!
```

## 相対パスでファイルを開くプログラムを実行してみる（再々）

sample.rb のあるディレクトリへ移動します。
```
$ cd hoge
```

Ruby のファイルを実行します。
```
$ ruby sample.rb
```

以下のような表示があれば OK です！  
現在地は hoge なので、 foo/bar 以下にある baz.txt を見つけられず、読み込むことに失敗しています。
```
path: foo/bar/baz.txt
Traceback (most recent call last):
	1: from sample.rb:3:in `<main>'
sample.rb:3:in `read': No such file or directory @ rb_sysopen - foo/bar/baz.txt (Errno::ENOENT)
```

