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
ms.openlocfilehash: 6be56c25cc6f639f73842f57cdf48a6339dccf9c
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191855"
---
# <a name="windows-server-2012-ad-fs-deployment-guide"></a>Windows Server 2012 AD FS の展開ガイド


Active Directory® フェデレーション サービスを使用する\(AD FS\)分散の識別を拡張するフェデレーション id 管理ソリューションをビルドする Windows Server® 2012 オペレーティング システムで、認証と承認サービスを Web\-組織やプラットフォームの境界を越えてベースのアプリケーション。 AD FS を展開することで、組織の既存の ID 管理機能をインターネットにまで拡張できます。  
  
AD FS を展開すると、次のことが可能になります。  
  
-   従業員または顧客を備えた Web\-シングル、\-サインオン\-で\(SSO\)エクスペリエンスへのリモート アクセスを内部的に必要なときには、Web サイトやサービスがホストされています。  
  
-   従業員または顧客を備えた Web\-、SSO が発生する間にアクセスするときに\-組織の Web サイトやネットワークのファイアウォール内からサービス。  
  
-   シームレスなアクセス権を持つ従業員または顧客を Web に提供\-複数回ログオンするには、従業員または顧客を必要とせず、インターネット上でフェデレーション パートナー組織内のリソースのベースします。  
  
-   その他の記号を使用せず、従業員または顧客の id を完全に制御を保持\-プロバイダー \(Windows Live ID、Liberty Alliance など、およびその他のユーザー\)します。  
  
## <a name="about-this-guide"></a>このガイドについて  
本ガイドはシステム管理者とシステム エンジニアによる使用を意図しています。 これは、ユーザーまたは組織内のインフラストラクチャ専門家やシステム アーキテクトによって事前に選択されている AD FS 設計の展開に関する詳しいガイダンスを提供します。  
  
までには、このガイドの指示に従って設計オプションを確認した後に待機することをお勧めするデザインが選択されていない場合、 [Windows Server 2012 で AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)と、最も選択しました。組織の適切な設計します。 既に選択されているデザインでこのガイドの使用に関する詳細については、次を参照してください。 [AD FS 設計の計画を実装する](Implementing-Your-AD-FS-Design-Plan.md)します。  
  
設計ガイドから設計を選択して要求、トークンの種類、属性ストア、およびその他の項目に関する必要な情報を収集して後、は、実稼働環境で AD FS 設計を展開するのにこのガイドを使用できます。 このガイドでは、次のプライマリ AD FS 設計のいずれかを展開するための手順を説明します。  
  
-   Web SSO  
  
-   フェデレーション Web SSO  
  
」のチェックリストを使用して、 [AD FS 設計の計画を実装する](Implementing-Your-AD-FS-Design-Plan.md)にこのガイドで指示を使用して、特定の設計を展開する最善の方法を決定します。 AD FS を展開するためのハードウェアとソフトウェアの要件については、次を参照してください、[付録 a:。AD FS の要件の確認](https://technet.microsoft.com/library/ff678034.aspx)で AD FS 設計ガイド。  
  
### <a name="what-this-guide-does-not-provide"></a>このガイドで説明されていないもの  
このガイドでは、次の内容は説明されていません。  
  
-   既存のネットワーク インフラストラクチャにフェデレーション サーバー、フェデレーション サーバー プロキシ、または Web サーバーを配置するタイミングと場所に関するガイダンスです。 詳細については、次を参照してください。[フェデレーション サーバーの配置の計画](https://technet.microsoft.com/library/dd807069.aspx)と[フェデレーション サーバー プロキシの配置の計画](https://technet.microsoft.com/library/dd807130.aspx)で、AD FS 設計ガイド。  
  
-   証明機関の使用に関するガイダンス\(Ca\) AD FS を設定するには  
  
-   設定するか、特定の Web の構成に関するガイダンス\-ベースのアプリケーション  
  
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
