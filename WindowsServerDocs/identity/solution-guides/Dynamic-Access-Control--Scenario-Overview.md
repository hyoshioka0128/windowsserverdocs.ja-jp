---
ms.assetid: 7b22adfa-298d-413c-88d0-1231825b7d4d
title: 'ダイナミック アクセス制御: シナリオの概要'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e53b267f1319681f4a1914b16aaed149134054a8
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2020
ms.locfileid: "78371420"
---
# <a name="dynamic-access-control-scenario-overview"></a>ダイナミック アクセス制御:シナリオの概要

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server 2012 では、ファイルサーバー全体にデータガバナンスを適用して、情報にアクセスできるユーザーの制御や、情報にアクセスしたユーザーの監査を行うことができます。 ダイナミック アクセス制御により、次のことが可能になります。  
  
-   自動および手動によるファイルの分類を使用してデータを特定する。 たとえば、組織のすべてのファイル サーバーのデータにタグを付けることができます。  
  
-   集約型のアクセス ポリシーを使用するセーフティネット ポリシーを適用し、ファイルへのアクセスを制御する。 たとえば、組織内の正常性情報にアクセスできるユーザーを定義できます。  
  
-   集約型の監査ポリシーを使用してファイルへのアクセスを監査し、コンプライアンス レポートや法的分析に使用する。 たとえば、高機密情報にアクセスしたユーザーを特定できます。  
  
-   自動 Rights Management サービス (RMS) 暗号化を使用して、機密性の高い Microsoft Office ドキュメントに RMS 保護を適用する。 たとえば、医療保険の携行性と責任に関する法律 (HIPAA) に関連する情報を含むすべてのドキュメントを暗号化するように RMS を構成できます。  
  
パートナーや基幹業務アプリケーションは、ダイナミック アクセス制御機能セットの基盤となるインフラストラクチャ投資をさらに応用できます。また、組織が Active Directory を使用している場合、これらの機能が提供する価値はより大きくなります。 このインフラストラクチャの特徴は次のとおりです。  
  
-   条件式と集約型ポリシーの処理に対応した Windows 用の新しい承認および監査エンジン。  
  
-   Kerberos 認証によるユーザーおよびデバイスの信頼性情報のサポート。  
  
-   ファイル分類インフラストラクチャ (FCI) の機能強化。  
  
-   パートナーがマイクロソフト以外のファイルを暗号化するソリューションを提供できるようにする RMS の拡張サポート。  
  
## <a name="in-this-scenario"></a>このシナリオの内容  
このコンテンツ セットの一部として、次に示すシナリオおよびガイダンスが含まれています。  
  
## <a name="BKMK_APP"></a>動的 Access Control コンテンツロードマップ  
  
|シナリオ|［評価］|プラン|配置|操作|  
|------------|------------|--------|----------|-----------|  
|**シナリオ: 集約型アクセスポリシー**<br /><br />ファイルの集約型アクセス ポリシーを作成すると、組織は、ユーザーの信頼性情報、デバイスの信頼性情報、およびリソース プロパティを使用した条件式を含む承認ポリシーを一元的に展開および管理できるようになります。 集約型アクセス ポリシーは、コンプライアンス上およびビジネス上の法的要件に基づきます。 また、Active Directory 内で作成およびホストされるため、容易に管理および展開できます。<br /><br />**フォレスト間での信頼性情報の展開**<br /><br />Windows Server 2012 では、AD DS が各フォレストで "要求ディクショナリ" を保持し、フォレスト内で使用されているすべての要求の種類が Active Directory フォレストレベルで定義されています。 プリンシパルが信頼の境界を越える必要があるシナリオは多数あります。 このシナリオでは信頼性情報が信頼の境界を越える方法について説明します。|[動的 Access Control: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)<br /><br />[フォレスト間にわたる要求の展開](Deploy-Claims-Across-Forests.md)|[計画: 集約型アクセスポリシーの展開](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<br /><br />[ビジネス要求を集約型アクセスポリシーにマップする -   プロセス](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_1)<br />[動的 Access Control の管理の委任を -   する](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.1)<br />[集約型アクセスポリシーを計画するための -   の例外メカニズム](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.2)<br /><br />ユーザーの信頼性情報を使う場合のベスト プラクティス<br /><br />[ユーザードメインの要求を有効にするための適切構成を選択](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DC_OP3)-   <br />[ユーザーの要求を有効にするための操作の](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.4.2)-   <br />[集約型アクセスポリシーを使用せずにファイルサーバーの随意 acl でユーザー要求を使用する場合の -   の考慮事項](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_5)<br /><br />[デバイスの信頼性情報とデバイスのセキュリティグループの使用](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DeviceClaims)<br /><br />[静的なデバイスの信頼性情報を使用する場合の -   の考慮事項](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.1)<br />[デバイスの信頼性情報を有効にするための操作の](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.3)-   <br /><br />展開用ツール<br /><br />-   [データ分類ツールキット](https://go.microsoft.com/fwlink/?LinkId=%20244300)|[集約型アクセスポリシー &#40;のデモンストレーション手順を展開する&#41;](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)<br /><br />[フォレスト&#40;間での要求の展開のデモンストレーション手順&#41;](Deploy-Claims-Across-Forests--Demonstration-Steps-.md)|-集約型アクセスポリシーのモデリング|  
|**シナリオ: ファイルアクセスの監査**<br /><br />セキュリティ監査は、企業のセキュリティ維持の最も強力なサポート手段の 1 つです。 セキュリティ監査の重要な目標の 1 つがコンプライアンス遵守です。 たとえば、Sarbanes Oxley、HIPAA、および Payment Card Industry (PCI) などの業界標準は、データ セキュリティとプライバシーに関する厳格なルール セットへの準拠を企業に要求します。 セキュリティ監査によってこれらのポリシーが存在するかどうかが明確化されます。つまり、監査ポリシーによって各種の標準に準拠しているかどうかが証明されます。 さらにセキュリティ監査は、異常な動作の検出、セキュリティ ポリシー内のギャップの特定と解消、さらに、ユーザー アクティビティの記録を作成し、これを使用して法的分析を実施することで、法的責任を問われる可能性のある動作の防止にも役立ちます。|[シナリオ: ファイルアクセスの監査](Scenario--File-Access-Auditing.md)|[ファイル アクセスの監査の計画](Plan-for-File-Access-Auditing.md)|[中央監査ポリシー &#40;を使用したセキュリティ監査の展開のデモンストレーション手順&#41;](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md)|[ファイルサーバーに適用される集約型アクセスポリシーを監視](https://technet.microsoft.com/library/jj574188.aspx)-   には<br />[ファイルとフォルダーに関連付けられた集約型アクセスポリシーを監視](https://technet.microsoft.com/library/jj574198.aspx)-   には<br />[ファイルとフォルダーのリソース属性を監視 -   には](https://technet.microsoft.com/library/jj574208.aspx)<br />[要求の種類を監視](https://technet.microsoft.com/library/jj574086.aspx)-   <br />[サインイン時にユーザーとデバイスの信頼性情報を監視 -   には](https://technet.microsoft.com/library/jj574082.aspx)<br />[集約型アクセスポリシーとルールの定義を監視](https://technet.microsoft.com/library/jj574115.aspx)-   には<br />[リソース属性の定義を監視](https://technet.microsoft.com/library/jj574155.aspx)-   <br />[リムーバブル記憶装置の使用を監視](https://technet.microsoft.com/library/jj574128.aspx)-   ます。|  
|**シナリオ: アクセス拒否アシスタンス**<br /><br />現在は、ユーザーがファイル サーバー上のリモート ファイルにアクセスを試みた場合、アクセスが拒否されたことだけが示されます。 このことが、問題を特定する必要があるヘルプデスクや IT 管理者への要求を増やしています。また、管理者がユーザーから適切なコンテキストを得るのが難しい場合が多いということが、この問題の解決を難しくしています。 <br />Windows Server 2012 では、データのインフォメーションワーカーおよびビジネスオーナーが、関与する前にアクセス拒否の問題を処理し、関連するときに、迅速な解決に必要なすべての情報を提供することを目的としています。 この目標を達成するうえでの課題の1つは、アクセス拒否を処理する一元的な方法がなく、すべてのアプリケーションが異なる方法で対処することです。そのため、windows Server 2012 では、Windows Explorer のアクセス拒否エクスペリエンスを向上させることが目的の1つです。|[シナリオ: アクセス拒否アシスタンス](Scenario--Access-Denied-Assistance.md)|[アクセス拒否アシスタンスの計画](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)<br /><br />[アクセス拒否アシスタンスモデルを決定 -   には](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.1)<br />[アクセス要求を処理するユーザーを決定](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_12)-   には<br />[アクセス拒否アシスタンスメッセージをカスタマイズ -   には](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_13)<br />[例外の -   計画](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.4)<br />[アクセス拒否アシスタンスの展開方法を決定 -   には](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.5)|[アクセス拒否アシスタンス&#40;の展開のデモンストレーション手順&#41;](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md)||  
|**シナリオ: Office ドキュメントの分類ベースの暗号化**<br /><br />機密情報を保護する主な目的は組織のリスクを低減することです。 HIPAA や Payment Card Industry Data Security Standard (PCI-DSS) などのさまざまなコンプライアンス規定が情報の暗号化を義務付けており、その他にも数多くのビジネス上の理由で機密情報が暗号化されています。 一方、情報の暗号化は高コストであるだけでなく、ビジネスの生産性を低下させる原因にもなります。 このためさまざまな組織がさまざまなアプローチを採用して、暗号化する情報に優先順位を設定しています。 <br />このシナリオをサポートするために、Windows Server 2012 では、機密性の高い Windows Office ファイルを分類に基づいて自動的に暗号化する機能が用意されています。 これはファイル管理タスクを通じて実行されます。ファイル管理タスクは、ファイル サーバー上のファイルを機密性が高いと認識した数秒後に Active Directory Rights Management サーバー (AD RMS) 保護を起動します。|[シナリオ: Office ドキュメントの分類ベースの暗号化](Scenario--Classification-Based-Encryption-for-Office-Documents.md)|[ドキュメントの分類ベースの暗号化用に展開を計画する](assetId:///14714ba6-d6a2-45e4-aae5-d3318817e52a)|[Office ファイル&#40;の暗号化の展開のデモンストレーションステップ&#41;](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md)||  
|**シナリオ: 分類を使用してデータに関する洞察を得る**<br /><br />データおよび記憶域リソースへの依存は、ほとんどの組織で重要度を増し続けています。 IT 管理者は、従来よりも大規模かつ複雑な記憶域インフラストラクチャを監視しながら総保有コストを妥当な水準に保つ責任を負うという、難しさを増す課題に直面しています。 記憶域リソースの管理はデータのボリュームや可用性だけに関することではなくなり、企業のポリシーを適用し、記憶域の消費用途を知ることで、効率的な使用率とリスク軽減のためのコンプライアンスを実現することも含まれるようになりました。 ファイル分類インフラストラクチャは、データを効率よく管理できるように分類プロセスを自動化することによって、データの性質を理解できるようにします。 ファイル分類インフラストラクチャでは、手動、プログラム、自動の 3 つの分類方法を使用できます。 このシナリオでは自動ファイル分類方法について扱います。|[シナリオ: 分類を使用してデータに関する洞察を得る](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)|[自動ファイル分類の計画](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)|[自動ファイル分類&#40;の展開のデモンストレーション手順&#41;](Deploy-Automatic-File-Classification--Demonstration-Steps-.md)||  
|**シナリオ: ファイルサーバーでの情報の保持を実装する**<br /><br />保持期間とは、ドキュメントの有効期限が切れるまでに保存される時間の長さです。 組織によって、保持期間が異なる場合があります。 フォルダー内のファイルを、短い保持期間のファイル、中間の保持期間のファイル、または長い保持期間のファイルとして分類し、それぞれの期間に対して期限を割り当てることができます。 訴訟ホールドにすることでファイルを無期限に保持することもできます。 <br />ファイル分類インフラストラクチャおよびファイル サーバー リソース マネージャーは、ファイル管理タスクおよびファイル分類を使用して一連のファイルに保持期間を適用します。 フォルダーに保持期間を割り当てた後にファイル管理タスクを使用することで、割り当てられた保持期間をいつまで適用するかを構成できます。 フォルダー内のファイルの有効期限が切れそうになると、ファイルの所有者に電子メールによる通知が届きます。 ファイルを訴訟ホールドとして分類し、ファイル管理タスクでファイルの有効期限が切れないように設定できます。|[シナリオ: ファイルサーバーでの情報の保持を実装する](Scenario--Implement-Retention-of-Information-on-File-Servers.md)|[ファイルサーバーの情報の保持を計画する](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)|[ファイルサーバー &#40;での情報の保持を実装する展開のデモンストレーションの手順&#41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md)||  
  
> [!NOTE]  
> ダイナミック アクセス制御は ReFS (Resilient File System) ではサポートされません。  
  
## <a name="BKMK_LINKS"></a>関連項目  
  
|コンテンツの種類|参照|  
|----------------|--------------|  
|**製品評価**|-   [動的 Access Control レビューアーガイド](https://go.microsoft.com/fwlink/?LinkId=244309)<br />[動的 Access Control 開発者ガイド](https://go.microsoft.com/fwlink/?LinkId=245870)の -   |  
|**計画**|[集約型アクセスポリシーの展開を計画](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)-   <br />[ファイルアクセスの監査の -   計画](Plan-for-File-Access-Auditing.md)|  
|**展開**|-   [Active Directory の展開](https://go.microsoft.com/fwlink/p/?LinkID=238318)<br />[ファイルサービスおよび記憶域サービスの展開](https://go.microsoft.com/fwlink/?LinkID=24430)の -   |  
|**運用**|[動的 Access Control PowerShell リファレンス](https://go.microsoft.com/fwlink/?LinkId=243150)|  
|**ツールと設定**|[データ分類ツールキット](https://go.microsoft.com/fwlink/?LinkID=244300)|  
|**コミュニティ リソース**|[ディレクトリサービスフォーラム](https://social.technet.microsoft.com/Forums/winserverDS/threads)|  
  


