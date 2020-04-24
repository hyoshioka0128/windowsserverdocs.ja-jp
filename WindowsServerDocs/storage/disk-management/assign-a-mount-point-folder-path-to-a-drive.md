---
title: ドライブにマウント ポイント フォルダー パスを割り当てます。
description: この記事では、ドライブに (ドライブ文字ではなく) マウント ポイント フォルダー パスを割り当てる方法について説明します。
ms.date: 06/07/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b2fda216b57fbf036ce20c40b4c8b38d44404f3c
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80815535"
---
# <a name="assign-a-mount-point-folder-path-to-a-drive"></a>ドライブにマウント ポイント フォルダー パスを割り当てる

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ディスクの管理を使用して、ドライブに (ドライブ文字ではなく) マウント ポイント フォルダー パスを割り当てることができます。 マウント ポイント フォルダー パスは、ベーシックまたはダイナミック NTFS ボリューム上の空のフォルダーに対してのみ使用できます。

## <a name="assigning-a-mount-point-folder-path-to-a-drive"></a>ドライブにマウント ポイント フォルダー パスを割り当てる

> [!NOTE]
> 以下の手順を実行するには、少なくとも **Backup Operators** または **Administrators** グループのメンバーである必要があります。

#### <a name="to-assign-a-mount-point-folder-path-to-a-drive-by-using-the-windows-interface"></a>Windows インターフェイスを使用して、ドライブにマウント ポイント フォルダー パスを割り当てるには

1.  ディスクの管理で、マウント ポイント フォルダー パスを割り当てるパーティションまたはボリュームを右クリックします。 
2. **[ドライブ文字とパスの変更]** をクリックし、 **[追加]** をクリックします。 
3. **[次の空の NTFS フォルダーにマウントする]** をクリックします。
4. NTFS ボリュームじょうの空のフォルダーへのパスを入力するか、 **[参照]** をクリックしてフォルダーを見つけます。

#### <a name="to-assign-a-mount-point-folder-path-to-a-drive-using-a-command-line"></a>コマンド ラインを使用してドライブにマウント ポイント フォルダー パスを割り当てるには

1.  コマンド プロンプトを開き、「`diskpart`」と入力します。

2.  **DISKPART** プロンプトで、「`list volume`」と入力し、パスを割り当てる対象のボリューム番号を書き留めます。

3.  **DISKPART** プロンプトで、「`select volume <volumenumber>`」と入力します。 

4. パスを割り当てるシンプル ボリュームの*ボリューム番号*を選択します。

5.  **DISKPART** プロンプトで、「`assign [mount=<path>]`」と入力します。

#### <a name="to-remove-a-mount-point-folder-path-to-a-drive"></a>ドライブのマウント ポイント フォルダー パスを削除するには

-   マウント ポイント フォルダー パスを削除するには、パスをクリックし、 **[削除]** をクリックします。

| 値 | 説明 |
| --- | --- |
| **list volume** | すべてのディスク上のベーシック ボリュームとダイナミック ボリュームの一覧を表示します。 |
| **select volume**        | <em>volumenumber</em> がボリューム番号である指定されたボリュームを選択し、そのボリュームにフォーカスを移動します。 ボリュームが指定されていない場合、**select** コマンドは、フォーカスがある現在のボリュームを一覧表示します。 番号、ドライブ文字、マウント ポイント フォルダー パスでボリュームを指定できます。 ベーシック ディスク上でボリュームを選択すると、対応するパーティションもフォーカスされます。|
| **assign** | <ul><li> フォーカスがあるボリュームにドライブ文字またはマウント ポイント フォルダー パスを割り当てます。 ドライブ文字またはマウント ポイント フォルダー パスが指定されていない場合は、次に利用可能なドライブ文字が割り当てられます。 ドライブ文字またはマウント ポイント フォルダー パスが既に使用中の場合、エラーが生成されます。</li>  <li>**assign** コマンドを使用して、リムーバブル ドライブに関連付けられているドライブ名を変更できます。</li> <li> ブート ボリュームまたはページング ファイルが含まれているボリュームにドライブ文字を割り当てることはできません。 さらに、Original Equipment Manufacturer (OEM) パーティション、EFI システム パーティション、またはベーシック データ パーティション以外の任意の GPT パーティションにドライブ文字を割り当てることはできません。</li></ul> |
| **mount=** <em>path</em> | マウントされたドライブが存在する、空の既存の NTFS フォルダーを指定します。  |

## <a name="additional-considerations"></a>その他の考慮事項

-   ローカルまたはリモート コンピューターを管理している場合は、そのコンピューター上の NTFS フォルダーを参照できます。
-   マウント ポイント フォルダー パスは、ベーシックまたはダイナミック NTFS ボリューム上の空のフォルダーに対してのみ使用できます。
-   マウント ポイント フォルダー パスを変更するには、フォルダー パスを削除し、新しい場所を使用して新しいフォルダー パスを作成します。 マウント ポイント フォルダー パスを直接変更することはできません。
-   ドライブにマウント ポイント フォルダー パスを割り当てるときに、**イベント ビューアー**を使用して、システム ログに、マウント ポイント フォルダー パスの障害を示す、クラスター サービスのエラーや警告がないことを確認します。 これらのエラーは、 **[ソース]** 列の **[ClusSvc]** と **[カテゴリ]** 列の **[物理ディスク リソース]** に表示されます。
-   [mountvol](https://go.microsoft.com/fwlink/?linkid=64111) コマンドを使用して、マウントされたドライブを作成することもできます。

## <a name="see-also"></a>関連項目
-   [コマンド ライン構文の表記規則](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


