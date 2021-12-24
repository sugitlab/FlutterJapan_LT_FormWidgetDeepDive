---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Flutter Japan LT slide

  26 Dec. 2021

drawings:
  persist: false
title: Form Widget Deep Dive
---

# Form Widget Deep Dive 

Form Widget を **正しく** 使いこなそう

---

# Text Input Form
基本のフォーム

まずはテキストを入力するだけのテキストボックスを対象にします。

```dart
Form(
  child: TextFormField(),
)
```

Form Widget を親に、TextFormField Widget を子に指定しています。

これが **基本のForm** です。

---

# Demo 
入力欄のみ

何も設定をしない場合は、ただ文字を入力するだけになります。

<iframe width="120%" height="500" style="transform:scale(0.8); transform-origin:0 0;" src="https://dartpad.dev/?id=dfa70f46920b1b1d1a18815283c40f2b" />

[Gist](https://gist.github.com/sugitlab/dfa70f46920b1b1d1a18815283c40f2b)
[DartPad](https://dartpad.dev/dfa70f46920b1b1d1a18815283c40f2b)

---

# TextFormField - InputDecoration

```dart
TextFormField(
  decoration: InputDecoration(
    labelText: 'Label',
    hintText: 'Hint',
    helperText: 'Helper',
  ),
)
```

入力フォームにデコレーションを施すことができます。

- labelText
- helperText
- hintText
- ...

---

# Demo
InputDecoration

ラベル・へルパー・ヒントの表示箇所はこんな感じになります。

<iframe width="120%" height="500" style="transform:scale(0.8); transform-origin:0 0;" src="https://dartpad.dev/?id=e793bcb1568a1dc9a0bdf7a4e5b8cc49" />

---

# Validator
入力の検証

バリデーター（値の検証）を設定します。

```dart
TextFormField(
  validator: (value) {
    if (value == null || value.isEmpty) {
      return 'Please enter some text.';
    } else {
      return null;
    }
  }
),
```

とりあえず、フォームが空っぽの時にメッセージを、そうでなければnullを返すようにしてみました。

この validator はいつのタイミングで実行されるのでしょう?

---

# Demo
validate()

TextFormFieldをラップするFormウィジェットのKeyを使って、validate()メソッドを呼び出します。 <br>
validate()メソッドはそのFormに含まれるすべてのFormFieldのvalidatorを実行します。

<iframe width="120%" height="500" style="transform:scale(0.8); transform-origin:0 0;" src="https://dartpad.dev/c5e4c4a4d5eb6de72ef391945e2d842e" />

---

# Form と Field

何が違う??

Form Widget と TextFormField Widget を使用してきました。

Validatorを使うことで、ちょっとFormが役に立ったように見えます。

しかし、Formがなくとも Validation は可能です。

```dart
TextFormField(
  validator: (value) {
    if (value == null || value.length < 5) {
      return 'Please enter some text.';
    } else {
      return null;
    }
  },
  autovalidateMode: AutovalidateMode.onUserInteraction,
),
```

---

# Demo
autovalidate

autovalidateModeをonUserInteractionにすると、入力の変更を逐一チェックしてバリデーションします。

ちょっと鬱陶しいですね。

<iframe width="120%" height="400" style="transform:scale(0.8); transform-origin:0 0;" src="https://dartpad.dev/?id=f7218b92ad1444f72f85a5c316ef669b" />

---

# TextFormFieldを2つにしてみよう
複数のField

```dart
Column(
  mainAxisAlignment: MainAxisAlignment.center,
  children: [
    TextFormField(
      decoration: const InputDecoration(labelText:'Form1'),
      validator: (value) {
        // 省略
      },
    ),
    TextFormField(
      decoration: const InputDecoration(labelText:'Form2'),
      validator: (value) {
        // 省略
      },
    ),
  ],
),

```

---

# Fieldをまとめて ほげほげ したい
ってことがあるんですよね

- まとめて一気にバリデーション
- まとめて一気に入力初期化

そんなケースがよくあります。


---

# Demo
validateとreset

<iframe width="120%" height="500" style="transform:scale(0.8); transform-origin:0 0;" src="https://dartpad.dev/?id=5a123c3fc4832490a00dde626febe23c" />

---

# hoge