---
title: ボリュームまたはフォルダーにクォータを適用する
description: この記事では、ボリュームまたはフォルダーにストレージ クォータを適用する方法を説明します。
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e937464ca3af1292de5fd63303ba4a430f831dcd
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475861"
---
# <a name="checklist-apply-a-quota-to-a-volume-or-folder"></a>チェックリスト:ボリュームまたはフォルダーにクォータを適用します。

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server (半期チャネル)

1. しきい値の通知または記憶域レポートを電子メールで送信する場合は、電子メールの設定を構成します [電子メール通知を構成します。](configure-email-notifications.md)

2. ボリュームまたはフォルダーの記憶域の要件を評価します。 データを指定するには、 **[記憶域レポートの管理]** ノードのレポートを使用できます  (たとえば、実行、ファイル所有者レポートによって大量のディスク領域を使用するユーザーを識別するためにオンデマンドで)。[オン デマンドでレポートを生成する](generate-reports-on-demand.md)

3. 利用可能な構成済みのクォータのテンプレートを確認します  (で**クォータの管理**、クリックして、**クォータ テンプレート**ノードです)。[クォータ テンプレートのプロパティを編集します。](edit-quota-template-properties.md) 
<br />- または - <br /> 組織内で記憶域ポリシーを適用するための新しいクォータのテンプレートを作成します。 [クォータ テンプレートを作成します。](create-quota-template.md)

4. テンプレートを基に、ボリュームまたはフォルダーにクォータを作成します。  
 [クォータを作成する](create-quota.md) <br /> - または - <br /> 自動適用クォータを作成して、ボリュームまたはフォルダーのサブフォルダーに自動的にクォータを生成します。 [自動適用クォータを作成する](create-auto-apply-quota.md)

6. クォータの使用率を定期的に監視するため、クォータの使用率レポートを含むレポート タスクをスケジュールします。 [レポートのセットをスケジュールする](schedule-set-of-reports.md)

> [!Note]
> ボリュームまたはフォルダーのファイルをスクリーンする場合は、「[チェックリスト。ボリュームまたはフォルダーにファイル スクリーンを適用](checklist-apply-file-screen-to-volume-or-folder.md)します。











