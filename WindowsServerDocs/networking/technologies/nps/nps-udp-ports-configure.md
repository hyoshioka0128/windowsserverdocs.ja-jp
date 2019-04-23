---
title: NPS の UDP ポート情報を構成する
description: このトピックを使用して、リモート認証ダイヤルイン ユーザー サービス (RADIUS) 認証と Windows Server 2016 でアカウンティング トラフィックにネットワーク ポリシー サーバー (NPS) を使用するポートを構成することができます。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 70569958-d7a7-474e-a817-6b7b5134784a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 44c20092180c47e97f1505271203f4491606bbcf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851973"
---
# <a name="configure-nps-udp-port-information"></a>NPS の UDP ポート情報を構成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

次の手順を使用して、リモート認証ダイヤルイン ユーザー サービスのネットワーク ポリシー サーバー (NPS) を使用するポートを構成する\(RADIUS\)認証およびアカウンティングのトラフィック。

既定では、NPS が RADIUS トラフィックをポート 1812、1813、1645、およびインターネット プロトコル バージョン 6 の両方の 1646 でリッスン\(IPv6\)とすべてのインストールされているネットワーク アダプターの IPv4 です。

>[!NOTE]
>ネットワーク アダプターの IPv4 または IPv6 のいずれかをアンインストールする場合、NPS は、アンインストールされたプロトコルについて RADIUS トラフィックを監視しません。

値は、認証用は 1812、アカウンティング用は 1813 は RADIUS 標準ポートを定義して、Internet Engineering Task Force \(IETF\) Rfc 2865 および 2866 でします。 ただし、既定では、多くのアクセス サーバーを使用して、認証要求の 1645 と 1646 アカウンティング要求。 どのポート番号を使用することに関係なく、同じものを使用する NPS とアクセス サーバーが構成されていることを確認します。

>[重要]RADIUS の既定のポート番号を使用しない場合は、新しいポートで RADIUS トラフィックを許可するローカル コンピューターのファイアウォールで例外を構成する必要があります。 詳細については、次を参照してください。 [RADIUS トラフィックのファイアウォールの構成](nps-firewalls-configure.md)します。

この手順を完了するには、少なくとも **Domain Admins** グループ、またはそれと同等のメンバーシップが必要です。

## <a name="to-configure-nps-udp-port-information"></a>NPS の UDP ポート情報を構成するには 

1. NPS コンソールを開きます。
2. **[ネットワーク ポリシー サーバー]** を右クリックし、**[プロパティ]** をクリックします。
3. をクリックして、**ポート**タブをクリックし、ポートの設定を確認します。 RADIUS 認証および RADIUS アカウンティングの UDP ポートは、既定値 (1812 および 1645 認証の場合と 1813 および 1646 をアカウンティング用) から変化する場合、入力で使用するポート設定**認証**と**アカウンティング**します。
4. 認証またはアカウンティング要求を複数のポート設定を使用するには、ポート番号をコンマで区切ります。

NPS の管理に関する詳細については、次を参照してください。[ネットワーク ポリシー サーバーの管理](nps-manage-top.md)します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。
