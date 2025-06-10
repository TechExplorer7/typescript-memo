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
