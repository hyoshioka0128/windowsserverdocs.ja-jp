---
title: 'チェックリスト: ボリュームまたはフォルダーにファイル スクリーンを適用する'
description: この記事では、ボリュームまたはフォルダーにファイル スクリーンを適用する方法を説明します。
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 4d38e9a92a9c99663d81aab2a0164c5a30002f6a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401993"
---
# <a name="checklist---apply-a-file-screen-to-a-volume-or-folder"></a>チェックリスト: ボリュームまたはフォルダーにファイル スクリーンを適用する

> 適用対象: Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)、windows server 2012 R2、windows Server 2012、Windows Server 2008 R2

ボリュームまたはフォルダーにファイル スクリーンを適用するには、次の一覧の手順を実行します。
1. ファイル スクリーン処理の通知または記憶域レポートをメールで送信する場合は、「[電子メール通知を構成する](configure-email-notifications.md)」の手順に従って電子メール設定を構成します。

2. ファイル スクリーン処理の監査レポートを生成する場合は、監査データベースへのファイル スクリーン処理イベントの記録を有効にします。
[ファイル スクリーンの監査を構成する](configure-file-screen-audit.md)

3. スクリーン処理規則の候補となる、保存されているファイルの種類を評価します。 データを指定するには、 **[記憶域レポートの管理]** ノードのレポートを使用できます (たとえば、ファイル グループごとのファイル レポートや大きいサイズのファイルのレポートをオン デマンドで実行して、大量のディスク領域を使用しているファイルを特定します)。[オンデマンドでレポートを生成する](generate-reports-on-demand.md) 

4. 構成済みのファイル グループを見直すか、新しいファイル グループを作成して、組織内で特定のスクリーン処理ポリシーを適用します。 [スクリーン処理のためにファイル グループを定義する](define-file-groups-for-screening.md)  

5. 利用可能なファイル スクリーン テンプレートのプロパティを見直します ( **[ファイル]** スクリーンの管理 で、 **[ファイルスクリーンテンプレート]** ノードをクリックします)。[ファイルスクリーンテンプレートのプロパティの編集](edit-file-screen-template-properties.md) 
<br />
 \- または -
 <br /> 組織内で記憶域ポリシーを適用するための新しいファイル スクリーン テンプレートを作成します。  [ファイル スクリーン テンプレートを作成する](create-file-screen-template.md) 

6. テンプレートを基に、ボリュームまたはフォルダーにファイル スクリーンを作成します。 
 [ファイル スクリーンを作成する](create-file-screen.md)
 
7. ボリュームまたはフォルダーのサブフォルダーに、ファイル スクリーンの例外を構成します。 [ファイル スクリーンの例外を作成する](create-file-screen-exception.md) 

8. ファイル スクリーン処理の監査レポートを含むレポート タスクをスケジュールし、スクリーン処理の動作状況を定期的に監視します。
  [レポートのセットをスケジュールする](schedule-set-of-reports.md)


> [!NOTE]
> ボリュームまたはフォルダーの記憶域を制限する場合は、「[チェックリスト: ボリュームまたはフォルダーにクォータを適用する](checklist-apply-file-screen-to-volume-or-folder.md)」をご覧ください。