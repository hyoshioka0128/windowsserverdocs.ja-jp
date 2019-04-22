---
title: ネットワーク ポリシー サーバーの展開
description: このトピックでは、Windows Server 2016 では、ネットワーク ポリシー サーバーの展開のコンテンツへのリンクを提供し、詳細なガイダンスについては、NPS へのリンクが含まれています。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8da8951a9c6ed5022c892bbf01b33614d38abc5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814843"
---
# <a name="deploy-network-policy-server"></a>ネットワーク ポリシー サーバーの展開

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

ネットワーク ポリシー サーバーの展開については、このトピックを使用できます。

>[!NOTE]
>他のネットワーク ポリシー サーバー ドキュメント ライブラリの次のセクションで使用できます。  
>- [ネットワーク ポリシー サーバーの概要](nps-getstart-top.md)
>- [ネットワーク ポリシー サーバーを計画します。](nps-plan-top.md)
>- [ネットワーク ポリシー サーバーを管理します。](nps-manage-top.md)

Windows Server 2016 コア ネットワーク ガイドには計画およびネットワーク ポリシー サーバーのインストールに関するセクションが含まれています\(NPS\)、Active Directory ドメインに NPS を展開するための前提条件として、ガイドで紹介するテクノロジが機能します。 詳細については、"NPS1 の展開"では、Windows Server 2016 のセクションを参照してください。[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployNPS1)します。

## <a name="deploy-nps-certificates-for-vpn-and-8021x-access"></a>VPN と 802.1 X アクセス NPS 証明書を展開します。

拡張認証プロトコルなどの認証方式を展開する場合\(EAP\) 、NPS でサーバーの使用を必要とする保護された EAP の証明書しは、NPS の証明書を展開するには、ガイドに[802.1 X ワイヤード (有線) およびワイヤレス展開にサーバー証明書展開](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)します。

## <a name="deploy-nps-for-8021x-wireless-access"></a>802.1 X ワイヤレス アクセス用の NPS を展開します。

ワイヤレス アクセスのためには、NPS を展開するには、ガイドを使用することができます[デプロイ パスワード ベース 802.1 X 認証ワイヤレス アクセス](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access)します。

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Windows 10 の VPN アクセス用の NPS を展開します。

NPS を使用して、常に仮想プライベート ネットワークの接続要求を処理することができます\(VPN\)コンピューターと Windows 10 を実行しているデバイスを使用しているリモートの社員用の接続。

詳細については、次を参照してください。、[リモート アクセス常に VPN 展開ガイドの Windows Server 2016 および Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy)します。

