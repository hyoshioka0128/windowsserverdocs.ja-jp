---
title: wbadmin start systemstatebackup
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 998366c1-0a64-45e6-9ed3-4c3f5b8406f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0244f984d29c8a802475d2dc08f1cdfe4495f0b9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362231"
---
# <a name="wbadmin-start-systemstatebackup"></a>wbadmin start systemstatebackup



ローカルコンピューターのシステム状態のバックアップを作成し、指定した場所に保存します。

> [!NOTE]
> Windows Server バックアップはバックアップまたはシステム状態のバックアップまたはシステム状態の回復の一部としてユーザーのレジストリ ハイブ (HKEY_CURRENT_USER) を回復します。

このサブコマンドを使用してシステム状態のバックアップを実行するには、 **Backup Operators**グループまたは**Administrators**グループのメンバであるか、適切な権限が委任されている必要があります。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でのコマンドプロンプトを開くには、 **[コマンドプロンプト]** を右クリックし、 **[管理者として実行]** をクリックします)。

このサブコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

## <a name="syntax"></a>構文

```
wbadmin start systemstatebackup
-backupTarget:<VolumeName>
[-quiet]
```

## <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                                                                                                                                                                      説明                                                                                                                                                                                                                      |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -backuptarget | バックアップを保存する場所を指定します。 記憶域の場所には、次の形式のドライブ文字または GUID ベースのボリュームが必要です: \\\\? \ volume{*guid*}。</br>Windows Server 2008 を実行しているコンピューターでは、共有ネットワークフォルダーへのシステム状態のバックアップはサポートされていません。 サーバーで Windows Server 2008 R2 以降が実行されている場合は、 **backuptarget:\\\\servername\sharedFolder\\** を使用して、システム状態のバックアップを格納できます。 |
|    -通知の停止     |                                                                                                                                                                                                   ユーザーにプロンプトを表示せずにサブコマンドを実行します。                                                                                                                                                                                                    |

## <a name="remarks"></a>注釈

システム状態のバックアップをボリュームに保存する方法については、Microsoft サポート技術情報の記事 944530 ([https://go.microsoft.com/fwlink/?LinkId=110439](https://go.microsoft.com/fwlink/?LinkId=110439)) を参照してください。

## <a name="BKMK_examples"></a>例

システム状態のバックアップを作成し、ボリューム f に保存するには、次のように入力します。
```
wbadmin start systemstatebackup -backupTarget:f:
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBBackup](https://technet.microsoft.com/library/jj902459.aspx)コマンドレット