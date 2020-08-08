---
title: 記憶域レポートを構成する
description: この記事では、記憶域レポートの既定のパラメーターを構成する方法を説明します。
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8b9d6a53b5f34c0c053de860895f5c4e48b07c83
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961496"
---
# <a name="configure-storage-reports"></a>記憶域レポートを構成する

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

記憶域レポートの既定のパラメーターを構成することができます。 これらの既定のパラメーターは、クォータまたはファイル スクリーン処理イベント発生時に生成されるインシデント レポートに使用されます。 また、スケジュールされたレポートやオン デマンドのレポートにも使用され、これらのレポートの特定のプロパティを定義する際に既定のパラメーターを上書きできます。

> [!Important]
> 1 種類のレポートについて既定のパラメーターを変更すると、その既定の設定を使用するすべてのインシデント レポートおよび既存のスケジュールされたレポート タスクに変更が反映されます。

## <a name="to-configure-the-default-parameters-for-storage-reports"></a>記憶域レポートの既定のパラメーターを構成するには

1. コンソール ツリーで、**[ファイル サーバー リソース マネージャー]** を右クリックし、**[オプションの構成]** をクリックします。 [**ファイル サーバー リソース マネージャーのオプション**] ダイアログ ボックスが開きます。

2. **[記憶域レポート]** タブの **[既定のパラメーターを構成する]** で、変更するレポートの種類を選択します。

3. [**パラメーターの編集**] をクリックします。

4. 選択したレポートの種類に応じて、異なるレポート パラメーターが編集できるようになります。 必要なすべての変更を行ったら、**[OK]** をクリックし、そのレポートの種類の既定のパラメーターとしてそれらを保存します。

5.  編集対象の各レポートの種類に対し、手順 2 ～ 4 を繰り返します。

6. すべてのレポートについて、既定のパラメーターの一覧を表示するには、**[レポートの表示]** をクリックします。 次に、**[閉じる]** をクリックします。

7.  **[OK]** をクリックします。

## <a name="additional-references"></a>その他の参照情報

-   [ファイル サーバー リソース マネージャーのオプションを設定する](setting-file-server-resource-manager-options.md)
-   [記憶域レポートの管理](storage-reports-management.md)