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
ms.openlocfilehash: 62910af666fb16db5c2e7a30b49eedfa8c12cacb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860853"
---
# <a name="checklist-apply-a-quota-to-a-volume-or-folder"></a>チェックリスト:ボリュームまたはフォルダーにクォータを適用します。

> 適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

1. しきい値の通知または記憶域レポートを電子メールで送信する場合は、電子メールの設定を構成します [電子メール通知を構成します。](configure-email-notifications.md)

2. ボリュームまたはフォルダーの記憶域の要件を評価します。 データを指定するには、**[記憶域レポートの管理]** ノードのレポートを使用できます  (たとえば、実行、ファイル所有者レポートによって大量のディスク領域を使用するユーザーを識別するためにオンデマンドで)。[オンデマンドでレポートを生成します。](generate-reports-on-demand.md)

3. 利用可能な構成済みのクォータのテンプレートを確認します  (で**クォータの管理**、クリックして、**クォータ テンプレート**ノードです)。[クォータ テンプレートのプロパティを編集します。](edit-quota-template-properties.md) 
<br />- または - <br /> 組織内で記憶域ポリシーを適用するための新しいクォータのテンプレートを作成します。 [クォータ テンプレートを作成します。](create-quota-template.md)

4. テンプレートを基に、ボリュームまたはフォルダーにクォータを作成します。  
 [クォータを作成します。](create-quota.md) <br /> - または - <br /> 自動適用クォータを作成して、ボリュームまたはフォルダーのサブフォルダーに自動的にクォータを生成します。 [作成、自動適用クォータ](create-auto-apply-quota.md)

6. クォータの使用率を定期的に監視するため、クォータの使用率レポートを含むレポート タスクをスケジュールします。 [一連のレポートのスケジュール設定します。](schedule-set-of-reports.md)

> [!Note]
> ボリュームまたはフォルダーのファイルをスクリーンする場合は、「[チェックリスト。ボリュームまたはフォルダーにファイル スクリーンを適用](checklist-apply-file-screen-to-volume-or-folder.md)します。











