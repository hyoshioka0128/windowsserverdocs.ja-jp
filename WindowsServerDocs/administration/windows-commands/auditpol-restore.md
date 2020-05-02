---
title: auditpol 復元
description: Auditpol 復元コマンドのリファレンストピック。このコマンドは、システム監査ポリシーの設定、すべてのユーザーのユーザーごとの監査ポリシー設定、および/backup オプションで使用されるコンマ区切り値 (CSV) ファイル形式と構文的に一致するファイルからのすべての監査オプションを復元します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ad73e520-484f-4cf1-a7f9-ae7488e9edf6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 64605a985c1cff13b842a99ae4ea52485bfc8220
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719060"
---
# <a name="auditpol-restore"></a>auditpol 復元

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

システム監査ポリシー設定、すべてのユーザーのユーザーごとの監査ポリシー設定、および/backup オプションで使用されるコンマ区切り値 (CSV) ファイル形式と構文的に一致するファイルからのすべての監査オプションを復元します。

*ユーザーごと*のポリシーと*システム*ポリシーに対して*復元*操作を実行するには、セキュリティ記述子でそのオブジェクトセットの**書き込み**または**フルコントロール**のアクセス許可を持っている必要があります。 "**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利を持っている場合は、*復元*操作を実行することもできます。これは、エラーや悪意のある攻撃が発生したときにセキュリティ記述子を復元する場合に便利です。

## <a name="syntax"></a>構文

```
auditpol /restore /file:<filename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| ------- | -------- |
| /file | 監査ポリシーの復元元のファイルを指定します。 このファイルは、/backup オプションを使用して作成されているか、/backup オプションで使用される CSV ファイル形式と構文的に一致している必要があります。 |
| /? |コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

システム監査ポリシー設定、すべてのユーザーのユーザーごとの監査ポリシー設定、および/backup コマンドを使用して作成された auditpolicy .csv という名前のファイルのすべての監査オプションを復元するには、次のように入力します。

```
auditpol /restore /file:c:\auditpolicy.csv
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [auditpol バックアップ](auditpol-backup.md)

- [auditpol コマンド](auditpol.md)
