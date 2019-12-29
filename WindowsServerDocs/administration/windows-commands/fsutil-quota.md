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
ms.openlocfilehash: 5e1c6793ca866ecacd8b00aa7e01d632c2538405
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376837"
---
# <a name="fsutil-quota"></a>Fsutil クォータ
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

NTFS ボリュームのディスククォータを管理して、ネットワークベースの記憶域をより細かく制御できるようにします。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
fsutil quota [disable] <VolumePath>
fsutil quota [enforce] <VolumePath>
fsutil quota [modify] <VolumePath> <Threshold> <Limit> <UserName>
fsutil quota [query] <VolumePath>
fsutil quota [track] <VolumePath>
fsutil quota [violations]
```

## <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                                    説明                                                                                    |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    無効化    |                                                         指定されたボリュームでのクォータの追跡と適用を無効にします。                                                          |
|    徹底    |                                                                   指定されたボリュームにクォータの使用を強制します。                                                                   |
|    変更     |                                                              既存のディスククォータを変更するか、新しいクォータを作成します。                                                              |
|     クエリ (query)     |                                                                            既存のディスククォータの一覧を表示します。                                                                            |
|     軌道     |                                                                    指定されたボリュームのディスク使用量を追跡します。                                                                     |
|  事項   | システムログとアプリケーションログを検索し、クォータ違反が検出されたか、ユーザーがクォータしきい値またはクォータ制限に達したことを示すメッセージを表示します。 |
| \<VolumePath > |                                  必須。 ドライブ名の後にコロン、または**ボリューム {** <em>guid</em> **}** の形式の GUID を指定します。                                  |
| \<Threshold >  |                            警告が発行される制限 (バイト単位) を設定します。 このパラメーターは、 **fsutil quota modify**コマンドに必要です。                            |
|   \<Limit >    |                                最大許容ディスク使用量 (バイト単位) を設定します。 このパラメーターは、 **fsutil quota modify**コマンドに必要です。                                |
|  \<UserName >  |                                      ドメインまたはユーザー名を指定します。 このパラメーターは、 **fsutil quota modify**コマンドに必要です。                                       |

## <a name="remarks"></a>コメント

-   ディスククォータはボリューム単位で実装され、ハードおよびソフトの両方の記憶域の制限をユーザーごとに実装することができます。

-   新しいユーザーを追加するたびにクォータ制限を設定したり、クォータ制限を自動的に追跡したり、レポートにコンパイルしたり、システム管理者に電子メールで自動的に送信したりするために、 **fsutil quota**を使用する書き込みスクリプトを使用できます。

### <a name="BKMK_examples"></a>例
GUID を使用して指定されたディスクボリュームの既存のディスククォータを一覧表示するには、{92884 2df-5a01-11de 80-806e6f6e6963} と入力します。

```
fsutil quota query Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

ドライブ文字**C:** で指定されたディスクボリュームの既存のディスククォータを一覧表示するには、次のように入力します。

```
Fsutil quota query C:
```

#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


