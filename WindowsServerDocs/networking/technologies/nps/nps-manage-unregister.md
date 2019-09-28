---
title: Active Directory ドメインから NPS の登録を解除する
description: このトピックを使用して、Windows Server 2016 のネットワークポリシーサーバーを実行しているサーバーを NPS の既定のドメインまたは別のドメインに登録することができます。
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 68a94616-3c29-45bd-bd33-e4c578f119e1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3225c42ab14e2ea1bc283f520b14c09ebc2254c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396083"
---
# <a name="unregister-an-nps-from-an-active-directory-domain"></a>Active Directory ドメインから NPS の登録を解除する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

Nps の展開の管理プロセスでは、NPS を別のドメインに移動したり、NPS を置き換えたり、nps を削除したりすると便利な場合があります。 

NPS を移動または使用停止するときに、nps が Active Directory でユーザーアカウントのプロパティを読み取るアクセス許可を持っている Active Directory ドメインの NPS を登録解除できます。

これらの手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

## <a name="to-unregister-an-nps"></a>NPS の登録を解除するには

1. ドメインコントローラーの サーバーマネージャーで、 **[ツール]** をクリックし、 **[Active Directory ユーザーとコンピューター]** をクリックします。 Active Directory ユーザーとコンピューター コンソールが開きます。

2. **[ユーザー]** をクリックし、 **[RAS and IAS servers]** をダブルクリックします。

3. **[メンバー]** タブをクリックし、登録を解除する NPS を選択します。

4. **[削除]** をクリックし、 **[はい]** をクリックして、 **[OK]** をクリックします。

