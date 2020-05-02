---
title: bootcfg addsw
description: 指定されたオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを追加する、bootcfg addsw コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 17abdc1ba28afad173ea6486519277916f08ad3d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709944"
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
| `/s <computer>` | リモートコンピューターの名前または IP アドレスを指定します (円記号は使用しないでください)。 既定はローカル コンピュータです。 |
| `/u <domain>\<user>`  | または`<user>` `<domain>\<user>`によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
| `/p <password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 |
| `/mm <maximumram>` | オペレーティングシステムが使用できる RAM の最大容量を mb 単位で指定します。 値は 32 Mb 以上である必要があります。 |
| /bv | 指定さ **/basevideo** `<osentrylinenum>`れたに/basevideo オプションを追加し、インストールされているビデオドライバーの標準 VGA モードを使用するようにオペレーティングシステムに指示します。 |
| /so | 指定さ **/sos** `<osentrylinenum>`れたに/sos オプションを追加し、読み込まれているときにデバイスドライバー名を表示するようにオペレーティングシステムに指示します。 |
| /ng | 指定さ **/noguiboot** `<osentrylinenum>`れたに/noguiboot オプションを追加し、CTRL + ALT + DEL ログオンプロンプトの前に表示される進行状況バーを無効にします。 |
| `/id <osentrylinenum>` | オペレーティングシステムの読み込みオプションを追加する Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。 |
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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bootcfg コマンド](bootcfg.md)
