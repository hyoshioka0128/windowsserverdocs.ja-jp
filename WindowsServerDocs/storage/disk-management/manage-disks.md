---
title: "ディスクを管理する"
description: "この記事では、ディスクを管理する方法について説明します。"
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ae96071733b961fbe65551120894c21c633db83e
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="manage-disks"></a>ディスクを管理する

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックと各サブトピックでは、ディスクの管理を使用してコンピューターのディスクを管理する方法について説明します。異なるパーティション スタイル間でディスクを変換する方法や、Windows で新しいディスクのオンライン状態を処理する方法についても説明します。

## <a name="converting-disk-types"></a>ディスクの種類を変換する

ディスクの管理を使用して、さまざまな種類およびパーティション スタイルの間でディスクを変換できますが、一部の操作は元に戻すことができません (ドライブを再フォーマットする場合を除く)。 アプリケーションに最も適したディスクの種類とパーティション スタイルを慎重に検討する必要があります。

次の表に、さまざまなパーティション スタイル間でディスクを変換するためのオプションを示します。

| ディスクの種類 | MBR への変換  | GPT への変換| ダイナミックへの変換 |
| ---- | --- | --- |--- |
| <p>マスター ブート レコード (MBR)</p> | <p>--</p> | <p>可能 (ディスク上にボリュームがない場合)。</p> | <p>可能だが、ディスクがブート不可能になる可能性がある。 注を参照。</p> |
| <p>GUID パーティション テーブル (GPT)</p> | <p>可能 (ディスク上にボリュームがない場合)。</p> | <p>--</p>  | <p>可能だが、ディスクがブート不可能になる可能性がある。 注を参照。</p> |


> [!NOTE]
> マルチブートのシナリオで、1 つのオペレーティング システムを起動し、別のオペレーティング システムを含むベーシック MBR ディスクをダイナミック ディスクに変換すると、別のオペレーティング システムを起動することはできなくなります。

## <a name="online-and-offline-status"></a>オンラインとオフラインの状態

ディスクの管理には、ディスクのオンラインとオフラインの状態が表示されます。 

Windows の既定では、新しく検出されたすべてのディスクがオンラインになり、読み取り/書き込みアクセスが設定されます。 Windows Server の既定では、新しく検出されたディスクがオンラインになり、読み取り/書き込みアクセスが設定されます。ただし、共有バス (SCSI、iSCSI、Serial Attached SCSI、ファイバー チャネルなど) 上にある場合を除きます。 共有バス上のディスクは、初めて検出されたときにオフラインになります

ディスクがオフラインの場合、ディスクを初期化したり、ディスク上にボリュームを作成したりするには、ディスクをオンラインにする必要があります。 

-  ディスクをオンラインまたはオフラインにするには、ディスク名を右クリックし、適切な操作を選択します。

## <a name="see-also"></a>関連項目

-   [新しいディスクの初期化](initialize-new-disks.md)
-   [ディスクを別のコンピューターに移動する](move-disks-to-another-computer.md)
-   [ダイナミック ディスクからベーシック ディスクへの再変換](change-a-dynamic-disk-back-to-a-basic-disk.md)
-   [マスター ブート レコード ディスクから GUID パーティション テーブル ディスクへの変換](change-an-mbr-disk-into-a-gpt-disk.md)
-   [GUID パーティション テーブル ディスクからマスター ブート レコード ディスクへの変換](change-a-gpt-disk-into-an-mbr-disk.md)
-   [仮想ハード ディスクの管理](manage-virtual-hard-disks.md)