---
ms.assetid: 74ef34c8-e13f-499b-b2bb-952ad7036622
title: フェデレーション サーバーの名前解決の要件
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 88ec418bd72a6389856deb1abd85641d8782bc30
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408041"
---
# <a name="name-resolution-requirements-for-federation-servers"></a>フェデレーション サーバーの名前解決の要件

企業ネットワーク上のクライアントコンピューターが Active Directory フェデレーションサービス (AD FS) \(\)AD FS によって保護されているアプリケーションまたは Web サービスにアクセスしようとすると、まずフェデレーションサーバーに対して認証を行う必要があります。 認証する方法の 1 つでは、会社のネットワーク クライアントが Windows 統合認証を通じて、ローカルのフェデレーション サーバーにアクセスします。  
  
## <a name="configure-corporate-dns"></a>企業 DNS を構成する  
ローカルのフェデレーション サーバーで Windows 統合認証を通じて正常な名前解決を実行、ドメイン ネーム システム \(DNS\) アカウントの企業ネットワーク内には、新しいホストのパートナーを構成 \(A\) 完全修飾ドメイン名を解決するリソース レコード \(FQDN\) フェデレーション サーバー クラスターの IP アドレスにフェデレーション サーバーのホスト名です。  
  
次の図を見ると、特定のシナリオでのこのタスクの実現方法がわかります。 この場合は、Microsoft Network Load Balancing \(NLB\) 既存のフェデレーション サーバー ファームの 1 つのクラスターの FQDN 名と 1 つのクラスター IP アドレスを提供します。  
  
![名の要件](media/adfs2_deploy_single_fs.gif)  
  
NLB を使用する FQDN をクラスターまたはクラスターの IP アドレスを構成する方法については、[クラスター パラメーターの指定](https://go.microsoft.com/fwlink/?LinkId=75282)を参照してください。  
  
会社の DNS にフェデレーション サーバーを構成する方法については、[企業 DNS にフェデレーション サーバーのホスト &#40;A&#41; リソース レコードを追加する](../../ad-fs/deployment/Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)を参照してください。  
  
境界ネットワーク内のフェデレーション サーバー プロキシを構成する方法については、[フェデレーション サーバー プロキシの名前解決要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)参照してください。  
  

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
