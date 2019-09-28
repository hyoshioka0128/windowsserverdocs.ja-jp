---
title: NPS の UDP ポート情報を構成する
description: このトピックを使用して、Windows Server 2016 のリモート認証ダイヤルインユーザーサービス (RADIUS) 認証およびアカウンティングトラフィックに対してネットワークポリシーサーバー (NPS) が使用するポートを構成できます。
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 70569958-d7a7-474e-a817-6b7b5134784a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1ba6c059639b9ae7e77a9e103e7ed84f6a2032df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405302"
---
# <a name="configure-nps-udp-port-information"></a>NPS の UDP ポート情報を構成する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

ネットワークポリシーサーバー (NPS) がリモート認証ダイヤルインユーザーサービス @no__t 0RADIUS @ no__t 認証およびアカウンティングトラフィックに使用するポートを構成するには、次の手順を実行します。

既定では、NPS は、インターネットプロトコルバージョン 6 \(IPv6 @ no__t と IPv4 の両方について、ポート1812、1813、1645、および1646の RADIUS トラフィックをリッスンします。

>[!NOTE]
>ネットワークアダプターで IPv4 または IPv6 のいずれかをアンインストールした場合、NPS は、アンインストールされたプロトコルの RADIUS トラフィックを監視しません。

Authentication の場合は1812、アカウンティングの場合は1813のポート値は、インターネット技術標準化委員会によって定義されている RADIUS 標準ポート \(IETF @ no__t-1 (Rfc 2865 および 2866) です。 ただし、既定では、多くのアクセスサーバーは認証要求にポート1645を使用し、アカウンティング要求には1646を使用します。 どのポート番号を使用するかにかかわらず、NPS とアクセスサーバーが同じものを使用するように構成されていることを確認してください。

>:RADIUS の既定のポート番号を使用しない場合は、ローカルコンピューターのファイアウォールで例外を構成して、新しいポートでの RADIUS トラフィックを許可する必要があります。 詳細については、「 [Configure firewall FOR RADIUS Traffic](nps-firewalls-configure.md)」を参照してください。

この手順を完了するには、少なくとも **Domain Admins** グループ、またはそれと同等のメンバーシップが必要です。

## <a name="to-configure-nps-udp-port-information"></a>NPS の UDP ポート情報を構成するには 

1. NPS コンソールを開きます。
2. **[ネットワーク ポリシー サーバー]** を右クリックし、 **[プロパティ]** をクリックします。
3. **[ポート]** タブをクリックし、ポートの設定を確認します。 RADIUS 認証および RADIUS アカウンティングの UDP ポートが、指定された既定値 (認証の場合は1812および1645、アカウンティングの場合は1813および 1646) と異なる場合は、[**認証**と**アカウンティング**] にポート設定を入力します。
4. 認証またはアカウンティング要求に複数のポート設定を使用するには、ポート番号をコンマで区切ります。

NPS の管理の詳細については、「 [Manage Network Policy Server](nps-manage-top.md)」を参照してください。

NPS の詳細については、「[ネットワークポリシーサーバー (nps)](nps-top.md)」を参照してください。
