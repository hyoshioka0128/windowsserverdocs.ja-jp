---
title: GUID パーティション テーブル (GPT) ディスクからマスター ブート レコード (MBR) ディスクへの変換
description: GUID パーティション テーブル (GPT) ディスクをマスター ブート レコード (MBR) パーティション スタイルのディスクに変換する方法について説明します。
ms.date: 06/19/2018
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5cd345230ce5c0fc556bfd8b421d866bd827507b
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "66812447"
---
# <a name="convert-a-gpt-disk-into-an-mbr-disk"></a>GPT ディスクを MBR ディスクに変換する

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

マスター ブート レコード (MBR) ディスクは、標準 BIOS パーティション テーブルを使用します。 GUID パーティション テーブル (GPT) ディスクは、Unified Extensible Firmware Interface (UEFI) を使用します。 MBR ディスクでは、各ディスク上で 4 つを超えるパーティションをサポートしていません。 2 テラバイト (TB) より大きいディスクでは、MBR パーティション方式はお勧めできません。

ディスクが空で、ボリュームが含まれていない限り、GPT から MBR パーティション スタイルにディスクを変更できます。

> [!NOTE]
> ディスクを変換する前に、ディスク上のすべてのデータをバックアップし、ディスクにアクセスするすべてのプログラムを閉じます。

> [!NOTE]
> 以下の手順を実行するには、少なくとも **Backup Operators** または **Administrators** グループのメンバーである必要があります。

## <a name="converting-using-the-windows-interface"></a>Windows インターフェイスを使用して変換する

1.  MBR ディスクに変換するベーシック GPT ディスク上のすべてのボリュームをバックアップまたは移動します。

2.  ディスクにパーティションまたはボリュームが含まれている場合、それぞれを右クリックし、 **[ボリュームの削除]** をクリックします。

3.  MBR ディスクに変換する GPT ディスクを右クリックし、 **[MBR ディスクに変換]** をクリックします。

## <a name="converting-using-a-command-line"></a>コマンド ラインを使用して変換する

1.  MBR ディスクに変換するベーシック GPT ディスク上のすべてのボリュームをバックアップまたは移動します。

2.  **[コマンド プロンプト]** を右クリックし、 **[管理者として実行]** を選択して、管理者特権でコマンド プロンプトを開きます。

3. 「`diskpart`」と入力します。 ディスクにパーティションやボリュームが含まれていない場合は、手順 6. に進みます。

4.  **DISKPART** プロンプトで、「`list disk`」と入力します。 削除するディスクのディスク番号を書き留めておきます。

5.  **DISKPART** プロンプトで、「`select disk <disknumber>`」と入力します。

6.  **DISKPART** プロンプトで、「`clean`」と入力します。

    > [!IMPORTANT]
    > **clean** コマンドを実行すると、ディスク上のすべてのパーティションやボリュームが削除されます。

7.  **DISKPART** プロンプトで、「`convert mbr`」と入力します。

|                Value                  |      説明   |
| ------------------------------------- | -----------------  |
|  <strong>list disk</strong>  | ディスクとディスクに関する情報を一覧表示します。ディスクのサイズ、利用可能な空き領域の容量、ディスクがベーシック ディスクとダイナミック ディスクのどちらであるか、ディスクでマスター ブート レコード (MBR) と GUID パーティション テーブル (GPT) のどちらのパーティション スタイルが使用されているかなどの情報が表示されます。 アスタリスク (\*) でマークされているディスクにフォーカスがあります。 |
| <strong>select disk</strong> |                                                                                                          <em>disknumber</em> がディスク番号である指定されたディスクを選択し、そのディスクにフォーカスを移動します。                                                                                                           |
| <strong>convert mbr</strong> |                                                                               GUID パーティション テーブル (GPT) パーティション スタイルの空のベーシック ディスクをマスター ブート レコード (MBR) パーティション スタイルのベーシック ディスクに変換します。                                                                                |

## <a name="see-also"></a>参照

-   [コマンド ライン構文の表記規則](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)