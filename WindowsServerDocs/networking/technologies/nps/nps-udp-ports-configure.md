---
title: NPS の UDP ポート情報を構成する
description: このトピックを使用して、Windows Server 2016 のリモート認証ダイヤルインユーザーサービス (RADIUS) 認証およびアカウンティングトラフィックに対してネットワークポリシーサーバー (NPS) が使用するポートを構成できます。
manager: brianlic
ms.topic: article
ms.assetid: 70569958-d7a7-474e-a817-6b7b5134784a
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c522206fe701d47f8f0c07e7c7a64d7e6fc7074c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944512"
---
# <a name="configure-nps-udp-port-information"></a>NPS の UDP ポート情報を構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

ネットワークポリシーサーバー (NPS) がリモート認証ダイヤルインユーザーサービス \( RADIUS 認証およびアカウンティングトラフィックに使用するポートを構成するには、次の手順を実行し \) ます。

既定では、NPS は、 \( \) インストールされているすべてのネットワークアダプターについて、インターネットプロトコルバージョン 6 IPv6 と IPv4 の両方について、ポート1812、1813、1645、および1646の RADIUS トラフィックをリッスンします。

>[!NOTE]
>IPv4 または IPv6 をネットワーク アダプターからアンインストールした場合、NPS は、アンインストールされたプロトコルについて RADIUS トラフィックを監視しません。

Authentication の場合は1812、アカウンティングの場合は1813のポート値は、 \( \) rfc 2865 および2866のインターネット技術標準化委員会によって定義される RADIUS 標準ポートです。 ただし、既定では、多くのアクセスサーバーは認証要求にポート1645を使用し、アカウンティング要求には1646を使用します。 どのようなポート番号を使用する場合でも、NPS とアクセス サーバーに同じポート番号を構成するようにしてください。

>:RADIUS の既定のポート番号を使用しない場合は、ローカルコンピューターのファイアウォールで例外を構成して、新しいポートでの RADIUS トラフィックを許可する必要があります。 詳細については、「 [Configure firewall FOR RADIUS Traffic](nps-firewalls-configure.md)」を参照してください。

この手順を完了するには、少なくとも、**Domain Admins** グループ、またはそれと同等の権限を持つグループのメンバである必要があります。

## <a name="to-configure-nps-udp-port-information"></a>NPS の UDP ポート情報を構成するには

1. NPS コンソールを開きます。
2. [**ネットワーク ポリシー サーバー**] を右クリックし、[**プロパティ**] をクリックします。
3. [**ポート**] タブをクリックし、ポートの設定を確認します。 RADIUS 認証および RADIUS アカウンティングの UDP ポートが、指定された既定値 (認証の場合は1812および1645、アカウンティングの場合は1813および 1646) と異なる場合は、[**認証**と**アカウンティング**] にポート設定を入力します。
4. 認証またはアカウンティング要求に複数のポート設定を使用するには、ポート番号をコンマで区切ります。

NPS の管理の詳細については、「 [Manage Network Policy Server](nps-manage-top.md)」を参照してください。

NPS の詳細については、「[ネットワークポリシーサーバー (nps)](nps-top.md)」を参照してください。
