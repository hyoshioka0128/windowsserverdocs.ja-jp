---
title: グループ ポリシーを更新する
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 83dd48297535aafe30e48fe37010d81b279f4c91
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863453"
---
# <a name="refresh-group-policy"></a>グループ ポリシーを更新する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

この手順を使用すると、ローカル コンピューターのグループ ポリシーを手動で更新します。 グループ ポリシーが更新される、証明書自動登録が構成されていて正しく機能している、ローカル コンピューターでは、証明機関 (CA) によって証明書自動登録された場合。  
  
> [!NOTE]  
> グループ ポリシーは、ドメイン メンバー コンピューターを再起動したときに、またはユーザーがドメイン メンバー コンピューターにログオンしたときに自動的に更新します。 さらに、グループ ポリシーは定期的に更新します。 既定では、この定期的な更新は最大 30 分のランダム オフセットでは 90 分ごとに実行します。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  
  
### <a name="to-refresh-group-policy-on-the-local-computer"></a>ローカル コンピューターのグループ ポリシーを更新するには  
  
1.  NPS がインストールされているコンピューターで Windows PowerShell を開く&reg; タスク バーのアイコンを使用しています。  
  
2.  Windows PowerShell プロンプトで「 **gpupdate**, 、ENTER キーを押します。  
  


