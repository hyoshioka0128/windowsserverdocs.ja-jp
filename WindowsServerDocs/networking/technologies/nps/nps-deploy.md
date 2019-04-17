---
title: ネットワーク ポリシー サーバーを展開します。
description: このトピックでは、Windows Server 2016 では、ネットワーク ポリシー サーバーの展開のコンテンツへのリンクを提供し、NPS に関する追加のガイダンスへのリンクが含まれています。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: daf62e2a593014e16bcb5fd16542b2e9c75b9c1d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-network-policy-server"></a>ネットワーク ポリシー サーバーを展開します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

ネットワーク ポリシー サーバーを展開する方法については、このトピックを使用できます。

>[!NOTE]
>他のネットワーク ポリシー サーバーのドキュメント ライブラリの以下のセクションでを使用することができます。  
>- [ネットワーク ポリシー サーバーの概要](nps-getstart-top.md)
>- [ネットワーク ポリシー サーバーを計画します。](nps-plan-top.md)
>- [ネットワーク ポリシー サーバーを管理します。](nps-manage-top.md)

Windows Server 2016 コア ネットワーク ガイドには計画およびネットワーク ポリシー サーバー \(NPS\) のインストールに関するセクションが含まれていて、このガイドで紹介するテクノロジは、Active Directory ドメインに NPS の展開の前提条件として機能します。 詳細については、Windows Server 2016 で「NPS1 の展開」セクションを参照してください。[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployNPS1)します。

## <a name="deploy-nps-server-certificates-for-vpn-and-8021x-access"></a>VPN および 802.1 X アクセス用の NPS サーバーの証明書を展開します。

ガイドを使用して NPS サーバーの証明書を展開するには、NPS サーバーのサーバー証明書の使用を必要とする、Extensible Authentication Protocol \(EAP\) など、保護された EAP の認証方法を展開する場合は、[802.1 X ワイヤードおよびワイヤレス展開用のサーバー証明書の展開](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)します。

## <a name="deploy-nps-for-8021x-wireless-access"></a>NPS を 802.1 X ワイヤレス アクセスを展開します。

ワイヤレス アクセスのためには、NPS を展開するには、ガイドを使用することができます[展開パスワード ベース 802.1 X 認証ワイヤレス アクセス](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access)します。

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Windows 10 VPN アクセス用の NPS を展開します。

NPS を使用すると、コンピューターと Windows 10 を実行しているデバイスを使用しているリモートの社員の接続を常に仮想プライベート ネットワーク \(VPN\) に対する接続要求を処理します。

詳細については、次を参照してください。、[リモート アクセス常に [VPN の展開ガイドの Windows Server 2016 および Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy)します。

