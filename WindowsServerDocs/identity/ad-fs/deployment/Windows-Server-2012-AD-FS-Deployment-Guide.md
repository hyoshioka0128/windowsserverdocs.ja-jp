---
ms.assetid: e2ad9e80-a036-4bac-a4fb-afa83756aa1f
title: "Windows Server 2012 AD FS 展開ガイド"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3e555d1003878e12320cb8557bd205ac24e1bbb3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="windows-server-2012-ad-fs-deployment-guide"></a>Windows Server 2012 AD FS 展開ガイド

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server® 2012 オペレーティング システムで Active Directory® フェデレーション サービス \(AD FS\) を使って、組織やプラットフォームの境界を越えて、分散識別、認証、および承認サービスを Web ベース アプリケーションを拡張するフェデレーション ID 管理ソリューションを構築できます。 AD FS を展開して、インターネットに、組織の既存の ID 管理機能を拡張できます。  
  
AD FS を展開できます。  
  
-   内部でホストされる Web サイトやサービスへのリモート アクセスを必要があるときに Web ベース、シングル sign\-で \(SSO\) 体験従業員または顧客を提供します。  
  
-   クロス組織の Web サイトやネットワークのファイアウォール内からサービスにアクセスするときに、Web ベースの sso で従業員または顧客を提供します。  
  
-   従業員または顧客が複数回ログオンを必要とせず、インターネット上のフェデレーション パートナー組織内の Web ベースのリソースにシームレスなアクセス権を持つ従業員または顧客を提供します。  
  
-   その他の sign\ にプロバイダーを使用せず、従業員または顧客の ID を完全に制御を保持 \ (Windows Live ID、Liberty Alliance などと others\)。  
  
## <a name="about-this-guide"></a>このガイドについて  
このガイドは、システム管理者とシステム エンジニアが対象読者です。 または、組織内のインフラストラクチャ専門家やシステム アーキテクトによって事前に選択された AD FS 設計を展開するための詳しいガイダンスを提供します。  
  
設計のオプションを確認した後まで、このガイドの指示に従って待機することをお勧め設計が選択されていない場合、 [Windows Server 2012 で AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)組織にとって最適な設計を選択しているとします。 選択された設計では、このガイドの使用に関する詳細については、次を参照してください。 [AD FS 設計の計画を実装する](Implementing-Your-AD-FS-Design-Plan.md)します。  
  
設計のガイドから設計を選択し、信頼性情報、トークンの種類、属性ストア、およびその他の項目に関する必要な情報を収集した後、実稼働環境で AD FS 設計を展開するのにこのガイドを使用することができます。 このガイドでは、次の主な AD FS 設計のいずれかを展開するための手順を説明します。  
  
-   Web SSO  
  
-   フェデレーション Web SSO  
  
チェックリストを使用して[AD FS 設計の計画を実装する](Implementing-Your-AD-FS-Design-Plan.md)、特定の設計を展開するこのガイドの手順を使用する最善の方法を特定します。 AD FS を展開するためのハードウェアおよびソフトウェア要件については、次を参照してください。、[付録 a: 確認 AD FS の要件](https://technet.microsoft.com/library/ff678034.aspx)AD FS 設計ガイドにします。  
  
### <a name="what-this-guide-does-not-provide"></a>このガイドで説明としていない新機能  
このガイドでは提供されません。  
  
-   既存のネットワーク インフラストラクチャにフェデレーション サーバー、フェデレーション サーバー プロキシ、または Web サーバーを配置する場所についてのガイダンスです。 この情報は、次を参照してください。[フェデレーション サーバーの配置の計画](https://technet.microsoft.com/library/dd807069.aspx)と[フェデレーション サーバー プロキシの配置を計画](https://technet.microsoft.com/library/dd807130.aspx)AD FS 設計ガイドにします。  
  
-   証明機関 \(CAs\) を使用して AD FS をセットアップするためのガイダンス  
  
-   設定または特定の Web ベース アプリケーションを構成するためのガイダンス  
  
-   テスト ラボ環境を設定する指示をセットアップします。  
  
-   フェデレーション ログオン画面、Web.config ファイル、または構成データベースをカスタマイズする方法に関する情報。  
  
## <a name="in-this-guide"></a>このガイドで  
  
-   [AD FS の展開を計画するには](Planning-to-Deploy-AD-FS.md)  
  
-   [設計計画の AD FS を実装します。](Implementing-Your-AD-FS-Design-Plan.md)  
  
-   [チェックリスト: Web SSO 設計の実装](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [チェックリスト: フェデレーション Web SSO 設計の実装](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
  
-   [パートナー組織の構成](Configuring-Partner-Organizations.md)  
  
-   [要求規則の構成](Configuring-Claim-Rules.md)  
  
-   [フェデレーション サーバーを展開します。](Deploying-Federation-Servers.md)  
  
-   [フェデレーション サーバー プロキシを展開します。](Deploying-Federation-Server-Proxies.md)  
  
-   [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)  
