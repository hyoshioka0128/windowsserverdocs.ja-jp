---
ms.assetid: e2ad9e80-a036-4bac-a4fb-afa83756aa1f
title: Windows Server 2012 AD FS の展開ガイド
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 06946942bcdc5ea00acc22b91d6551a826357fcf
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868024"
---
# <a name="windows-server-2012-ad-fs-deployment-guide"></a>Windows Server 2012 AD FS の展開ガイド


Active Directory®フェデレーションサービス\(AD FS\)を Windows Server®2012オペレーティングシステムと共に使用して、分散識別、認証、およびを拡張するフェデレーション id 管理ソリューションを構築できます。組織やプラットフォームの\-境界を越えた Web ベースのアプリケーションに対する認証サービス。 AD FS を展開することにより、組織の既存の id 管理機能をインターネットに拡張できます。  
  
AD FS を展開すると、次のことが可能になります。  
  
-   内部でホストされている web\-サイトまたはサービス\-にリモートアクセスする必要がある場合、従業員や顧客に対して web ベースのシングル\-サインオン\(SSO\)エクスペリエンスを提供します。  
  
-   従業員または顧客が、ネットワークの\-ファイアウォール内から\-組織の web サイトやサービスにアクセスするときに、web ベースの SSO エクスペリエンスを提供します。  
  
-   従業員または顧客が複数回ログオンすること\-なく、インターネット上のフェデレーションパートナー組織内の Web ベースのリソースにシームレスにアクセスできるようにします。  
  
-   他のサイン\-オンプロバイダー \((Windows Live ID、\)Liberty アライアンスなど) を使用しなくても、従業員または顧客の id を完全に管理できます。  
  
## <a name="about-this-guide"></a>このガイドについて  
本ガイドはシステム管理者とシステム エンジニアによる使用を意図しています。 ここでは、お客様または組織内のインフラストラクチャスペシャリストやシステムアーキテクトによって事前選択された AD FS 設計を展開するための詳細なガイダンスを提供します。  
  
設計がまだ選択されていない場合は、 [Windows Server 2012 の AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)の設計オプションを確認して、に最適な設計を選択するまで、このガイドの手順に従うことをお勧めします。部門. 既に選択されている設計でこのガイドを使用する方法の詳細については、「 [AD FS デザイン計画の実装](Implementing-Your-AD-FS-Design-Plan.md)」を参照してください。  
  
設計ガイドから設計を選択し、要求、トークンの種類、属性ストア、およびその他の項目に関する必要な情報を収集したら、このガイドを使用して、実稼働環境に AD FS 設計をデプロイできます。 このガイドでは、次のいずれかの主要な AD FS 設計を展開する手順について説明します。  
  
-   Web SSO  
  
-   フェデレーション Web SSO  
  
[AD FS 設計計画の実装](Implementing-Your-AD-FS-Design-Plan.md)に関するチェックリストを使用して、このガイドの指示に従って特定の設計をデプロイするための最適な方法を決定します。 AD FS を[展開するためのハードウェアとソフトウェアの要件の詳細については、「付録 a:AD FS 設計ガイド](https://technet.microsoft.com/library/ff678034.aspx)の「AD FS の要件」を参照してください。  
  
### <a name="what-this-guide-does-not-provide"></a>このガイドで説明されていないもの  
このガイドでは、次の内容は説明されていません。  
  
-   既存のネットワークインフラストラクチャ内のフェデレーションサーバー、フェデレーションサーバープロキシ、または Web サーバーをいつどこに配置するかについてのガイダンス。 この情報については、AD FS 設計ガイドの「[フェデレーションサーバーの配置を計画](https://technet.microsoft.com/library/dd807069.aspx)する」および「[フェデレーションサーバープロキシの配置を計画](https://technet.microsoft.com/library/dd807130.aspx)する」を参照してください。  
  
-   証明機関\(ca\)を使用して AD FS を設定するためのガイダンス  
  
-   特定の Web\-ベースアプリケーションを設定または構成するためのガイダンス  
  
-   テスト ラボ環境を設定する手順。  
  
-   フェデレーション ログオン画面、web.config ファイル、または構成データベースのカスタマイズ方法に関する情報。  
  
## <a name="in-this-guide"></a>このガイドについて  
  
-   [AD FS の展開計画](Planning-to-Deploy-AD-FS.md)  
  
-   [AD FS 設計計画の実装](Implementing-Your-AD-FS-Design-Plan.md)  
  
-   [チェックリスト:Web SSO 設計の実装](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [チェックリスト:フェデレーション Web SSO 設計の実装](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
  
-   [パートナー組織の構成](Configuring-Partner-Organizations.md)  
  
-   [要求規則の構成](Configuring-Claim-Rules.md)  
  
-   [フェデレーション サーバーの展開](Deploying-Federation-Servers.md)  
  
-   [フェデレーション サーバー プロキシの展開](Deploying-Federation-Server-Proxies.md)  
  
-   [AD FS 1.x との相互運用](Interoperating-with-AD-FS-1.x.md)  
