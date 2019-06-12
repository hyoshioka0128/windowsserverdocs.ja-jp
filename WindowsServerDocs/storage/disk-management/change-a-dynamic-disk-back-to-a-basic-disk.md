---
title: ダイナミック ディスクからベーシック ディスクへの再変換
description: ダイナミック ディスクをベーシック ディスクに再変換する方法について説明します。
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 249db6d2779e696ef93fecfd11718dbcce8654be
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812468"
---
# <a name="change-a-dynamic-disk-back-to-a-basic-disk"></a>ダイナミック ディスクからベーシック ディスクへの再変換

> **適用対象します。** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、ダイナミック ディスク上のすべてのデータを削除し、ベーシック ディスクに変換する方法について説明します。 Windows からダイナミック ディスクが非推奨とされましたし、使用してもうお勧めしません。、 ベーシック ディスクを使用するか、新しい使用勧め代わりに、[記憶域スペース](https://support.microsoft.com/help/12438/windows-10-storage-spaces)する場合にプールのディスク一緒に大量のテクノロジです。 Windows が起動するボリュームをミラー化する場合、多くのマザーボードに搭載されているような、ハードウェア RAID コントローラーを使用できます。

> [!WARNING]
> ダイナミック ディスクをベーシック ディスクに再変換するには、ディスクからすべてのボリュームを削除し、ディスク上のすべてのデータを完全に消去する必要があります。 操作を開始する前に、保存する必要のあるデータをすべてバックアップしてください。

## <a name="changing-a-dynamic-disk-back-to-a-basic-disk"></a>ダイナミック ディスクからベーシック ディスクに再変換する

-   [Windows インターフェイスを使用します。](#to-change-a-dynamic-disk-back-to-a-basic-disk-using-the-windows-interface)
-   [コマンドラインを使用](#to-change-a-dynamic-disk-back-to-a-basic-disk-using-a-command-line)

> [!NOTE]
> 以下の手順を実行するには、少なくとも **Backup Operators** または **Administrators** グループのメンバーである必要があります。

#### <a name="to-change-a-dynamic-disk-back-to-a-basic-disk-using-the-windows-interface"></a>Windows インターフェイスを使用してダイナミック ディスクをベーシック ディスクに再変換するには

1.  ダイナミックからベーシックに変換するディスク上のすべてのボリュームをバックアップします。

2.  [ディスクの管理] で、ベーシック ディスクに変換するダイナミック ディスク上の各ボリュームを右クリックし、 **[ボリュームの削除]** をクリックします。

3.  ディスク上のすべてのボリュームが削除されたら、ディスクを右クリックし、 **[ベーシック ディスクに変換する]** をクリックします。

#### <a name="to-change-a-dynamic-disk-back-to-a-basic-disk-using-a-command-line"></a>コマンド ラインを使用してダイナミック ディスクをベーシック ディスクに再変換するには

1.  ダイナミックからベーシックに変換するディスク上のすべてのボリュームをバックアップします。

2.  コマンド プロンプトを開き、「`diskpart`」と入力します。

3.  **DISKPART** プロンプトで、「`list disk`」と入力します。 ベーシックに変換するディスクのディスク番号を書き留めておきます。

4.  **DISKPART** プロンプトで、「`select disk <disknumber>`」と入力します。

5.  **DISKPART** プロンプトで、「`detail disk <disknumber>`」と入力します。

6.  ディスク上の各ボリュームについて、**DISKPART** プロンプトで、「`select volume= <volumenumber>`」と入力し、次に「`delete volume`」と入力します。

7.  **DISKPART**プロンプトで、「`select disk <disknumber>`」と入力し、ベーシック ディスクに変換するディスクのディスク番号を指定します。

8.  **DISKPART** プロンプトで、「`convert basic`」と入力します。


| Value  | 説明 |
| --- | --- |
| **ディスクの一覧**                         | ディスクとディスクに関する情報を一覧表示します。ディスクのサイズ、利用可能な空き領域の容量、ディスクがベーシック ディスクとダイナミック ディスクのどちらであるか、ディスクでマスター ブート レコード (MBR) と GUID パーティション テーブル (GPT) のどちらのパーティション スタイルが使用されているかなどの情報が表示されます。 アスタリスク (*) でマークされているディスクにフォーカスがあります。 |
| **ディスクを選択して** <em>disknumber</em>   | <em>disknumber</em> がディスク番号である指定されたディスクを選択し、そのディスクにフォーカスを移動します。  |
| **詳細ディスク** <em>disknumber</em>   | 選択したディスクとそのディスク上のボリュームのプロパティを表示します。  |
| **ボリュームを選択** <em>disknumber</em> | <em>disknumber</em> がボリューム番号である指定されたボリュームを選択し、そのボリュームにフォーカスを移動します。 ボリュームが指定されていない場合、**select** コマンドは、フォーカスがある現在のボリュームを一覧表示します。 番号、ドライブ文字、マウント ポイント パスでボリュームを指定できます。 ベーシック ディスクでボリュームを選択すると、対応するパーティションにフォーカスが移動します。 |
| **ボリュームを削除します。**                     | 選択したボリュームを削除します。 システム ボリューム、ブート ボリューム、または使用中のページング ファイルやクラッシュ ダンプ (メモリ ダンプ) を含むボリュームは削除できません。 |
| **基本的な変換します。** | 空のダイナミック ディスクをベーシック ディスクに変換します。  |

## <a name="additional-considerations"></a>その他の考慮事項

-   ディスクをベーシック ディスクに再変換する前に、ディスク上のボリュームやデータをすべて削除しておく必要があります。 データを維持する場合は、ディスクをベーシック ディスクに変換する前に、データをバックアップするか、別のボリュームに移動します。
-   ダイナミック ディスクをベーシック ディスクに変更すると、そのディスクにはパーティションと論理ドライブのみを作成できます。

## <a name="see-also"></a>関連項目

-   [コマンドライン構文の表記規則](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)