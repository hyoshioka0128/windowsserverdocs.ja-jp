---
title: ネットワーク ポリシー サーバーの展開
description: このトピックでは、Windows Server 2016 のネットワークポリシーサーバー展開コンテンツへのリンクを示し、NPS に関する追加のガイダンスへのリンクを示します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33cada472c314088bc1485bab6d9631226b0ffaf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405413"
---
# <a name="deploy-network-policy-server"></a>ネットワーク ポリシー サーバーの展開

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、ネットワークポリシーサーバーの展開について説明します。

>[!NOTE]
>ネットワークポリシーサーバーのその他のドキュメントについては、次のライブラリのセクションを参照してください。  
>- [ネットワークポリシーサーバーを使用したはじめに](nps-getstart-top.md)
>- [ネットワークポリシーサーバーを計画する](nps-plan-top.md)
>- [ネットワークポリシーサーバーの管理](nps-manage-top.md)

「Windows Server 2016 Core ネットワークガイド」には、ネットワークポリシーサーバーの計画とインストールに関するセクションが含まれています \(NPS @ no__t。このガイドに記載されているテクノロジは、Active Directory ドメインに NPS を展開するための前提条件として機能します。 詳細については、「Windows Server 2016 [Core ネットワークガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployNPS1)」の「Deploy NPS1」セクションを参照してください。

## <a name="deploy-nps-certificates-for-vpn-and-8021x-access"></a>VPN および 802.1 X アクセス用に NPS 証明書を展開する

拡張認証プロトコル @no__t、NPS でサーバー証明書を使用する必要がある保護された EAP などの認証方法を展開する場合は、「[のサーバー証明書の展開」ガイドを使用して nps 証明書を展開することができます。802.1 x ワイヤードおよびワイヤレス展開](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)。

## <a name="deploy-nps-for-8021x-wireless-access"></a>802.1 X ワイヤレスアクセス用に NPS を展開する

ワイヤレスアクセス用に NPS を展開する方法については、「[パスワードベースの 802.1 x 認証ワイヤレスアクセスの展開](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access)」ガイドを参照してください。

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Windows 10 VPN アクセス用に NPS を展開する

NPS を使用すると、Windows 10 を実行しているコンピューターとデバイスを使用しているリモート従業員の Always On 仮想プライベートネットワーク @no__t 0VPN @ no__t 接続の接続要求を処理できます。

詳細については、「 [Windows Server 2016 および windows 10 用のリモートアクセス ALWAYS ON VPN 展開ガイド](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy)」を参照してください。

