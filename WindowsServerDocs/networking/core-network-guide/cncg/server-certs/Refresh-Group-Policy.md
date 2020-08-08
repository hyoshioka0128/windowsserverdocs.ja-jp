---
title: グループ ポリシーを更新
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.author: lizross
author: eross-msft
ms.openlocfilehash: b0bc677d56e97f6b10d1ca12ece92067e210eab9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949396"
---
# <a name="refresh-group-policy"></a>グループ ポリシーを更新

>適用先:Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、ローカル コンピューターのグループ ポリシーを手動で更新します。 グループ ポリシーが更新される、証明書自動登録が構成されていて正しく機能している、ローカル コンピューターでは、証明機関 (CA) によって証明書自動登録された場合。

> [!NOTE]
> グループ ポリシーは、ドメイン メンバー コンピューターを再起動したときに、またはユーザーがドメイン メンバー コンピューターにログオンしたときに自動的に更新します。 さらに、グループ ポリシーは定期的に更新します。 既定では、この定期的な更新は最大 30 分のランダム オフセットでは 90 分ごとに実行します。

**Administrators**、またはそれと同等のメンバーシップが、この手順を実行するために最低限必要なメンバーシップです。

### <a name="to-refresh-group-policy-on-the-local-computer"></a>ローカル コンピューターのグループ ポリシーを更新するには

1.  NPS がインストールされているコンピューターで Windows PowerShell を開く&reg; タスク バーのアイコンを使用しています。

2.  Windows PowerShell プロンプトで「 **gpupdate**, 、ENTER キーを押します。



