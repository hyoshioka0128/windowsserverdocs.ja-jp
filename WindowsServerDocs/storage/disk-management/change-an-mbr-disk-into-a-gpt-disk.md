---
title: "マスター ブート レコード (MBR) ディスクから GUID パーティション テーブル (GPT) ディスクへの変換"
description: "マスター ブート レコード (MBR) ディスクから GUID パーティション テーブル (GPT) ディスクに変換する方法について説明します。"
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f28d151d3b1d6b19b9ca330c5ff8576a53acbfa5
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="change-a-master-boot-record-mbr-disk-into-a-guid-partition-table-gpt-disk"></a>マスター ブート レコード (MBR) ディスクから GUID パーティション テーブル (GPT) ディスクへの変換

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

マスター ブート レコード (MBR) ディスクは、標準 BIOS パーティション テーブルを使用します。 GUID パーティション テーブル (GPT) ディスクは、Unified Extensible Firmware Interface (UEFI) を使用します。 GPT ディスクの 1 つの利点は、各ディスク上で 4 つを超えるパーティションを設定できることです。 GPT は、ディスクが 2 テラバイト (TB) より大きい場合にも必要になります。

ディスクにパーティションやボリュームが含まれていない限り、MBR から GPT パーティション スタイルにディスクを変更できます。
リムーバブル メディア、またはクラスター サービスによって使用される共有 SCSI またはファイバー チャネルのバスに接続されているクラスター ディスクで GPT パーティション スタイルを使用することはできません。

> [!NOTE]
> ディスクを変換する前に、ディスク上で実行されているプログラムをすべて閉じます。

## <a name="changing-an-mbr-disk-into-a-gpt-disk"></a>MBR ディスクを GPT ディスクに変換する

-   [Windows インターフェイスを使用する](#BKMK_WINUI)
-   [コマンド ラインを使用する](#BKMK_CMD)

> [!NOTE]
> 以下の手順を実行するには、少なくとも **Backup Operators** または **Administrators** グループのメンバーである必要があります。

<a id="BKMK_WINUI"></a>
#### <a name="to-change-an-mbr-disk-into-a-gpt-disk-using-the-windows-interface"></a>Windows インターフェイスを使用して MBR ディスクを GPT ディスクに変換するには

1.  GPT ディスクに変換するベーシック MBR ディスク上のデータをバックアップまたは移動します。

2.  ディスクにパーティションまたはボリュームが含まれている場合、それぞれを右クリックし、**[パーティションの削除]** または **[ボリュームの削除]** をクリックします。

3.  GPT ディスクに変換する MBR ディスクを右クリックし、**[GPT ディスクに変換]** をクリックします。

<a id="BKMK_CMD"></a>
#### <a name="to-change-an-mbr-disk-into-a-gpt-disk-using-a-command-line"></a>コマンド ラインを使用して MBR ディスクを GPT ディスクに変換するには

1.  GPT ディスクに変換するベーシック MBR ディスク上のデータをバックアップまたは移動します。

2.  **[コマンド プロンプト]** を右クリックし、**[管理者として実行]** を選択して、管理者特権でコマンド プロンプトを開きます。

3. 「`diskpart`」と入力します。 ディスクにパーティションやボリュームが含まれていない場合は、手順 6. に進みます。

4.  **DISKPART** プロンプトで、「`list disk`」と入力します。 変換するディスクのディスク番号を書き留めておきます。

5.  **DISKPART** プロンプトで、「`select disk <disknumber>`」と入力します。

6.  **DISKPART** プロンプトで、「`clean`」と入力します。

> [!NOTE]
> **clean** コマンドを実行すると、ディスク上のすべてのパーティションやボリュームが削除されます。

7.  **DISKPART** プロンプトで、「`convert gpt`」と入力します。

<br />

| 値  | 説明  |
| ----- | ----|
| <p>**list disk**</p> | <p>ディスクとディスクに関する情報を一覧表示します。ディスクのサイズ、利用可能な空き領域の容量、ディスクがベーシック ディスクとダイナミック ディスクのどちらであるか、ディスクでマスター ブート レコード (MBR) と GUID パーティション テーブル (GPT) のどちらのパーティション スタイルが使用されているかなどの情報が表示されます。 アスタリスク (*) でマークされているディスクにフォーカスがあります。</p> |
| <p>**select disk** <em>disknumber</em></p> | <p><em>disknumber</em> がディスク番号である指定されたディスクを選択し、そのディスクにフォーカスを移動します。</p> |
| <p>**clean**</p> | <p>フォーカスのあるディスクからすべてのパーティションまたはボリュームを削除します。</p>  |
| <p>**convert gpt**</p>| <p>マスター ブート レコード (MBR) パーティション スタイルの空のベーシック ディスクをGUID パーティション テーブル (GPT) パーティション スタイルのベーシック ディスクに変換します。</p> |

## <a name="see-also"></a>関連項目

-   [コマンド ライン構文の表記規則](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


