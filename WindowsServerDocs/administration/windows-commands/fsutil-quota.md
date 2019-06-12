---
ms.assetid: 21225c11-7c72-4ea2-96bd-e63d4beb3be5
title: Fsutil クォータ
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 1e844d73348ee31f309f44895831ded9a2e6365c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439061"
---
# <a name="fsutil-quota"></a>Fsutil クォータ
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

ネットワーク ベースの記憶域をより正確に制御を提供する NTFS ボリューム上のディスク クォータを管理します。

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
|    無効化    |                                                         クォータの追跡と指定されたボリュームでの強制を無効にします。                                                          |
|    適用します。    |                                                                   指定されたボリュームでクォータ使用率を適用します。                                                                   |
|    変更     |                                                              既存のディスク クォータを変更します。 または、新しいクォータを作成します。                                                              |
|     query     |                                                                            既存のディスク クォータの一覧を表示します。                                                                            |
|     トラック     |                                                                    ディスクの指定されたボリュームでの使用状況を追跡します。                                                                     |
|  違反   | システムおよびアプリケーションのログを検索し、クォータ違反が検出されたこと、またはユーザーがクォータのしきい値またはクォータの上限に達したことを示すメッセージが表示されます。 |
| \<VolumePath > |                                  必須。 ドライブ名の後にコロンまたは形式の GUID を指定します**ボリューム {** <em>GUID</em> **}** します。                                  |
| \<しきい値 >  |                            警告が発行された日時です (バイト単位) での制限を設定します。 このパラメーターが必要です、 **fsutil クォータの変更**コマンド。                            |
|   \<制限値 >    |                                許可された最大ディスク使用量をバイト単位で設定します。 このパラメーターが必要です、 **fsutil クォータの変更**コマンド。                                |
|  \<ユーザー名 >  |                                      ドメインまたはユーザー名を指定します。 このパラメーターが必要です、 **fsutil クォータの変更**コマンド。                                       |

## <a name="remarks"></a>注釈

-   ディスク クォータは、ボリュームごとに実装され、両方のハードおよびソフトの記憶域制限をユーザーごとに実装できるようにします。

-   使用するスクリプトを記述を使用する**fsutil クォータ**新しいユーザーを追加するたびに、クォータ制限を設定またはクォータの制限値を自動的に追跡するには、コンパイルして、レポートにし、自動的に電子メールでシステム管理者に送信します。

### <a name="BKMK_examples"></a>例
{928842df-5a01-11de-a85c-806e6f6e6963}、GUID で指定されているディスク ボリュームの既存のディスク クォータの一覧を表示するには、次のように入力します。

```
fsutil quota query Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

既存のディスク クォータをドライブ文字で指定されているディスク ボリュームの一覧を表示する**c:** 種類。

```
Fsutil quota query C:
```

#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


