---
title: グループ ポリシーを更新
description: このトピックの「802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部である
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4d9f5d38199f8cf3c0ffe46df4cd975cd9c56ff6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="refresh-group-policy"></a>グループ ポリシーを更新

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、ローカル コンピューター上のグループ ポリシーを手動で更新します。 グループ ポリシーが更新される、証明書自動登録が構成されていて正しく機能して、ローカル コンピューターでは、証明機関 (CA) によって証明書を自動登録します。  
  
> [!NOTE]  
> ドメイン メンバーのコンピューターを再起動するときに、またはユーザーがドメイン メンバー コンピューターにログオンするときに、グループ ポリシーを自動的に更新します。 さらに、グループ ポリシーは定期的に更新します。 既定では、この定期的な更新は最大 30 分のランダム オフセットで 90 分ごとに実行します。  
  
メンバーシップ**管理者**、相当するものでは、この手順を完了するために必要な最低限またはします。  
  
### <a name="to-refresh-group-policy-on-the-local-computer"></a>ローカル コンピューターのグループ ポリシーを更新するには  
  
1.  NPS がインストールされているコンピューターで Windows PowerShell を開く&reg;タスクバーのアイコンを使用しています。  
  
2.  Windows PowerShell プロンプトで、次のように入力します。 **gpupdate**、し、Enter キーを押します。  
  


