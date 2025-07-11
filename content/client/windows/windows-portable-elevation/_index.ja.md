---
title: Windows ポータブル昇格
weight: 49
---

Windowsポータブルプログラムには管理者権限がないため、以下の問題が発生する可能性があります：

- UAC（ユーザーアカウント制御）ウィンドウがポップアップしたときに画面を送信できない。
- タスクマネージャーなどの昇格されたウィンドウがポップアップしたときに、マウスが反応しなくなる。

権限を昇格することで、RustDeskは起動時またはセッション中に管理者権限を持つプロセスを作成でき、スクリーンショットとマウス操作を実行できるようになり、上記の問題を回避できます。

## 起動時に昇格

この方法では、リモートユーザーは接続時に昇格を要求する必要がありません。2つの方法があります：

* 方法1：ポータブルプログラムの名前を `-qs-` を含むように変更します（1.2.0、1.2.1、1.2.2、1.2.3バージョンは `qs.exe` で終わります）。左マウスボタンをクリックして実行し、UACウィンドウで `受け入れる` をクリックします。

* 方法2：右クリックして管理者として実行します。

## 制御される側で昇格

制御される側は、接続時に直接 `受け入れて昇格` をクリックするか、既に接続されている場合は `昇格` をクリックできます。

| 接続中 | 接続済み |
| :---: | :---: |
| ![](/docs/en/client/windows/windows-portable-elevation/images/cm_unauth.jpg) | ![](/docs/en/client/windows/windows-portable-elevation/images/cm_auth.jpg) |

## 制御側で昇格を要求

アクションメニューから `昇格を要求` を選択すると、以下のダイアログボックスが表示されます。`リモートユーザーに認証を求める` を選択した場合、ユーザー名とパスワードを入力する必要はありませんが、リモートコンピューターのユーザーは管理者権限を持っている必要があります。`管理者のユーザー名とパスワードを送信` を選択した場合、リモートコンピューターのユーザーはUACウィンドウで受け入れるだけで済みます。リクエストを送信した後、相手側がUACウィンドウを受け入れるのを待ってください。確認後、成功メッセージが表示されます。**どちらの方法も制御される側で誰かがUACウィンドウを受け入れる必要があります**。したがって、相手側に誰も利用できない場合は、制御側で昇格を要求すべきではありません。

| メニュー | ダイアログ |
| :---: | :---: |
| ![](/docs/en/client/windows/windows-portable-elevation/images/menu.png) | ![](/docs/en/client/windows/windows-portable-elevation/images/dialog.png) |
| **待機** | **成功** |
| ![](/docs/en/client/windows/windows-portable-elevation/images/wait.png) | ![](/docs/en/client/windows/windows-portable-elevation/images/success.png) |

## 選択方法

| シナリオ | 方法 |
| :---: | :---: |
| 昇格が不要 | プログラムをインストール |
| 制御される側にユーザーが利用できない | リネーム<br/>*または*<br/> 管理者として実行 |
| 制御される側にユーザーが利用可能<br/>*かつ*<br/> 接続時に即座に昇格<br/>*かつ*<br/> 受け入れクリック接続 | 制御される側で接続を受信するときに `受け入れて昇格` をクリック |
| 制御される側にユーザーが利用可能<br/>*かつ*<br/> 必要に応じて昇格 | 制御される側の接続管理ウィンドウで `昇格` をクリック<br/>*または*<br/> 制御側で昇格を要求 |