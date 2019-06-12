---
title: wbadmin start systemstatebackup
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d98ba295b2a76baf98e85a01a02677d57922877d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440265"
---
# <a name="wbadmin-start-systemstatebackup"></a>wbadmin start systemstatebackup



ローカル コンピューターのシステム状態のバックアップを作成し、指定された場所に保存します。

> [!NOTE]
> Windows Server バックアップはバックアップまたはシステム状態のバックアップまたはシステム状態の回復の一部としてユーザーのレジストリ ハイブ (HKEY_CURRENT_USER) を回復します。

このサブコマンドでシステム状態のバックアップを実行するには、メンバーである、 **Backup Operators**グループまたは**管理者**グループ、またはをされている必要が適切なアクセス許可を委任します。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (を開き、管理者特権でコマンド プロンプトを右クリック**コマンド プロンプト**、 をクリックし、**管理者として実行**)。

このサブコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文

```
wbadmin start systemstatebackup
-backupTarget:<VolumeName>
[-quiet]
```

## <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                                                                                                                                                                      説明                                                                                                                                                                                                                      |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -backuptarget | バックアップを格納する場所を指定します。 記憶域の場所は、ドライブ文字または形式の GUID ベースのボリュームが必要です: \\ \\? \Volume {*GUID*}。</br>Windows Server 2008 を実行するコンピューターでは、共有ネットワーク フォルダーへのシステム状態のバックアップはサポートされていません。 サーバーには、Windows Server 2008 R2 が実行されているか、後でコマンドを使用することができる場合 **-backuptarget:\\\\servername\sharedFolder\\** システム状態のバックアップを格納します。 |
|    -通知の停止     |                                                                                                                                                                                                   ユーザーにプロンプトなしで、サブコマンドを実行します。                                                                                                                                                                                                    |

## <a name="remarks"></a>注釈

ボリュームにシステム状態のバックアップを保存する方法については、システム状態ファイル、さらに、含まれています。 944530 でマイクロソフト サポート技術情報の記事を参照してください。 ([https://go.microsoft.com/fwlink/?LinkId=110439](https://go.microsoft.com/fwlink/?LinkId=110439))。

## <a name="BKMK_examples"></a>例

システム状態のバックアップを作成してボリューム f に保存、次のように入力します。
```
wbadmin start systemstatebackup -backupTarget:f:
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [開始 WBBackup](https://technet.microsoft.com/library/jj902459.aspx)コマンドレット