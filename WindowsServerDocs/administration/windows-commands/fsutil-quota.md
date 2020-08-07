---
title: fsutil quota
description: Fsutil quota コマンドの参照記事。これは、NTFS ボリュームのディスククォータを管理して、ネットワークベースの記憶域をより細かく制御できるようにします。
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 21225c11-7c72-4ea2-96bd-e63d4beb3be5
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 7edf7ac908df419611fb42dd819323b15c8ded4e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889926"
---
# <a name="fsutil-quota"></a>fsutil quota

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

NTFS ボリュームのディスククォータを管理して、ネットワークベースの記憶域をより細かく制御できるようにします。

## <a name="syntax"></a>構文

```
fsutil quota [disable] <volumepath>
fsutil quota [enforce] <volumepath>
fsutil quota [modify] <volumepath> <threshold> <limit> <username>
fsutil quota [query] <volumepath>
fsutil quota [track] <volumepath>
fsutil quota [violations]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 無効化 (disable) | 指定されたボリュームでのクォータの追跡と適用を無効にします。 |
| 徹底 | 指定されたボリュームにクォータの使用を強制します。 |
| 変更 | 既存のディスククォータを変更するか、新しいクォータを作成します。 |
| query | 既存のディスククォータの一覧を表示します。 |
| track | 指定されたボリュームのディスク使用量を追跡します。 |
| 事項 | システムログとアプリケーションログを検索し、クォータ違反が検出されたか、ユーザーがクォータしきい値またはクォータ制限に達したことを示すメッセージを表示します。 |
| `<volumepath>` | 必須。 ドライブ名の後にコロン、または形式の GUID を指定し `volume{GUID}` ます。 |
| `<threshold>`  | 警告が発行される制限 (バイト単位) を設定します。 このパラメーターは、コマンドに必要です `fsutil quota modify` 。 |
| `<limit>` | 最大許容ディスク使用量 (バイト単位) を設定します。 このパラメーターは、コマンドに必要です `fsutil quota modify` 。 |
| `<username>` | ドメインまたはユーザー名を指定します。 このパラメーターは、コマンドに必要です `fsutil quota modify` 。 |

#### <a name="remarks"></a>Remarks

- ディスククォータはボリューム単位で実装され、ハードおよびソフトの両方の記憶域の制限をユーザーごとに実装することができます。

- 新しいユーザーを追加するたびにクォータ制限を設定したり、クォータ制限を自動的に追跡したり、レポートにコンパイルしたり、システム管理者に電子メールで自動的に送信したりするために、 **fsutil quota**を使用する書き込みスクリプトを使用できます。

### <a name="examples"></a>例

GUID を使用して指定されたディスクボリュームの既存のディスククォータを一覧表示するには、{92884 2df-5a01-11de 80-806e6f6e6963} と入力します。

```
fsutil quota query volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

ドライブ文字**C:** で指定されたディスクボリュームの既存のディスククォータを一覧表示するには、次のように入力します。

```
fsutil quota query C:
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)
