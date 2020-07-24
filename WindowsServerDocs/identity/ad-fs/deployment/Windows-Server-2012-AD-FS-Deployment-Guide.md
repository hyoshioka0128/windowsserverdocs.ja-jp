---
ms.assetid: e2ad9e80-a036-4bac-a4fb-afa83756aa1f
title: Windows Server 2012 AD FS の展開ガイド
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6abeb801bed30ebd3681e47705eb7aa409a65d71
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86964894"
---
# <a name="windows-server-2012-ad-fs-deployment-guide"></a>Windows Server 2012 AD FS の展開ガイド


&reg; \( \) Windows Server 2012 オペレーティングシステムと共に Active Directory フェデレーションサービス AD FS を使用すると、 &reg; 組織やプラットフォームの境界を越えて識別、認証、および承認の分散サービスを Web ベースのアプリケーションに拡張するフェデレーション id 管理ソリューションを構築でき \- ます。 AD FS を展開することにより、組織の既存の id 管理機能をインターネットに拡張できます。  
  
AD FS を展開すると、次のことが可能になります。  
  
-   \-内部でホストされている \- \- \( \) web サイトまたはサービスにリモートアクセスする必要がある場合、従業員や顧客に対して web ベースのシングルサインオン SSO エクスペリエンスを提供します。  
  
-   従業員または顧客が、 \- \- ネットワークのファイアウォール内から組織の web サイトやサービスにアクセスするときに、web ベースの SSO エクスペリエンスを提供します。  
  
-   従業員または顧客が \- 複数回ログオンすることなく、インターネット上のフェデレーションパートナー組織内の Web ベースのリソースにシームレスにアクセスできるようにします。  
  
-   他のサイン \- オンプロバイダー ( \( WINDOWS Live ID、Liberty アライアンスなど) を使用しなくても、従業員または顧客の id を完全に管理 \) できます。  
  
## <a name="about-this-guide"></a>このガイドについて  
本ガイドはシステム管理者とシステム エンジニアによる使用を意図しています。 ここでは、お客様または組織内のインフラストラクチャスペシャリストやシステムアーキテクトによって事前選択された AD FS 設計を展開するための詳細なガイダンスを提供します。  
  
設計がまだ選択されていない場合は、 [Windows Server 2012 の AD FS 設計ガイド](../design/ad-fs-design-guide-in-windows-server-2012.md)の設計オプションを確認し、組織に最適な設計を選択してから、このガイドの手順に従うことをお勧めします。 既に選択されている設計でこのガイドを使用する方法の詳細については、「 [AD FS デザイン計画の実装](Implementing-Your-AD-FS-Design-Plan.md)」を参照してください。  
  
設計ガイドから設計を選択し、要求、トークンの種類、属性ストア、およびその他の項目に関する必要な情報を収集したら、このガイドを使用して、実稼働環境に AD FS 設計をデプロイできます。 このガイドでは、次のいずれかの主要な AD FS 設計を展開する手順について説明します。  
  
-   Web SSO  
  
-   フェデレーション Web SSO  
  
[AD FS 設計計画の実装](Implementing-Your-AD-FS-Design-Plan.md)に関するチェックリストを使用して、このガイドの指示に従って特定の設計をデプロイするための最適な方法を決定します。 AD FS を展開するためのハードウェアとソフトウェアの要件の詳細については、AD FS 設計ガイドの[「付録 a: AD FS 要件の確認](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678034(v=ws.11))」を参照してください。  
  
### <a name="what-this-guide-does-not-provide"></a>このガイドで説明されていないもの  
このガイドでは、次の内容は説明されていません。  
  
-   既存のネットワークインフラストラクチャ内のフェデレーションサーバー、フェデレーションサーバープロキシ、または Web サーバーをいつどこに配置するかについてのガイダンス。 この情報については、AD FS 設計ガイドの「[フェデレーションサーバーの配置を計画](../design/planning-federation-server-placement.md)する」および「[フェデレーションサーバープロキシの配置を計画](../design/planning-federation-server-proxy-placement.md)する」を参照してください。  
  
-   証明機関 ca を使用して \( AD FS を設定するためのガイダンス \)  
  
-   特定の Web ベースアプリケーションを設定または構成するためのガイダンス \-  
  
-   テスト ラボ環境を設定する手順。  
  
-   フェデレーション ログオン画面、web.config ファイル、または構成データベースのカスタマイズ方法に関する情報。  
  
## <a name="in-this-guide"></a>このガイドの内容  
  
-   [AD FS の展開計画](Planning-to-Deploy-AD-FS.md)  
  
-   [AD FS 設計計画の実装](Implementing-Your-AD-FS-Design-Plan.md)  
  
-   [チェックリスト:Web SSO 設計の実装](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [チェックリスト:フェデレーション Web SSO 設計の実装](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
  
-   [パートナー組織の構成](Configuring-Partner-Organizations.md)  
  
-   [要求規則の構成](Configuring-Claim-Rules.md)  
  
-   [フェデレーション サーバーの展開](Deploying-Federation-Servers.md)  
  
-   [フェデレーション サーバー プロキシの展開](Deploying-Federation-Server-Proxies.md)  
  
-   [AD FS 1.x との相互運用](Interoperating-with-AD-FS-1.x.md)  
