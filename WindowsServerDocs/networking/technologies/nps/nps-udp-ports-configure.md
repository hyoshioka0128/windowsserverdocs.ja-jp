---
title: NPS の UDP ポート情報を構成します。
description: このトピックを使用して、リモート認証ダイヤルイン ユーザー サービス (RADIUS) 認証、および Windows Server 2016 でのアカウンティング トラフィックのネットワーク ポリシー サーバー (NPS) を使用するポートを構成することができます。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 70569958-d7a7-474e-a817-6b7b5134784a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f0e703dc6f9083f1e79091a6cee6d1ac58753d12
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-nps-udp-port-information"></a>NPS の UDP ポート情報を構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用すると、リモート認証ダイヤルイン ユーザー サービス \(RADIUS\) 認証とアカウンティング トラフィックのネットワーク ポリシー サーバー (NPS) を使用するポートを構成します。

既定では、NPS は、RADIUS トラフィックをすべてインストールされているネットワーク アダプター用ポート 1812、1813、1645、および 1646 用インターネット プロトコル バージョン 6 \(IPv6\) と IPv4 の両方をリッスンします。

>[!NOTE]
>ネットワーク アダプターの IPv4 または IPv6 のいずれかをアンインストールすると、NPS では、インストールされていないプロトコルの RADIUS トラフィックは監視しません。

認証 1812、1813 アカウンティング用のポートの値は、Rfc 2865 と 2866 でインターネット技術標準化委員 \(IETF\) によって定義された RADIUS 標準ポートです。 ただし、既定では、多くのアクセス サーバーの認証要求 1645 と 1646 アカウンティング要求に使用します。 どのポート番号を使用する場合に関係なく同じものを使用して、アクセス サーバーの NPS が構成されていることを確認します。

>[重要]RADIUS 既定のポート番号を使用しない場合は、新しいポートで RADIUS トラフィックを許可するように、ローカル コンピューターのファイアウォールで例外を構成する必要があります。 詳細については、次を参照してください。[RADIUS トラフィック用のファイアウォールを構成する](nps-firewalls-configure.md)します。

メンバーシップ**Domain Admins**、相当するものでは、この手順を完了するために必要な最低限またはします。

## <a name="to-configure-nps-udp-port-information"></a>NPS の UDP ポート情報を構成するには 

1. NPS コンソールを開きます。
2. 右クリック**ネットワーク ポリシー サーバー**、] をクリックし、**プロパティ**します。
3. をクリックして、**ポート**タブをクリックし、ポートの設定を確認します。 使用するポート設定を RADIUS 認証と RADIUS アカウンティングの UDP ポートの既定値 (1812 と認証、1645 と 1813 およびアカウンティングの 1646) から変化する場合、入力**認証**と**アカウンティング**します。
4. 認証またはアカウンティング要求を複数のポート設定を使用するには、ポート番号をコンマで区切ります。

NPS の管理に関する詳細については、次を参照してください。[ネットワーク ポリシー サーバーの管理](nps-manage-top.md)します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。
