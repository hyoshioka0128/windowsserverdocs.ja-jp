---
title: "ダイナミック ディスクからベーシック ディスクへの再変換"
description: "ダイナミック ディスクをベーシック ディスクに再変換する方法について説明します。"
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 9675141ec02c2362702265a18f5405554dff6038
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="change-a-dynamic-disk-back-to-a-basic-disk"></a>ダイナミック ディスクからベーシック ディスクへの再変換

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、ダイナミック ディスク上のすべてのデータを削除し、ベーシック ディスクに変換する方法について説明します。 ダイナミック ディスクは Windows では推奨されなくなりました。 ディスクをプールしてより大きいボリュームにする場合は、新しい[記憶域スペース](https://support.microsoft.com/help/12438/windows-10-storage-spaces) テクノロジを使用することをお勧めします。 Windows が起動するボリュームをミラー化する場合、多くのマザーボードに搭載されているような、ハードウェア RAID コントローラーを使用できます。

<br />

> [!WARNING]
> ダイナミック ディスクをベーシック ディスクに再変換するには、ディスクからすべてのボリュームを削除し、ディスク上のすべてのデータを完全に消去する必要があります。 操作を開始する前に、保存する必要のあるデータをすべてバックアップしてください。

## <a name="changing-a-dynamic-disk-back-to-a-basic-disk"></a>ダイナミック ディスクからベーシック ディスクに再変換する

-   [Windows インターフェイスを使用する](#BKMK_WINUI)
-   [コマンド ラインを使用する](#BKMK_CMD)

> [!NOTE]
> 以下の手順を実行するには、少なくとも **Backup Operators** または **Administrators** グループのメンバーである必要があります。

<a href="" id="BKMK_WINUI"></a>
#### <a name="to-change-a-dynamic-disk-back-to-a-basic-disk-using-the-windows-interface"></a>Windows インターフェイスを使用してダイナミック ディスクをベーシック ディスクに再変換するには
1.  ダイナミックからベーシックに変換するディスク上のすべてのボリュームをバックアップします。

2.  [ディスクの管理] で、ベーシック ディスクに変換するダイナミック ディスク上の各ボリュームを右クリックし、**[ボリュームの削除]** をクリックします。

3.  ディスク上のすべてのボリュームが削除されたら、ディスクを右クリックし、**[ベーシック ディスクに変換する]** をクリックします。


<a href="" id="BKMK_CMD"></a>
#### <a name="to-change-a-dynamic-disk-back-to-a-basic-disk-using-a-command-line"></a>コマンド ラインを使用してダイナミック ディスクをベーシック ディスクに再変換するには

1.  ダイナミックからベーシックに変換するディスク上のすべてのボリュームをバックアップします。

2.  コマンド プロンプトを開き、「`diskpart`」と入力します。

3.  **DISKPART** プロンプトで、「`list disk`」と入力します。 ベーシックに変換するディスクのディスク番号を書き留めておきます。

4.  **DISKPART** プロンプトで、「`select disk <disknumber>`」と入力します。

5.  **DISKPART** プロンプトで、「`detail disk <disknumber>`」と入力します。

6.  ディスク上の各ボリュームについて、**DISKPART** プロンプトで、「`select volume= <volumenumber>`」と入力し、次に「`delete volume`」と入力します。

7.  **DISKPART**プロンプトで、「`select disk <disknumber>`」と入力し、ベーシック ディスクに変換するディスクのディスク番号を指定します。

8.  **DISKPART** プロンプトで、「`convert basic`」と入力します。
 
<br /> <br />

| 値  | 説明 |
| --- |---|
| <p>**list disk**</p>                         | <p>ディスクとディスクに関する情報を一覧表示します。ディスクのサイズ、利用可能な空き領域の容量、ディスクがベーシック ディスクとダイナミック ディスクのどちらであるか、ディスクでマスター ブート レコード (MBR) と GUID パーティション テーブル (GPT) のどちらのパーティション スタイルが使用されているかなどの情報が表示されます。 アスタリスク (*) でマークされているディスクにフォーカスがあります。</p> |
| <p>**select disk** <em>disknumber</em></p>   | <p><em>disknumber</em> がディスク番号である指定されたディスクを選択し、そのディスクにフォーカスを移動します。</p>  |
| <p>**detail disk** <em>disknumber</em></p>   | <p>選択したディスクとそのディスク上のボリュームのプロパティを表示します。</p>  |
| <p>**select volume** <em>disknumber</em></p> | <p><em>disknumber</em> がボリューム番号である指定されたボリュームを選択し、そのボリュームにフォーカスを移動します。 ボリュームが指定されていない場合、**select** コマンドは、フォーカスがある現在のボリュームを一覧表示します。 番号、ドライブ文字、マウント ポイント パスでボリュームを指定できます。 ベーシック ディスクでボリュームを選択すると、対応するパーティションにフォーカスが移動します。</p> |
| <p>**delete volume**</p>                     | <p>選択したボリュームを削除します。 システム ボリューム、ブート ボリューム、または使用中のページング ファイルやクラッシュ ダンプ (メモリ ダンプ) を含むボリュームは削除できません。</p> |
| <p>**convert basic**</p> | <p>空のダイナミック ディスクをベーシック ディスクに変換します。</p>  |

## <a name="additional-considerations"></a>その他の考慮事項

-   ディスクをベーシック ディスクに再変換する前に、ディスク上のボリュームやデータをすべて削除しておく必要があります。 データを維持する場合は、ディスクをベーシック ディスクに変換する前に、データをバックアップするか、別のボリュームに移動します。
-   ダイナミック ディスクをベーシック ディスクに変更すると、そのディスクにはパーティションと論理ドライブのみを作成できます。

## <a name="see-also"></a>関連項目

-   [コマンド ライン構文の表記規則](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


