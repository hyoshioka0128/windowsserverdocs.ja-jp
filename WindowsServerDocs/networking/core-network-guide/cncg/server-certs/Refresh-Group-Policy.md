---
title: グループ ポリシーを更新する
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 88d39f41f61ae7c7f6a1fb84aa99806c4796c8cf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356189"
---
# <a name="refresh-group-policy"></a>グループ ポリシーを更新する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、ローカル コンピューターのグループ ポリシーを手動で更新します。 グループ ポリシーが更新される、証明書自動登録が構成されていて正しく機能している、ローカル コンピューターでは、証明機関 (CA) によって証明書自動登録された場合。  
  
> [!NOTE]  
> グループ ポリシーは、ドメイン メンバー コンピューターを再起動したときに、またはユーザーがドメイン メンバー コンピューターにログオンしたときに自動的に更新します。 さらに、グループ ポリシーは定期的に更新します。 既定では、この定期的な更新は最大 30 分のランダム オフセットでは 90 分ごとに実行します。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  
  
### <a name="to-refresh-group-policy-on-the-local-computer"></a>ローカル コンピューターのグループ ポリシーを更新するには  
  
1.  NPS がインストールされているコンピューターで Windows PowerShell を開く&reg; タスク バーのアイコンを使用しています。  
  
2.  Windows PowerShell プロンプトで「 **gpupdate**, 、ENTER キーを押します。  
  


