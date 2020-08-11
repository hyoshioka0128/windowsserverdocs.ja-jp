---
title: マスター ブート レコード (MBR) ディスクから GUID パーティション テーブル (GPT) ディスクへの変換
description: マスター ブート レコード (MBR) ディスクから GUID パーティション テーブル (GPT) ディスクに変換する方法について説明します。
ms.date: 06/07/2019
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 86934f2bf86ea8f91dfbe92f97952d76542a6bc4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935911"
---
# <a name="convert-an-mbr-disk-into-a-gpt-disk"></a>MBR ディスクを GPT ディスクに変換する

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

マスター ブート レコード (MBR) ディスクは、標準 BIOS パーティション テーブルを使用します。 GUID パーティション テーブル (GPT) ディスクは、Unified Extensible Firmware Interface (UEFI) を使用します。 GPT ディスクの 1 つの利点は、各ディスク上で 4 つを超えるパーティションを設定できることです。 GPT は、ディスクが 2 テラバイト (TB) より大きい場合にも必要になります。

ディスクにパーティションやボリュームが含まれていない限り、MBR から GPT パーティション スタイルにディスクを変更できます。

> [!NOTE]
> ディスクを変換する前に、ディスク上のすべてのデータをバックアップし、ディスクにアクセスするすべてのプログラムを閉じます。

> [!NOTE]
> 以下の手順を実行するには、少なくとも **Backup Operators** または **Administrators** グループのメンバーである必要があります。

## <a name="converting-using-the-windows-interface"></a>Windows インターフェイスを使用して変換する

1.  GPT ディスクに変換するベーシック MBR ディスク上のデータをバックアップまたは移動します。

2.  ディスクにパーティションまたはボリュームが含まれている場合、それぞれを右クリックし、 **[パーティションの削除]** または **[ボリュームの削除]** をクリックします。

3.  GPT ディスクに変換する MBR ディスクを右クリックし、 **[GPT ディスクに変換]** をクリックします。

## <a name="converting-using-a-command-line"></a>コマンド ラインを使用して変換する

次の手順を使用して、空の MBR ディスクを GPT ディスクに変換します。 MBR2GPT.EXE ツールを使用することもできますが、やや複雑です。詳細については、「[MBR パーティションを GPT に変換する](/windows/deployment/mbr-to-gpt)」を参照してください。

1.  GPT ディスクに変換するベーシック MBR ディスク上のデータをバックアップまたは移動します。

2.  **[コマンド プロンプト]** を右クリックし、 **[管理者として実行]** を選択して、管理者特権でコマンド プロンプトを開きます。

3. 「 `diskpart`」と入力し、 ディスクにパーティションやボリュームが含まれていない場合は、手順 6. に進みます。

4.  **DISKPART** プロンプトで、「`list disk`」と入力します。 変換するディスクのディスク番号を書き留めておきます。

5.  **DISKPART** プロンプトで、「`select disk <disknumber>`」と入力します。

6.  **DISKPART** プロンプトで、「`clean`」と入力します。

    > [!NOTE]
    > **clean** コマンドを実行すると、ディスク上のすべてのパーティションやボリュームが削除されます。

7.  **DISKPART** プロンプトで、「`convert gpt`」と入力します。

| 値  | 説明  |
| ----- | ---- |
| **list disk** | ディスクとディスクに関する情報を一覧表示します。ディスクのサイズ、利用可能な空き領域の容量、ディスクがベーシック ディスクとダイナミック ディスクのどちらであるか、ディスクでマスター ブート レコード (MBR) と GUID パーティション テーブル (GPT) のどちらのパーティション スタイルが使用されているかなどの情報が表示されます。 アスタリスク (*) でマークされているディスクにフォーカスがあります。 |
| **select disk** *disknumber* | *disknumber* がディスク番号である指定されたディスクを選択し、そのディスクにフォーカスを移動します。 |
| **clean** | フォーカスのあるディスクからすべてのパーティションまたはボリュームを削除します。  |
| **convert gpt**| マスター ブート レコード (MBR) パーティション スタイルの空のベーシック ディスクをGUID パーティション テーブル (GPT) パーティション スタイルのベーシック ディスクに変換します。 |

## <a name="see-also"></a>参照

-   [コマンド ライン構文の表記規則](/previous-versions/orphan-topics/ws.11/cc742449(v=ws.11))
