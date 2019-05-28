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
ms.openlocfilehash: 03325d8a65d88c35f09985223608fc7474a0fde5
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475848"
---
# <a name="checklist---apply-a-file-screen-to-a-volume-or-folder"></a>チェックリスト: ボリュームまたはフォルダーにファイル スクリーンを適用する

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

ボリュームまたはフォルダーにファイル スクリーンを適用するには、次の一覧の手順を実行します。
1. ファイル スクリーン処理の通知または記憶域レポートをメールで送信する場合は、「[電子メール通知を構成する](configure-email-notifications.md)」の手順に従って電子メール設定を構成します。

2. ファイル スクリーン処理の監査レポートを生成する場合は、監査データベースへのファイル スクリーン処理イベントの記録を有効にします。
[ファイル スクリーンの監査を構成する](configure-file-screen-audit.md)

3. スクリーン処理規則の候補となる、保存されているファイルの種類を評価します。 データを指定するには、 **[記憶域レポートの管理]** ノードのレポートを使用できます  (たとえば、実行ファイルをファイル グループのレポートまたは大きなファイルのレポートで大量のディスク領域を使用しているファイルを識別するためにオンデマンドで)。[オン デマンドでレポートを生成する](generate-reports-on-demand.md) 

4. 構成済みのファイル グループを見直すか、新しいファイル グループを作成して、組織内で特定のスクリーン処理ポリシーを適用します。 [スクリーン処理のためにファイル グループを定義する](define-file-groups-for-screening.md)  

5. 利用可能なファイル スクリーン テンプレートのプロパティを見直します  (で**ファイル スクリーニング管理**、クリックして、**ファイル スクリーン テンプレート**ノードです)。[ファイル スクリーン テンプレートのプロパティを編集します。](edit-file-screen-template-properties.md) 
<br />
 - または -
 <br /> 組織内で記憶域ポリシーを適用するための新しいファイル スクリーン テンプレートを作成します。  [ファイル スクリーン テンプレートを作成する](create-file-screen-template.md) 

6. テンプレートを基に、ボリュームまたはフォルダーにファイル スクリーンを作成します。 
 [ファイル スクリーンを作成します。](create-file-screen.md)
 
7. ボリュームまたはフォルダーのサブフォルダーに、ファイル スクリーンの例外を構成します。 [ファイル スクリーンの例外を作成する](create-file-screen-exception.md) 

8. ファイル スクリーン処理の監査レポートを含むレポート タスクをスケジュールし、スクリーン処理の動作状況を定期的に監視します。
  [レポートのセットをスケジュールする](schedule-set-of-reports.md)


> [!NOTE]
> 記憶域ボリュームまたはフォルダーを制限するを参照してください。[チェックリスト。ボリュームまたはフォルダーにクォータを適用する](checklist-apply-file-screen-to-volume-or-folder.md)