---
title: "GUID パーティション テーブル (GPT) ディスクからマスター ブート レコード (MBR) ディスクへの変換"
description: "GUID パーティション テーブル (GPT) ディスクをマスター ブート レコード (MBR) パーティション スタイルのディスクに変換する方法について説明します。"
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8efe6617c46267f7e165550de82b18421ab563ca
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="change-a-guid-partition-table-gpt-disk-into-a-master-boot-record-mbr-disk"></a>GUID パーティション テーブル (GPT) ディスクからマスター ブート レコード (MBR) ディスクへの変換

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

マスター ブート レコード (MBR) ディスクは、標準 BIOS パーティション テーブルを使用します。 GUID パーティション テーブル (GPT) ディスクは、Unified Extensible Firmware Interface (UEFI) を使用します。 MBR ディスクでは、各ディスク上で 4 つを超えるパーティションをサポートしていません。 2 テラバイト (TB) より大きいディスクでは、MBR パーティション方式はお勧めできません。

ディスクが空で、ボリュームが含まれていない限り、GPT から MBR パーティション スタイルにディスクを変更できます。

> [!NOTE]
> ディスクを変換する前に、ディスク上で実行されているプログラムをすべて閉じます。

<a name="changing-a-gpt-disk-into-an-mbr-disk"></a>GPT ディスクを MBR ディスクに変換する
-------------------------------------------------------

-   [Windows インターフェイスを使用する](#BKMK_WINUI)
-   [コマンド ラインを使用する](#BKMK_CMD)

> [!NOTE]
> 以下の手順を実行するには、少なくとも **Backup Operators** または **Administrators** グループのメンバーである必要があります。

 <a id="BKMK_WINUI"></a>
#### <a name="to-change-a-gpt-disk-into-an-mbr-disk-using-the-windows-interface"></a>Windows インターフェイスを使用して GPT ディスクを MBR ディスクに変換するには

1.  MBR ディスクに変換するベーシック GPT ディスク上のすべてのボリュームをバックアップまたは移動します。

2.  ディスクにパーティションまたはボリュームが含まれている場合、それぞれを右クリックし、**[ボリュームの削除]** をクリックします。

3.  MBR ディスクに変換する GPT ディスクを右クリックし、**[MBR ディスクに変換]** をクリックします。

 <a id="BKMK_CMD"></a>
#### <a name="to-change-a-gpt-disk-into-an-mbr-disk-using-a-command-line"></a>コマンド ラインを使用して GPT ディスクを MBR ディスクに変換するには

1.  MBR ディスクに変換するベーシック GPT ディスク上のすべてのボリュームをバックアップまたは移動します。

2.  **[コマンド プロンプト]** を右クリックし、**[管理者として実行]** を選択して、管理者特権でコマンド プロンプトを開きます。

3. 「`diskpart`」と入力します。 ディスクにパーティションやボリュームが含まれていない場合は、手順 6. に進みます。

4.  **DISKPART** プロンプトで、「`list disk`」と入力します。 削除するディスクのディスク番号を書き留めておきます。

5.  **DISKPART** プロンプトで、「`select disk <disknumber>`」と入力します。

6.  **DISKPART** プロンプトで、「`clean`」と入力します。

> [!IMPORTANT]
> **clean** コマンドを実行すると、ディスク上のすべてのパーティションやボリュームが削除されます。

7.  **DISKPART** プロンプトで、「`convert mbr`」と入力します。

<br />

| 値 | 説明 |
| --- | --- |
| <p>**list disk**</p> | <p>ディスクとディスクに関する情報を一覧表示します。ディスクのサイズ、利用可能な空き領域の容量、ディスクがベーシック ディスクとダイナミック ディスクのどちらであるか、ディスクでマスター ブート レコード (MBR) と GUID パーティション テーブル (GPT) のどちらのパーティション スタイルが使用されているかなどの情報が表示されます。 アスタリスク (*) でマークされているディスクにフォーカスがあります。</p> |
| <p>**select disk**</p> | <p><em>disknumber</em> がディスク番号である指定されたディスクを選択し、そのディスクにフォーカスを移動します。</p> | <p>**clean**</p> | <p>フォーカスのあるディスクからすべてのパーティションまたはボリュームを削除します。</p> |
| <p>**convert mbr**</p> | <p>GUID パーティション テーブル (GPT) パーティション スタイルの空のベーシック ディスクをマスター ブート レコード (MBR) パーティション スタイルのベーシック ディスクに変換します。</p>

## <a name="see-also"></a>関連項目

-   [コマンド ライン構文の表記規則](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


