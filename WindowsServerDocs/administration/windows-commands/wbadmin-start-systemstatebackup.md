---
title: wbadmin start systemstatebackup
description: Wbadmin start systemstatebackup の Windows コマンドのトピック。ローカルコンピューターのシステム状態のバックアップを作成し、指定した場所に保存します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 998366c1-0a64-45e6-9ed3-4c3f5b8406f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ecbf5a055684026413615a104b4c983ff51ca9e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829575"
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

### <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                                                                                                                                                                      説明                                                                                                                                                                                                                      |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -backuptarget | バックアップを保存する場所を指定します。 記憶域の場所には、次の形式のドライブ文字または GUID ベースのボリュームが必要です: \\\\? \ volume{*guid*}。</br>Windows Server 2008 を実行しているコンピューターでは、共有ネットワークフォルダーへのシステム状態のバックアップはサポートされていません。 サーバーで Windows Server 2008 R2 以降が実行されている場合は、 **backuptarget:\\\\servername\sharedFolder\\** を使用して、システム状態のバックアップを格納できます。 |
|    -quiet     |                                                                                                                                                                                                   ユーザーにプロンプトを表示せずにサブコマンドを実行します。                                                                                                                                                                                                    |

## <a name="remarks"></a>コメント

システム状態のバックアップをボリュームに保存する方法については、Microsoft サポート技術情報の記事 944530 ([https://go.microsoft.com/fwlink/?LinkId=110439](https://go.microsoft.com/fwlink/?LinkId=110439)) を参照してください。

## <a name="examples"></a><a name=BKMK_examples></a>例

システム状態のバックアップを作成し、ボリューム f に保存するには、次のように入力します。
```
wbadmin start systemstatebackup -backupTarget:f:
```

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBBackup](https://technet.microsoft.com/library/jj902459.aspx)コマンドレット