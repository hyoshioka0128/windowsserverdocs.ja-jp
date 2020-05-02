---
ms.assetid: 21225c11-7c72-4ea2-96bd-e63d4beb3be5
title: Fsutil クォータ
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 8079bacaa54282a1dd1091ffacd427ddaf74cc59
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725472"
---
# <a name="fsutil-quota"></a>Fsutil クォータ
> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

NTFS ボリュームのディスククォータを管理して、ネットワークベースの記憶域をより細かく制御できるようにします。



## <a name="syntax"></a>構文

```
fsutil quota [disable] <VolumePath>
fsutil quota [enforce] <VolumePath>
fsutil quota [modify] <VolumePath> <Threshold> <Limit> <UserName>
fsutil quota [query] <VolumePath>
fsutil quota [track] <VolumePath>
fsutil quota [violations]
```

### <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                                    [説明]                                                                                    |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    無効化 (disable)    |                                                         指定されたボリュームでのクォータの追跡と適用を無効にします。                                                          |
|    徹底    |                                                                   指定されたボリュームにクォータの使用を強制します。                                                                   |
|    変更     |                                                              既存のディスククォータを変更するか、新しいクォータを作成します。                                                              |
|     query     |                                                                            既存のディスククォータの一覧を表示します。                                                                            |
|     track     |                                                                    指定されたボリュームのディスク使用量を追跡します。                                                                     |
|  事項   | システムログとアプリケーションログを検索し、クォータ違反が検出されたか、ユーザーがクォータしきい値またはクォータ制限に達したことを示すメッセージを表示します。 |
| \<VolumePath> |                                  必須。 ドライブ名の後にコロン、または**ボリューム {**<em>guid</em>**}** の形式の GUID を指定します。                                  |
| \<しきい値>  |                            警告が発行される制限 (バイト単位) を設定します。 このパラメーターは、 **fsutil quota modify**コマンドに必要です。                            |
|   \<制限>    |                                最大許容ディスク使用量 (バイト単位) を設定します。 このパラメーターは、 **fsutil quota modify**コマンドに必要です。                                |
|  \<ユーザー名>  |                                      ドメインまたはユーザー名を指定します。 このパラメーターは、 **fsutil quota modify**コマンドに必要です。                                       |

## <a name="remarks"></a>Remarks

-   ディスククォータはボリューム単位で実装され、ハードおよびソフトの両方の記憶域の制限をユーザーごとに実装することができます。

-   新しいユーザーを追加するたびにクォータ制限を設定したり、クォータ制限を自動的に追跡したり、レポートにコンパイルしたり、システム管理者に電子メールで自動的に送信したりするために、 **fsutil quota**を使用する書き込みスクリプトを使用できます。

### <a name="examples"></a><a name="BKMK_examples"></a>例
GUID を使用して指定されたディスクボリュームの既存のディスククォータを一覧表示するには、{92884 2df-5a01-11de 80-806e6f6e6963} と入力します。

```
fsutil quota query Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

ドライブ文字**C:** で指定されたディスクボリュームの既存のディスククォータを一覧表示するには、次のように入力します。

```
Fsutil quota query C:
```

## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


