---
title: 802.1 X 有線および無線展開のサーバー証明書を展開する
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: 0a39ecae-39cc-4f26-bd6f-b71ed02fc4ad
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2d4cdcd11e0eb334064ddefec0eda775ffccff2c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446473"
---
# <a name="deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>802.1 X 有線および無線展開のサーバー証明書を展開する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このガイドを使用して、リモート アクセスおよびネットワーク ポリシー サーバー (NPS) のインフラストラクチャ サーバーにサーバー証明書をデプロイすることができます。   

このガイドは次のセクションで構成されます。  

-   [このガイドを使用するための前提条件](#bkmk_pre)  

-   [このガイドで説明されていないもの](#bkmk_not)  

-   [テクノロジの概要](#bkmk_tech)  

-   [サーバー証明書の展開の概要](Server-Certificate-Deployment-Overview.md)  

-   [サーバー証明書の展開の計画](Server-Certificate-Deployment-Planning.md)  

-   [サーバー証明書の展開](Server-Certificate-Deployment.md)  

### <a name="digital-server-certificates"></a>**サーバーのデジタル証明書**  
このガイドでは、リモート アクセス サーバーと NPS インフラストラクチャ サーバーに証明書を自動的に登録する Active Directory 証明書サービス (AD CS) を使用する手順を提供します。 AD CS を使用すると、公開キー基盤 (PKI) を構築し、組織の公開キーの暗号化、デジタル証明書、およびデジタル署名機能を提供できます。  

デジタル サーバー証明書、ネットワーク上のコンピューター間の認証を使用する場合、証明書を提供します。   

1. 暗号化による機密性。  
2. デジタル署名によって整合性。  
3. コンピューター ネットワーク上のコンピューター、ユーザー、またはデバイス アカウントと証明書のキーを関連付けることによって認証されます。  

### <a name="server-types"></a>**サーバーの種類**  
このガイドを使用すると、次の種類のサーバーにサーバー証明書を展開できます。  
- メンバーであるし、DirectAccess または標準の仮想プライベート ネットワーク (VPN) サーバー、なっている、リモート アクセス サービスを実行しているサーバー、 **RAS and IAS Servers**グループ。  
- ネットワーク ポリシー サーバー (NPS) サービスが実行するサーバーのメンバーである、 **RAS and IAS Servers**グループ。  

### <a name="advantages-of-certificate-autoenrollment"></a>**証明書の自動登録の利点**  
自動登録の場合とも呼ばれる、サーバー証明書の自動登録には次の利点があります。  

- AD CS 証明機関 (CA) は、すべての NPS とリモート アクセス サーバーにサーバー証明書を自動的に登録します。  
- ドメイン内のすべてのコンピューターが信頼されたルート証明機関にインストールされている CA 証明書を自動的に受信するすべてのドメイン メンバー コンピューターに保存します。 このため、ドメイン内のすべてのコンピューターは、CA によって発行された証明書を信頼します。 この信頼により、互いに自分の身元し、セキュリティで保護された通信に参加するには、認証サーバーです。  
- グループ ポリシーを更新するには、以外のすべてのサーバーの手動の再構成は必要ありません。  
- すべてのサーバー証明書には、拡張キー使用法 (EKU) 拡張機能で、サーバー認証の目的と、クライアント認証の目的の両方が含まれます。  
- スケーラビリティ。 このガイドで、エンタープライズ ルート CA を展開した後は、エンタープライズの下位 Ca を追加することで、公開キー基盤 (PKI) を展開できます。  
- 管理の容易さ。 AD CS のコンソールを使用して、または Windows PowerShell コマンドとスクリプトを使用して、AD CS を管理できます。  
- 簡易化。 Active Directory グループ アカウントとグループのメンバーシップを使用してサーバー証明書を登録するサーバーを指定するとします。   
- サーバー証明書を展開するときに、証明書はこのガイドの手順で構成するテンプレートに基づきます。 つまり、特定のサーバーの型の別の証明書テンプレートをカスタマイズするまたは発行するすべてのサーバー証明書の同じテンプレートを使用することができます。  

## <a name="bkmk_pre"></a>このガイドを使用するための前提条件  

このガイドは、Windows Server 2016 で AD CS および Web サーバー (IIS) サーバーの役割を使用して、サーバー証明書をデプロイする方法について説明します。 このガイドの手順を実行するための前提条件を次に示します。  

- Windows Server 2016 コア ネットワーク ガイドを使用して、コア ネットワークをデプロイする必要があります。 または既にインストールされているし、正しく機能しているネットワーク上のコア ネットワーク ガイドで提供されるテクノロジが必要です。 これらのテクノロジは、TCP/IP v4、DHCP、Active Directory ドメインのサービス (AD DS)、DNS、および NPS。  
  >[!NOTE]
  >Windows Server 2016 コア ネットワーク ガイドは、Windows Server 2016 テクニカル ライブラリで使用できます。 詳細については、次を参照してください。[コア ネットワーク ガイド](../../../core-network-guide/Core-Network-Guide.md)します。

- 展開を実行する前にこの展開する準備は、このガイドの計画セクションを参照する必要があります。  
- このガイドに記載されている順序で手順を行う必要があります。 先に進んだりしないようにし、サーバー、または、展開の展開に至るまでの手順を実行すると失敗せずに、CA を展開します。  
- なる、エンタープライズ ルート ca で AD CS をインストールしたが 1 台のサーバーとなる Web se に CA が証明書失効リスト (CRL) を発行できるように、Web サーバー (IIS) をインストールする 1 つのサーバー、ネットワークの上 2 つの新しいサーバーを展開する準備する必要があります。した rver します。   

>[!NOTE]  
>このガイドにも、組織の名前付け規則に従ってコンピューターの名前か、展開する Web および AD CS サーバーに静的 IP アドレスを割り当てる準備ができます。 さらに、ドメインにコンピューターを参加する必要があります。  

## <a name="bkmk_not"></a>このガイドで説明としていないもの  
このガイドでは、設計と AD CS を使用して、公開キー基盤 (PKI) の展開に関する包括的な手順は提供されません。 AD CS のドキュメントと、このガイドではテクノロジを展開する前に PKI 設計のドキュメントを確認することをお勧めします。   

## <a name="bkmk_tech"></a>テクノロジの概要  
AD CS および Web サーバー (IIS) のテクノロジの概要を次に示します。  

### <a name="active-directory-certificate-services"></a>Active Directory 証明書サービス  
Windows Server 2016 での AD CS では、作成および公開キー テクノロジを採用しているソフトウェア セキュリティ システムで使用される X.509 証明書を管理するためのカスタマイズ可能なサービスを提供します。 組織では、ユーザー、デバイス、またはサービスの id を対応する公開キーにバインドすることによってセキュリティを強化するために AD CS を使用できます。 AD CS には、証明書の登録と失効多様な拡張性の高い環境で管理できるようにする機能も含まれています。  

詳細については、次を参照してください。 [Active Directory 証明書サービスの概要](https://technet.microsoft.com/library/hh831740.aspx)と[公開キー インフラストラクチャの設計ガイダンス](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx)します。  

### <a name="web-server-iis"></a>Web サーバー (IIS)  

Windows Server 2016 での Web サーバー (IIS) ロールは、web サイト、サービス、およびアプリケーションを確実にホストのセキュリティで保護された、管理が容易なモジュール、および拡張可能なプラットフォームを提供します。 IIS では、インターネット、イントラネットまたはエクストラネット上のユーザーと情報を共有できます。 IIS は、IIS、ASP.NET、FTP サービス、PHP、および Windows Communication Foundation (WCF) を一体化した統合 web プラットフォームです。  

詳細については、次を参照してください。 [Web サーバー (IIS) の概要](https://technet.microsoft.com/library/hh831725.aspx)します。  
