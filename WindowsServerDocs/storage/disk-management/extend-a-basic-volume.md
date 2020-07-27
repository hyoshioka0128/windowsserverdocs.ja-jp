---
title: ベーシック ボリュームを拡張する
description: Windows の既存のボリュームに領域を追加して、ドライブ上の空き領域に拡張することができます。ただし、空き領域にボリュームがなく (未割り当て)、間に他のボリュームがなく、拡張するボリュームのすぐ後にある場合に限ります。 この記事では、その方法について説明します。
ms.date: 12/19/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 19b48bd74dad4e20780b41852afbee15f5ec1ade
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966104"
---
# <a name="extend-a-basic-volume"></a>ベーシック ボリュームを拡張する

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ディスクの管理を使用して既存のボリュームに領域を追加して、ドライブ上の空き領域に拡張することができます。ただし、次の図に示すように、空き領域にボリュームがなく (未割り当て)、間に他のボリュームがなく、拡張するボリュームのすぐ後にある場合に限ります。 また、拡張するベーシック ボリュームが NTFS または ReFS ファイル システムでフォーマットされている必要もあります。

:::image type="content" source="media/extend-volume-space-highlighted.png" alt-text="ボリュームが拡張できる空き領域を示すディスクの管理。":::

## <a name="to-extend-a-volume-by-using-disk-management"></a>ディスクの管理を使用してボリュームを拡張するには

ボリュームをドライブ上のボリュームのすぐ後にある空き領域に拡張する方法を次に示します。

1. 管理者のアクセス許可でディスクの管理を開きます。

   そのための簡単な方法は、タスクバーの検索ボックスに「**コンピューターの管理**」と入力し、 **[コンピューターの管理]** を長押しし (または右クリックし)、 **[管理者として実行]**  >  **[はい]** の順に選択することです。 [コンピューターの管理] が開いたら、 **[ストレージ]**  >  **[ディスクの管理]** の順に移動します。
2. 拡張するボリュームを長押しし (または右クリックし)、 **[ボリュームの拡張]** を選択します。

   **[ボリュームの拡張]** がグレー表示されている場合は、次のことを確認してください。
    - ディスクの管理またはコンピューターの管理を管理者のアクセス許可で開いた状態
    - 上の図に示されているように、ボリュームのすぐ後 (右側) に未割り当て領域がある。 未割り当て領域と拡張するボリュームの間に別のボリュームがある場合は、中間のボリュームとそのボリュームのすべてのファイルを削除し (必ず、最初に重要なファイルをバックアップまたは移動してください)、データを破棄せずにボリュームを移動できる Microsoft 以外のディスク パーティション アプリを使用するか、ボリュームの拡張をスキップし、代わりに未割り当て領域に個別のボリュームを作成してください。
    - このボリュームが NTFS または ReFS ファイル システムでフォーマットされている。 その他のファイル システムでは拡張できません。そのため、ボリューム上のファイルを移動またはバックアップしてから、NTFS または ReFS ファイル システムでボリュームをフォーマットする必要があります。
    - ディスクが 2 TB を超える場合は、GPT パーティション構成を使用していることを確認してください。 ディスク上で 2 TB 以上を使用するには、GPT パーティション構成を使用して初期化する必要があります。 GPT に変換する場合は、「[MBR ディスクを GPT ディスクに変換する](change-an-mbr-disk-into-a-gpt-disk.md)」を参照してください。
    - それでもボリュームを拡張できない場合は、[Microsoft コミュニティ - ファイル、フォルダー、ストレージ](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639)のサイトを検索してみてください。答えが見つからない場合は、そこで質問を投稿してください。Microsoft、またはコミュニティの他のメンバーがヘルプを試みます。または、[Microsoft サポートにお問い合わせください](https://support.microsoft.com/contactus/)。

3. **[次へ]** を選択してから、ウィザードの **[ディスクの選択]** ページ (ここに示されています) で、拡張するボリュームの量を指定します。 通常は、使用可能なすべての空き領域を使用する既定値を使用しますが、空き領域に追加のボリュームを作成する場合は、小さい値を使用することもできます。

   :::image type="content" source="media/extend-volume-wizard.png" alt-text="使用可能なすべての領域を取得するために拡張されるボリュームを示すボリュームの拡張ウィザード":::

4. **[次へ]** を選択してから、 **[完了]** を選択してボリュームを拡張します。

## <a name="to-extend-a-volume-by-using-powershell"></a>PowerShell を使用してボリュームを拡張するには

1. [スタート] ボタンを長押しし (または右クリックし)、[Windows PowerShell (管理者)] を選択します。
2. *$drive_letter* 変数で拡張するボリュームのドライブ文字を指定して次のコマンドを入力し、ボリュームのサイズを最大サイズに変更します。

   ```PowerShell
   # Variable specifying the drive you want to extend
   $drive_letter = "C"

   # Script to get the partition sizes and then resize the volume
   $size = (Get-PartitionSupportedSize -DriveLetter $drive_letter)
   Resize-Partition -DriveLetter $drive_letter -Size $size.SizeMax
   ```

## <a name="see-slso"></a>関連項目

- [パーティションのサイズ変更](/powershell/module/storage/resize-partition)
- [DiskPart による拡張](../../administration/windows-commands/extend.md)
