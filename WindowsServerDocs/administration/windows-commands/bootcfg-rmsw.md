---
title: bootcfg rmsw
description: 指定されたオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを削除する、bootcfg rmsw コマンドの参照記事。
ms.topic: article
ms.assetid: fd7e4248-880e-4e2b-929e-87f8d44b9a63
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ffe80c6a95421a66a1aebd119664c9e4f68952d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880544"
---
# <a name="bootcfg-rmsw"></a>bootcfg rmsw

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを削除します。

## <a name="syntax"></a>構文

```
bootcfg /rmsw [/s <computer> [/u <domain>\<user> /p <password>]] [/mm] [/bv] [/so] [/ng] /id <osentrylinenum>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `/s <computer>` | リモートコンピューターの名前または IP アドレスを指定します (円記号は使用しないでください)。 既定値はローカル コンピューターです。 |
| `/u <domain>\<user>`  | またはによって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行し `<user>` `<domain>\<user>` ます。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
| `/p <password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 |
| /mm | /Maxmem オプションとそれに関連付けられている最大メモリ値を、指定したから削除し `<osentrylinenum>` ます。 /Maxmem オプションは、オペレーティングシステムが使用できる RAM の最大量を指定します。 |
| /bv | 指定したから/basevideo オプションを削除し `<osentrylinenum>` ます。 /Basevideo オプションは、インストールされているビデオドライバーの標準 VGA モードを使用するようにオペレーティングシステムに指示します。 |
| /so | 指定したから/sos オプションを削除し `<osentrylinenum>` ます。 /Sos オプションは、ドライバーの読み込み中にデバイスドライバー名を表示するようにオペレーティングシステムに指示します。 |
| /ng | 指定したから/noguiboot オプションを削除し `<osentrylinenum>` ます。 /Noguiboot オプションを指定すると、CTRL + ALT + DEL ログオンプロンプトの前に表示される進行状況バーが無効になります。 |
| `/id <osentrylinenum>` | オペレーティングシステムの読み込みオプションが追加される Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

**Bootcfg/rmsw**コマンドを使用するには、次のようにします。

```
bootcfg /rmsw /mm 64 /id 2
bootcfg /rmsw /so /id 3
bootcfg /rmsw /so /ng /s srvmain /u hiropln /id 2
bootcfg /rmsw /ng /id 2
bootcfg /rmsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bootcfg コマンド](bootcfg.md)
