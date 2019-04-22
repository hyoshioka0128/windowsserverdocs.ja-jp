---
ms.assetid: 7b22adfa-298d-413c-88d0-1231825b7d4d
title: 'ダイナミック アクセス制御: シナリオの概要'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f70bd138a16b23f1fbf7bfabc98ee184e3b9ab37
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825573"
---
# <a name="dynamic-access-control-scenario-overview"></a>ダイナミック アクセス制御:シナリオの概要

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Windows Server 2012 の情報にアクセスしたファイル サーバー情報にアクセスできるユーザーを制御および監査する全体にわたってデータ ガバナンスを適用できます。 ダイナミック アクセス制御により、次のことが可能になります。  
  
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
  
## <a name="BKMK_APP"></a>ダイナミック アクセス制御: コンテンツ ロードマップ  
  
|シナリオ|評価|プラン|配置|操作|  
|------------|------------|--------|----------|-----------|  
|**シナリオ:集約型アクセス ポリシー**<br /><br />ファイルの集約型アクセス ポリシーを作成すると、組織は、ユーザーの信頼性情報、デバイスの信頼性情報、およびリソース プロパティを使用した条件式を含む承認ポリシーを一元的に展開および管理できるようになります。 集約型アクセス ポリシーは、コンプライアンス上およびビジネス上の法的要件に基づきます。 また、Active Directory 内で作成およびホストされるため、容易に管理および展開できます。<br /><br />**フォレスト間にわたる信頼性情報の展開**<br /><br />Windows Server 2012 の AD DS フォレストごとに '信頼性情報ディクショナリ"を保持して、Active Directory フォレスト レベルで、フォレスト内で使用中の種類が定義されているすべての信頼性情報します。 プリンシパルが信頼の境界を越える必要があるシナリオは多数あります。 このシナリオでは信頼性情報が信頼の境界を越える方法について説明します。|[ダイナミック アクセス制御:シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)<br /><br />[フォレスト間にわたる信頼性情報を展開します。](Deploy-Claims-Across-Forests.md)|[プラン:集約型アクセス ポリシーの展開](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<br /><br />-   [集約型アクセス ポリシーをビジネス要求をマップするプロセス](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_1)<br />-   [ダイナミック アクセス制御の管理の委任](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.1)<br />-   [集約型アクセス ポリシーの計画の例外メカニズム](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.2)<br /><br />ユーザーの信頼性情報を使う場合のベスト プラクティス<br /><br />-   [ユーザー ドメイン内の要求を有効にする適切な構成の選択](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DC_OP3)<br />-   [ユーザーの信頼性情報を有効にする操作](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.4.2)<br />-   [ファイル サーバーでのユーザーの信頼性情報の使用に関する注意点集約型アクセス ポリシーを使用せず、随意 Acl](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_5)<br /><br />[デバイスの信頼性情報とデバイスのセキュリティ グループを使用してください。](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DeviceClaims)<br /><br />-   [静的なデバイスの信頼性情報の使用に関する注意点](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.1)<br />-   [デバイスの信頼性情報を有効にする操作](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.3)<br /><br />展開用ツール<br /><br />-   [Data Classification Toolkit](https://go.microsoft.com/fwlink/?LinkId=%20244300)|[集約型アクセス ポリシーを展開&#40;デモンストレーション手順&#41;](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)<br /><br />[フォレスト間にわたる信頼性情報の展開&#40;デモンストレーション手順&#41;](Deploy-Claims-Across-Forests--Demonstration-Steps-.md)|-集約型アクセス ポリシーのモデリング|  
|**シナリオ:ファイル アクセスの監査**<br /><br />セキュリティ監査は、企業のセキュリティ維持の最も強力なサポート手段の 1 つです。 セキュリティ監査の重要な目標の 1 つがコンプライアンス遵守です。 たとえば、Sarbanes Oxley、HIPAA、および Payment Card Industry (PCI) などの業界標準は、データ セキュリティとプライバシーに関する厳格なルール セットへの準拠を企業に要求します。 セキュリティ監査によってこれらのポリシーが存在するかどうかが明確化されます。つまり、監査ポリシーによって各種の標準に準拠しているかどうかが証明されます。 さらにセキュリティ監査は、異常な動作の検出、セキュリティ ポリシー内のギャップの特定と解消、さらに、ユーザー アクティビティの記録を作成し、これを使用して法的分析を実施することで、法的責任を問われる可能性のある動作の防止にも役立ちます。|[シナリオ:ファイル アクセスの監査](Scenario--File-Access-Auditing.md)|[計画ファイル アクセスの監査](Plan-for-File-Access-Auditing.md)|[セキュリティ監査サーバーの全体の監査ポリシーを展開&#40;デモンストレーション手順&#41;](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md)|-   [ファイル サーバーに適用する集約型アクセス ポリシーを監視します。](https://technet.microsoft.com/library/jj574188.aspx)<br />-   [ファイルとフォルダーに関連付けられた集約型アクセス ポリシーを監視します。](https://technet.microsoft.com/library/jj574198.aspx)<br />-   [リソース属性のファイルとフォルダーを監視します。](https://technet.microsoft.com/library/jj574208.aspx)<br />-   [モニターの要求の種類](https://technet.microsoft.com/library/jj574086.aspx)<br />-   [サインイン時にユーザーとデバイスの信頼性情報を監視します。](https://technet.microsoft.com/library/jj574082.aspx)<br />-   [集約型アクセス ポリシーのモニターとルールの定義](https://technet.microsoft.com/library/jj574115.aspx)<br />-   [監視リソース属性の定義](https://technet.microsoft.com/library/jj574155.aspx)<br />-   [リムーバブル記憶装置の使用状況監視](https://technet.microsoft.com/library/jj574128.aspx)します。|  
|**シナリオ:アクセス拒否アシスタンス**<br /><br />現在は、ユーザーがファイル サーバー上のリモート ファイルにアクセスを試みた場合、アクセスが拒否されたことだけが示されます。 このことが、問題を特定する必要があるヘルプデスクや IT 管理者への要求を増やしています。また、管理者がユーザーから適切なコンテキストを得るのが難しい場合が多いということが、この問題の解決を難しくしています。 <br />Windows Server 2012 の目標は、インフォメーション ワーカーおよびデータのビジネス オーナーがアクセス拒否 IT を取得する前に問題に対処するために、関連する時期と IT が関与するが、すばやく解決するためのすべての適切な情報を提供します。 この目標を達成するための課題の 1 つはアクセスが拒否された対処するための中央の方法はありませんし、それを異なる方法ですべてのアプリケーションが処理、ため Windows Explorer 用アクセス拒否エクスペリエンスを向上させるためには、目標の 1 つの Windows Server 2012。|[シナリオ:アクセス拒否アシスタンス](Scenario--Access-Denied-Assistance.md)|[アクセス拒否アシスタンスを計画します。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)<br /><br />-   [アクセス拒否アシスタンスのモデルを決定します。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.1)<br />-   [特定のアクセス要求を処理する必要があります。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_12)<br />-   [アクセス拒否アシスタンス メッセージをカスタマイズします。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_13)<br />-   [例外を計画します。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.4)<br />-   [どのアクセス拒否アシスタンスの決定が展開されています。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.5)|[アクセス拒否アシスタンスを展開&#40;デモンストレーション手順&#41;](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md)||  
|**シナリオ:Office ドキュメントに対する分類ベースの暗号化**<br /><br />機密情報を保護する主な目的は組織のリスクを低減することです。 HIPAA や Payment Card Industry Data Security Standard (PCI-DSS) などのさまざまなコンプライアンス規定が情報の暗号化を義務付けており、その他にも数多くのビジネス上の理由で機密情報が暗号化されています。 一方、情報の暗号化は高コストであるだけでなく、ビジネスの生産性を低下させる原因にもなります。 このためさまざまな組織がさまざまなアプローチを採用して、暗号化する情報に優先順位を設定しています。 <br />このシナリオをサポートするためには、Windows Server 2012 は、分類に基づいて、機密性の高い Windows Office ファイルを自動的に暗号化する機能を提供します。 これはファイル管理タスクを通じて実行されます。ファイル管理タスクは、ファイル サーバー上のファイルを機密性が高いと認識した数秒後に Active Directory Rights Management サーバー (AD RMS) 保護を起動します。|[シナリオ:Office ドキュメントに対する分類ベースの暗号化](Scenario--Classification-Based-Encryption-for-Office-Documents.md)|[ドキュメントの分類ベースの暗号化を展開する計画](assetId:///14714ba6-d6a2-45e4-aae5-d3318817e52a)|[Office ファイルの暗号化を適用する&#40;デモンストレーション手順&#41;](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md)||  
|**シナリオ:分類を使用して、データを取得します。**<br /><br />データおよび記憶域リソースへの依存は、ほとんどの組織で重要度を増し続けています。 IT 管理者は、従来よりも大規模かつ複雑な記憶域インフラストラクチャを監視しながら総保有コストを妥当な水準に保つ責任を負うという、難しさを増す課題に直面しています。 記憶域リソースの管理はデータのボリュームや可用性だけに関することではなくなり、企業のポリシーを適用し、記憶域の消費用途を知ることで、効率的な使用率とリスク軽減のためのコンプライアンスを実現することも含まれるようになりました。 ファイル分類インフラストラクチャは、データを効率よく管理できるように分類プロセスを自動化することによって、データの性質を理解できるようにします。 ファイル分類インフラストラクチャでは、手動、プログラム、自動の 3 つの分類方法を使用できます。 このシナリオでは自動ファイル分類方法について扱います。|[シナリオ:分類を使用して、データを取得します。](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)|[自動ファイル分類を計画します。](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)|[自動ファイル分類を展開&#40;デモンストレーション手順&#41;](Deploy-Automatic-File-Classification--Demonstration-Steps-.md)||  
|**シナリオ:ファイル サーバー上の情報の保持を実装します。**<br /><br />保持期間とは、ドキュメントの有効期限が切れるまでに保存される時間の長さです。 組織によって、保持期間が異なる場合があります。 フォルダー内のファイルを、短い保持期間のファイル、中間の保持期間のファイル、または長い保持期間のファイルとして分類し、それぞれの期間に対して期限を割り当てることができます。 訴訟ホールドにすることでファイルを無期限に保持することもできます。 <br />ファイル分類インフラストラクチャおよびファイル サーバー リソース マネージャーは、ファイル管理タスクおよびファイル分類を使用して一連のファイルに保持期間を適用します。 フォルダーに保持期間を割り当てた後にファイル管理タスクを使用することで、割り当てられた保持期間をいつまで適用するかを構成できます。 フォルダー内のファイルの有効期限が切れそうになると、ファイルの所有者に電子メールによる通知が届きます。 ファイルを訴訟ホールドとして分類し、ファイル管理タスクでファイルの有効期限が切れないように設定できます。|[シナリオ:ファイル サーバー上の情報の保持を実装します。](Scenario--Implement-Retention-of-Information-on-File-Servers.md)|[ファイル サーバー上の情報の保有期間を計画します。](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)|[ファイル サーバー上の情報の保持を実装するデプロイ&#40;デモンストレーション手順&#41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md)||  
  
> [!NOTE]  
> ダイナミック アクセス制御は ReFS (Resilient File System) ではサポートされません。  
  
## <a name="BKMK_LINKS"></a>参照してください。  
  
|コンテンツの種類|参考資料|  
|----------------|--------------|  
|**製品評価**|-   [ダイナミック アクセス制御のレビューアーズ ガイド](https://go.microsoft.com/fwlink/?LinkId=244309)<br />-   [ダイナミック アクセス制御の開発者ガイド](https://go.microsoft.com/fwlink/?LinkId=245870)|  
|**計画**|-   [集約型アクセス ポリシーの展開の計画](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<br />-   [計画ファイル アクセスの監査](Plan-for-File-Access-Auditing.md)|  
|**展開**|-   [Active Directory のデプロイ](https://go.microsoft.com/fwlink/p/?LinkID=238318)<br />-   [ファイル サービスおよび記憶域サービスの展開](https://go.microsoft.com/fwlink/?LinkID=24430)|  
|**運用**|[ダイナミック アクセス制御 PowerShell リファレンス](https://go.microsoft.com/fwlink/?LinkId=243150)|  
|**ツールと設定**|[Data Classification Toolkit](https://go.microsoft.com/fwlink/?LinkID=244300)|  
|**コミュニティ リソース**|[ディレクトリ サービス フォーラム](https://social.technet.microsoft.com/Forums/winserverDS/threads)|  
  


