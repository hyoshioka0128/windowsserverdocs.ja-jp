---
title: マスター ブート レコード (MBR) ディスクから GUID パーティション テーブル (GPT) ディスクへの変換
description: マスター ブート レコード (MBR) ディスクから GUID パーティション テーブル (GPT) ディスクに変換する方法について説明します。
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 902a845bbe6a7e2a4d811aac0ea2990fb3557832
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812455"
---
# <a name="convert-an-mbr-disk-into-a-gpt-disk"></a>MBR ディスクを GPT ディスクに変換します。

> **適用対象します。** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

マスター ブート レコード (MBR) ディスクは、標準 BIOS パーティション テーブルを使用します。 GUID パーティション テーブル (GPT) ディスクは、Unified Extensible Firmware Interface (UEFI) を使用します。 GPT ディスクの 1 つの利点は、各ディスク上で 4 つを超えるパーティションを設定できることです。 GPT は、ディスクが 2 テラバイト (TB) より大きい場合にも必要になります。

ディスクにパーティションやボリュームが含まれていない限り、MBR から GPT パーティション スタイルにディスクを変更できます。

> [!NOTE]
> ディスクを変換する前に、上の任意のデータをバックアップし、ディスクにアクセスするすべてのプログラムを閉じます。

> [!NOTE]
> 以下の手順を実行するには、少なくとも **Backup Operators** または **Administrators** グループのメンバーである必要があります。

## <a name="converting-using-the-windows-interface"></a>Windows インターフェイスを使用して変換します。

1.  GPT ディスクに変換するベーシック MBR ディスク上のデータをバックアップまたは移動します。

2.  ディスクにパーティションまたはボリュームが含まれている場合、それぞれを右クリックし、 **[パーティションの削除]** または **[ボリュームの削除]** をクリックします。

3.  GPT ディスクに変換する MBR ディスクを右クリックし、 **[GPT ディスクに変換]** をクリックします。

## <a name="converting-using-a-command-line"></a>コマンドラインを使用して変換します。

次の手順を使用して、空の MBR ディスクを GPT ディスクに変換します。 また、MBR2GPT があります。EXE のツールを使用することができますが、ちょっと複雑ですを参照してください[GPT に変換する MBR パーティション](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)の詳細。

1.  GPT ディスクに変換するベーシック MBR ディスク上のデータをバックアップまたは移動します。

2.  **[コマンド プロンプト]** を右クリックし、 **[管理者として実行]** を選択して、管理者特権でコマンド プロンプトを開きます。

3. 「`diskpart`. ディスクにパーティションやボリュームが含まれていない場合は、手順 6. に進みます。

4.  **DISKPART** プロンプトで、「`list disk`」と入力します。 変換するディスクのディスク番号を書き留めておきます。

5.  **DISKPART** プロンプトで、「`select disk <disknumber>`」と入力します。

6.  **DISKPART** プロンプトで、「`clean`」と入力します。

    > [!NOTE]
    > **clean** コマンドを実行すると、ディスク上のすべてのパーティションやボリュームが削除されます。

7.  **DISKPART** プロンプトで、「`convert gpt`」と入力します。

| Value  | 説明  |
| ----- | ---- |
| **ディスクの一覧** | ディスクとディスクに関する情報を一覧表示します。ディスクのサイズ、利用可能な空き領域の容量、ディスクがベーシック ディスクとダイナミック ディスクのどちらであるか、ディスクでマスター ブート レコード (MBR) と GUID パーティション テーブル (GPT) のどちらのパーティション スタイルが使用されているかなどの情報が表示されます。 アスタリスク (*) でマークされているディスクにフォーカスがあります。 |
| **ディスクを選択して** *disknumber* | *disknumber* がディスク番号である指定されたディスクを選択し、そのディスクにフォーカスを移動します。 |
| **クリーンアップ** | フォーカスのあるディスクからすべてのパーティションまたはボリュームを削除します。  |
| **Gpt に変換します。**| マスター ブート レコード (MBR) パーティション スタイルの空のベーシック ディスクをGUID パーティション テーブル (GPT) パーティション スタイルのベーシック ディスクに変換します。 |

## <a name="see-also"></a>関連項目

-   [コマンドライン構文の表記規則](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)