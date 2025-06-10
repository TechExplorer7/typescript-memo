# ステータス定義と型の管理方法

## ステータス定義

以下のように、Status オブジェクトと型を定義します。

```ts
export const Status = {
  Pending: "01",
  InProgress: "02",
  Completed: "03",
  Canceled: "04",
} as const;

export type Status = (typeof Status)[keyof typeof Status];
```

## 使用例

変数への代入

```ts
let currentStatus: Status = Status.Pending;
```

ステータスチェック

```ts
if (currentStatus === Status.Completed) {
  console.log("処理が完了しました");
}
```

ステータスを使った条件分岐

```ts
switch (currentStatus) {
  case Status.Pending:
    console.log("未処理です");
    break;
  case Status.InProgress:
    console.log("処理中です");
    break;
  case Status.Completed:
    console.log("完了しています");
    break;
  case Status.Canceled:
    console.log("キャンセルされました");
    break;
}
```

## 説明

### typeof の使い方

TypeScript では、値 Status の型情報を取得したいときに typeof を使います。

```ts
typeof Status

↓

{
  readonly Pending: "01";
  readonly InProgress: "02";
  readonly Completed: "03";
  readonly Canceled: "04";
}
```

## keyof typeof Status の意味

keyof を使うと、そのオブジェクトのキーを列挙したユニオン型になります。

```ts
keyof typeof Status

↓

"Pending" | "InProgress" | "Completed" | "Canceled"
```

### `(typeof Status)[keyof typeof Status]` の意味

オブジェクトのキーに対応する値の型を取り出すための記法です。

```ts
(typeof Status)[keyof typeof Status]

↓

"01" | "02" | "03" | "04"
```

### さらに補足

インデックスアクセス型の構文

```ts
オブジェクト型["プロパティ名"];

type A = { foo: number };
type Foo = A["foo"];
// type Foo = number
```

インデックスアクセス型にはユニオン型も使えます。

```ts
type Person = { name: string; age: number };
type T = Person["name" | "age"];
// type T = string | number
```

keyof 型演算子と組み合わせると、オブジェクトの全プロパティの型がユニオン型で得られます。

```ts
type Foo = { a: number; b: string; c: boolean };
type T = Foo[keyof Foo];
// type T = string | number | boolean
```
