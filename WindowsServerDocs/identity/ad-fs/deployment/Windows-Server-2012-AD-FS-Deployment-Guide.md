---
ms.assetid: e2ad9e80-a036-4bac-a4fb-afa83756aa1f
title: Windows Server 2012 AD FS デプロイ ガイド
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: aeb1d9042cea6be77ea15f6c753d720d7f814fe6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855825"
---
# <a name="windows-server-2012-ad-fs-deployment-guide"></a>Windows Server 2012 AD FS デプロイ ガイド


Active Directory&reg; Federation Services \(AD FS\) を Windows Server&reg; 2012 オペレーティングシステムと共に使用することで、組織やプラットフォームの境界を越えて、識別、認証、および承認の分散サービスを Web\-ベースのアプリケーションに拡張するフェデレーション id 管理ソリューションを構築できます。 AD FS を展開することにより、組織の既存の id 管理機能をインターネットに拡張できます。  
  
AD FS を展開すると、次のことが可能になります。  
  
-   従業員または顧客が、内部でホストされている Web サイトまたはサービスにリモートアクセスする必要がある場合に、\(SSO\) エクスペリエンスに基づいて、Web\-ベースのシングル\-署名\-を提供します。  
  
-   従業員または顧客が、ネットワークのファイアウォール内から\-組織の Web サイトまたはサービスにアクセスするときに、Web\-ベースの SSO エクスペリエンスを提供します。  
  
-   従業員または顧客が複数回ログオンすることなく、インターネット上のフェデレーションパートナー組織内の Web\-ベースのリソースにシームレスにアクセスできるようにします。  
  
-   Windows Live ID、Liberty アライアンス、およびその他の\)のプロバイダー \(、他の署名\-を使用しなくても、従業員または顧客の id を完全に管理できます。  
  
## <a name="about-this-guide"></a>このガイドについて  
本ガイドはシステム管理者とシステム エンジニアによる使用を意図しています。 ここでは、お客様または組織内のインフラストラクチャスペシャリストやシステムアーキテクトによって事前選択された AD FS 設計を展開するための詳細なガイダンスを提供します。  
  
設計がまだ選択されていない場合は、 [Windows Server 2012 の AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)の設計オプションを確認し、組織に最適な設計を選択してから、このガイドの手順に従うことをお勧めします。 既に選択されている設計でこのガイドを使用する方法の詳細については、「 [AD FS デザイン計画の実装](Implementing-Your-AD-FS-Design-Plan.md)」を参照してください。  
  
設計ガイドから設計を選択し、要求、トークンの種類、属性ストア、およびその他の項目に関する必要な情報を収集したら、このガイドを使用して、実稼働環境に AD FS 設計をデプロイできます。 このガイドでは、次のいずれかの主要な AD FS 設計を展開する手順について説明します。  
  
-   Web SSO  
  
-   フェデレーション Web SSO  
  
[AD FS 設計計画の実装](Implementing-Your-AD-FS-Design-Plan.md)に関するチェックリストを使用して、このガイドの指示に従って特定の設計をデプロイするための最適な方法を決定します。 AD FS を展開するためのハードウェアとソフトウェアの要件の詳細については、AD FS 設計ガイドの[「付録 a: AD FS 要件の確認](https://technet.microsoft.com/library/ff678034.aspx)」を参照してください。  
  
### <a name="what-this-guide-does-not-provide"></a>このガイドで説明されていないもの  
このガイドでは、次の内容は説明されていません。  
  
-   既存のネットワークインフラストラクチャ内のフェデレーションサーバー、フェデレーションサーバープロキシ、または Web サーバーをいつどこに配置するかについてのガイダンス。 この情報については、AD FS 設計ガイドの「[フェデレーションサーバーの配置を計画](https://technet.microsoft.com/library/dd807069.aspx)する」および「[フェデレーションサーバープロキシの配置を計画](https://technet.microsoft.com/library/dd807130.aspx)する」を参照してください。  
  
-   証明機関 \(CAs\) を使用してを設定するためのガイダンス AD FS  
  
-   特定の Web\-ベースのアプリケーションを設定または構成するためのガイダンス  
  
-   テスト ラボ環境を設定する手順。  
  
-   フェデレーション ログオン画面、web.config ファイル、または構成データベースのカスタマイズ方法に関する情報。  
  
## <a name="in-this-guide"></a>このガイドの内容  
  
-   [AD FS の展開計画](Planning-to-Deploy-AD-FS.md)  
  
-   [AD FS 設計計画の実装](Implementing-Your-AD-FS-Design-Plan.md)  
  
-   [チェックリスト: Web SSO 設計の実装](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [チェックリスト: フェデレーション Web SSO 設計の実装](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
  
-   [パートナー組織の構成](Configuring-Partner-Organizations.md)  
  
-   [要求規則の構成](Configuring-Claim-Rules.md)  
  
-   [フェデレーション サーバーの展開](Deploying-Federation-Servers.md)  
  
-   [フェデレーション サーバー プロキシの展開](Deploying-Federation-Server-Proxies.md)  
  
-   [AD FS 1.x との相互運用](Interoperating-with-AD-FS-1.x.md)  
