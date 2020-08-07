---
title: fsutil transaction
description: NTFS トランザクションを管理する fsutil transaction コマンドのリファレンス記事です。
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: f70281af6ecf652cc1dba95ec09b07529f71752e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889800"
---
# <a name="fsutil-transaction"></a>fsutil transaction

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

NTFS トランザクションを管理します。

## <a name="syntax"></a>構文

```
fsutil transaction [commit] <GUID>
fsutil transaction [fileinfo] <filename>
fsutil transaction [list]
fsutil transaction [query] [{files | all}] <GUID>
fsutil transaction [rollback] <GUID>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| コミット (commit) | 暗黙的または明示的に指定されたトランザクションが正常に終了したことを示します。 |
| `<GUID>` | トランザクションを表す GUID 値を指定します。 |
| fileinfo  | 指定されたファイルのトランザクション情報を表示します。 |
| `<filename>` | 完全なパスとファイル名を指定します。 |
| list | 現在実行されているトランザクションの一覧を表示します。 |
| query | 指定されたトランザクションの情報を表示します。<ul><li>を指定した場合、 `fsutil transaction query files` ファイル情報は指定したトランザクションに対してのみ表示されます。</li><li>を指定した場合は `fsutil transaction query all` 、トランザクションのすべての情報が表示されます。</li></ul> |
| ロールバック | 指定されたトランザクションを先頭にロールバックします。 |

### <a name="examples"></a>例

ファイル*c:\test.txt*のトランザクション情報を表示するには、次のように入力します。

```
fsutil transaction fileinfo c:\test.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [トランザクション NTFS](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v=ws.10))
