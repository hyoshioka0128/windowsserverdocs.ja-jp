---
title: 'チェックリスト: ボリュームまたはフォルダーにファイル スクリーンを適用する'
description: この記事では、ボリュームまたはフォルダーにファイル スクリーンを適用する方法を説明します。
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f4c6953d27361ab2e3210a1574a5988e434f701f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861923"
---
# <a name="checklist---apply-a-file-screen-to-a-volume-or-folder"></a>チェックリスト: ボリュームまたはフォルダーにファイル スクリーンを適用する

> 適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

ボリュームまたはフォルダーにファイル スクリーンを適用するには、次の一覧の手順を実行します。
1. ファイル スクリーン処理の通知または記憶域レポートをメールで送信する場合は、「[電子メール通知を構成する](configure-email-notifications.md)」の手順に従って電子メール設定を構成します。

2. ファイル スクリーン処理の監査レポートを生成する場合は、監査データベースへのファイル スクリーン処理イベントの記録を有効にします。
[ファイル スクリーンの監査を構成します。](configure-file-screen-audit.md)

3. スクリーン処理規則の候補となる、保存されているファイルの種類を評価します。 データを指定するには、**[記憶域レポートの管理]** ノードのレポートを使用できます  (たとえば、実行ファイルをファイル グループのレポートまたは大きなファイルのレポートで大量のディスク領域を使用しているファイルを識別するためにオンデマンドで)。[オンデマンドでレポートを生成します。](generate-reports-on-demand.md) 

4. 構成済みのファイル グループを見直すか、新しいファイル グループを作成して、組織内で特定のスクリーン処理ポリシーを適用します。 [スクリーン処理のためのファイル グループを定義します。](define-file-groups-for-screening.md)  

5. 利用可能なファイル スクリーン テンプレートのプロパティを見直します  (で**ファイル スクリーニング管理**、クリックして、**ファイル スクリーン テンプレート**ノードです)。[ファイル スクリーン テンプレートのプロパティを編集します。](edit-file-screen-template-properties.md) 
<br />
 - または -
 <br /> 組織内で記憶域ポリシーを適用するための新しいファイル スクリーン テンプレートを作成します。  [ファイル スクリーン テンプレートを作成します。](create-file-screen-template.md) 

6. テンプレートを基に、ボリュームまたはフォルダーにファイル スクリーンを作成します。 
 [ファイル スクリーンを作成します。](create-file-screen.md)
 
7. ボリュームまたはフォルダーのサブフォルダーに、ファイル スクリーンの例外を構成します。 [ファイル スクリーンの例外を作成します。](create-file-screen-exception.md) 

8. ファイル スクリーン処理の監査レポートを含むレポート タスクをスケジュールし、スクリーン処理の動作状況を定期的に監視します。
  [一連のレポートのスケジュール設定します。](schedule-set-of-reports.md)


> [!NOTE]
> 記憶域ボリュームまたはフォルダーを制限するを参照してください。[チェックリスト。ボリュームまたはフォルダーにクォータを適用します。](checklist-apply-file-screen-to-volume-or-folder.md)