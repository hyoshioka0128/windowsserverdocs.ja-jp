---
title: bootcfg addsw
description: 指定されたオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを追加する、bootcfg addsw コマンドの参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9d54c2cfdf898e1162d804220ae6dbb4a446fc5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926354"
---
# <a name="bootcfg-addsw"></a>bootcfg addsw

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを追加します。

## <a name="syntax"></a>構文

```
bootcfg /addsw [/s <computer> [/u <domain>\<user> /p <password>]] [/mm <maximumram>] [/bv] [/so] [/ng] /id <osentrylinenum>
```

### <a name="parameters"></a>パラメーター

| 用語 | 定義 |
| ---- | ---------- |
| `/s <computer>` | リモートコンピューターの名前または IP アドレスを指定します (円記号は使用しないでください)。 既定値はローカル コンピューターです。 |
| `/u <domain>\<user>`  | またはによって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行し `<user>` `<domain>\<user>` ます。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
| `/p <password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 |
| `/mm <maximumram>` | オペレーティングシステムが使用できる RAM の最大容量を mb 単位で指定します。 値は 32 Mb 以上である必要があります。 |
| /bv | 指定されたに **/basevideo**オプションを追加し `<osentrylinenum>` 、インストールされているビデオドライバーの標準 VGA モードを使用するようにオペレーティングシステムに指示します。 |
| /so | 指定されたに **/sos**オプションを追加し `<osentrylinenum>` 、読み込まれているときにデバイスドライバー名を表示するようにオペレーティングシステムに指示します。 |
| /ng | 指定されたに **/noguiboot**オプションを追加し `<osentrylinenum>` 、CTRL + ALT + DEL ログオンプロンプトの前に表示される進行状況バーを無効にします。 |
| `/id <osentrylinenum>` | オペレーティングシステムの読み込みオプションが追加される Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

**Bootcfg/addsw**コマンドを使用するには、次のようにします。

```
bootcfg /addsw /mm 64 /id 2
bootcfg /addsw /so /id 3
bootcfg /addsw /so /ng /s srvmain /u hiropln /id 2
bootcfg /addsw /ng /id 2
bootcfg /addsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bootcfg コマンド](bootcfg.md)
