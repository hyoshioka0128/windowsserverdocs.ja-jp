---
title: ボリュームまたはフォルダーにクォータを適用する
description: この記事では、ボリュームまたはフォルダーにストレージ クォータを適用する方法を説明します。
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 44eea3c3802e261239db9bf8350777e1b83fb9c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394332"
---
# <a name="checklist-apply-a-quota-to-a-volume-or-folder"></a>チェックリスト: ボリュームまたはフォルダーにクォータを適用する

> 適用対象: Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server (半期チャネル)

1. しきい値の通知または記憶域レポートを電子メールで送信する場合は、電子メールの設定を構成します [電子メール通知の構成](configure-email-notifications.md)

2. ボリュームまたはフォルダーの記憶域の要件を評価します。 データを指定するには、 **[記憶域レポートの管理]** ノードのレポートを使用できます (たとえば、所有者ごとのファイルのレポートをオン デマンドで実行して、大量のディスク領域を使用しているユーザーを特定します)。[オン デマンドでレポートを生成する](generate-reports-on-demand.md)

3. 利用可能な構成済みのクォータのテンプレートを確認します ( **[クォータの管理]** で、 **[クォータテンプレート]** ノードをクリックします)。[クォータテンプレートのプロパティの編集](edit-quota-template-properties.md) 
<br />\- または - <br /> 組織内で記憶域ポリシーを適用するための新しいクォータのテンプレートを作成します。 [クォータテンプレートを作成する](create-quota-template.md)

4. テンプレートを基に、ボリュームまたはフォルダーにクォータを作成します。  
 [クォータを作成する](create-quota.md) <br /> \- または - <br /> 自動適用クォータを作成して、ボリュームまたはフォルダーのサブフォルダーに自動的にクォータを生成します。 [自動適用クォータを作成する](create-auto-apply-quota.md)

6. クォータの使用率を定期的に監視するため、クォータの使用率レポートを含むレポート タスクをスケジュールします。 [レポートのセットをスケジュールする](schedule-set-of-reports.md)

> [!Note]
> ボリュームまたはフォルダーのファイルをスクリーン処理する場合は、「[チェックリスト: ボリュームまたはフォルダーにファイル スクリーンを適用する](checklist-apply-file-screen-to-volume-or-folder.md)」をご覧ください。











