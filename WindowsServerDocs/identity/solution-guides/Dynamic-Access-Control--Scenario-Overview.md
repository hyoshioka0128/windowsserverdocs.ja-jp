---
ms.assetid: 7b22adfa-298d-413c-88d0-1231825b7d4d
title: "ダイナミック アクセス制御シナリオの概要"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f70bd138a16b23f1fbf7bfabc98ee184e3b9ab37
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="dynamic-access-control-scenario-overview"></a>ダイナミック アクセス制御: シナリオの概要

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server 2012 のファイル サーバー全体で情報にアクセスできるユーザーを制御し、監査情報へのアクセスがユーザー データ ガバナンスを適用できます。 ダイナミック アクセス制御を使用することができます。  
  
-   ファイルの自動および手動の分類を使用してデータを識別します。 たとえば、ファイル サーバーでデータをタグ付け、組織全体にわたってする可能性があります。  
  
-   集約型アクセス ポリシーを使用するセーフティ ネット ポリシーを適用することで、ファイルへのアクセスを制御します。 たとえば、組織内での正常性情報にアクセスできるユーザーを定義する可能性があります。  
  
-   コンプライアンス レポートや法的分析のための集約型の監査ポリシーを使用してファイルへのアクセスを監査します。 たとえば、機密性の高い情報にアクセスしたユーザーを識別する可能性があります。  
  
-   機密性の高い Microsoft Office ドキュメントを自動的に RMS 暗号化を使用して、Rights Management Services (RMS) 保護を適用します。 たとえば、医療保険の携行性と責任に関する法律 (HIPAA) の情報が含まれているすべてのドキュメントを暗号化する RMS を構成できます。  
  
ダイナミック アクセス制御機能セットはパートナーによってさらに使用されると、基幹業務アプリケーションのことができるインフラストラクチャへの投資に基づいており、機能は、Active Directory を使用する組織にとって大きな価値を提供できます。 このインフラストラクチャが含まれます。  
  
-   条件式と集約型ポリシーが処理できる Windows の新しい承認および監査エンジンです。  
  
-   ユーザーの信頼性情報とデバイスの信頼性情報の Kerberos 認証のサポート。  
  
-   ファイル分類インフラストラクチャ (FCI) の機能強化。  
  
-   RMS の拡張は、パートナーがマイクロソフト以外のファイルを暗号化するソリューションを提供できるようにサポートします。  
  
## <a name="in-this-scenario"></a>このシナリオでは  
次のようなシナリオおよびガイダンスはこのコンテンツ セットの一部として含まれています。  
  
## <a name="BKMK_APP"></a>ダイナミック アクセス制御: コンテンツ ロードマップ  
  
|シナリオ|評価|計画|展開|動作|  
|------------|------------|--------|----------|-----------|  
|**シナリオ: 集約型アクセス ポリシー**<br /><br />ファイルを使用して一元的に展開して管理ユーザーの信頼性情報、デバイスの信頼性情報、およびリソース プロパティを使用して、条件式を含む承認ポリシーを組織には、集約型アクセス ポリシーを作成します。 これらのポリシーはコンプライアンスおよびビジネスの規制要件に基づいています。 これらのポリシーが作成され、ため、容易に管理および展開の Active Directory でホストされています。<br /><br />**フォレスト間にわたる信頼性情報の展開**<br /><br />Windows Server 2012 の AD DS は各フォレスト内に「信頼性情報ディクショナリ」を保持し、フォレスト内で使用中の種類が Active Directory フォレスト レベルで定義されているすべての信頼性情報します。 プリンシパルが信頼の境界を通過する必要があります多くのシナリオがあります。 このシナリオでは、信頼性情報が信頼の境界を走査する方法について説明します。|[ダイナミック アクセス制御: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)<br /><br />[フォレスト間にわたる要求を展開します。](Deploy-Claims-Across-Forests.md)|[計画: 集約型アクセス ポリシーの展開](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<br /><br />-   [ビジネス要求を集約型アクセス ポリシーにマップするプロセス](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_1)<br />-   [ダイナミック アクセス制御の管理の委任](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.1)<br />-   [集約型アクセス ポリシーの計画の例外メカニズム](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.2)<br /><br />ユーザーの信頼性情報の使用に関するベスト プラクティス<br /><br />-   [ユーザー ドメインで信頼性情報を有効にするに適した構成を選択します。](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DC_OP3)<br />-   [ユーザーの信頼性情報を有効にする操作](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.4.2)<br />-   [ファイル サーバー内のユーザーの信頼性情報の使用に関する考慮事項集約型アクセス ポリシーを使用せず随意 Acl](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_5)<br /><br />[デバイスの信頼性情報とデバイスのセキュリティ グループを使用してください。](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DeviceClaims)<br /><br />-   [静的デバイスの信頼性情報の使用に関する考慮事項](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.1)<br />-   [デバイスの信頼性情報を有効にする操作](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.3)<br /><br />展開用ツール<br /><br />-   [Data Classification Toolkit](https://go.microsoft.com/fwlink/?LinkId=%20244300)|[展開の集約型アクセス ポリシー (&) #40; デモンストレーション手順 & #41 です。](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)<br /><br />[フォレスト (&) #40; デモンストレーション手順 & #41 です。全体の信頼性情報を展開します。](Deploy-Claims-Across-Forests--Demonstration-Steps-.md)|-集約型アクセス ポリシーのモデリング|  
|**シナリオ: ファイル アクセスの監査**<br /><br />セキュリティ監査は、企業のセキュリティを維持するための最も強力なツールの 1 つです。 セキュリティ監査の重要な目標の 1 つは、コンプライアンス遵守です。 たとえば、Sarbanes Oxley、HIPAA、および Payment Card Industry (PCI) などの業界標準では、準拠を企業にデータのセキュリティとプライバシーに関連するルールの厳密なセットが必要です。 セキュリティ監査のヘルプのようなポリシーの有無を確立します。これにより、準拠や非準拠では、これらの基準が証明されます。 さらに、セキュリティ監査は変則的な動作の検出を特定し、セキュリティ ポリシーで、実際の格差の軽減を支援し、法的分析に使用できるユーザー アクティビティのレコードを作成することで責任を問わ動作を阻止します。|[シナリオ: ファイル アクセスの監査](Scenario--File-Access-Auditing.md)|[計画ファイル アクセスの監査](Plan-for-File-Access-Auditing.md)|[展開のセキュリティの監査と集約型の監査ポリシー (&) #40; デモンストレーション手順 & #41 です。](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md)|-   [ファイル サーバーに適用される集約型アクセス ポリシーを監視します。](https://technet.microsoft.com/library/jj574188.aspx)<br />-   [ファイルとフォルダーに関連付けられている集約型アクセス ポリシーを監視します。](https://technet.microsoft.com/library/jj574198.aspx)<br />-   [ファイルとフォルダーのリソース属性を監視します。](https://technet.microsoft.com/library/jj574208.aspx)<br />-   [要求の種類のモニタ](https://technet.microsoft.com/library/jj574086.aspx)<br />-   [サインイン時にユーザーとデバイスの信頼性情報を監視します。](https://technet.microsoft.com/library/jj574082.aspx)<br />-   [集約型アクセス ポリシーのモニタとルールの定義](https://technet.microsoft.com/library/jj574115.aspx)<br />-   [監視リソース属性の定義](https://technet.microsoft.com/library/jj574155.aspx)<br />-   [リムーバブル記憶装置の使用状況の監視](https://technet.microsoft.com/library/jj574128.aspx)します。|  
|**シナリオ: アクセス拒否アシスタンス**<br /><br />現在、ユーザーがリモート ファイル サーバーのファイルにアクセスしようとすると、アクセスが拒否されたことを取得するだけが示されますがいます。 これには、ヘルプ デスクへの要求が生成されますか問題が何かを理解する必要がある IT 管理者と管理者の多くの場合、問題を解決するが難しくなるハード時間ユーザーから適切なコンテキストを取得します。 <br />サポートするためのアクセスの拒否 IT を取得する前に問題に対処するインフォメーション ワーカーおよびビジネス オーナー データの目標は、Windows Server 2012、関連してタイミングに IT が関与する、すばやく解決に関する適切なすべての情報を提供します。 この目標を達成するうえで課題の 1 つはアクセスが拒否された対処するための集約型の方法はありませんしとは異なる方法ですべてのアプリケーションに対して、したがって、Windows Server 2012 で、目標の 1 つは、Windows エクスプ ローラーのアクセス拒否エクスペリエンスを向上させる。|[シナリオ: アクセス拒否アシスタンス](Scenario--Access-Denied-Assistance.md)|[アクセス拒否アシスタンスを計画します。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)<br /><br />-   [アクセス拒否アシスタンスのモデルを決定します。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.1)<br />-   [アクセス要求を処理する必要がありますを決定します。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_12)<br />-   [アクセス拒否アシスタンス メッセージをカスタマイズします。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_13)<br />-   [例外を計画します。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.4)<br />-   [どのアクセス拒否アシスタンスの決定が展開されています。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.5)|[アクセス拒否アシスタンス (&) #40; デモンストレーション手順 & #41; を展開します。](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md)||  
|**Office ドキュメントに対する分類ベースの暗号化をシナリオ:**<br /><br />機密情報の保護を主な目的は、組織のリスクを軽減します。 HIPAA や Payment Card Industry Data Security Standard (PCI-DSS) などのさまざまなコンプライアンス規定が情報の暗号化を義務付けており、ビジネス上の機密情報を暗号化するさまざまなビジネス上の理由があるいます。 ただし、情報の暗号化は高コストで、ビジネスの生産性が低下する可能性があります。 このため、組織は、いくつかの方法と、情報を暗号化するための優先順位を持つ傾向があります。 <br />このシナリオをサポートするには、Windows Server 2012 には、機密性の高い Windows Office ファイルを分類に基づいて自動で暗号化する機能が用意されています。 これは、機密性の高いドキュメントの Active Directory Rights Management サーバー (AD RMS) 保護は、ファイル サーバー上のファイルを機密性が高いと認識した後、数秒起動ファイル管理タスクを通じて実行されます。|[Office ドキュメントに対する分類ベースの暗号化をシナリオ:](Scenario--Classification-Based-Encryption-for-Office-Documents.md)|[ドキュメントの分類ベースの暗号化用の展開を計画します。](assetId:///14714ba6-d6a2-45e4-aae5-d3318817e52a)|[展開の暗号化の Office ファイル (&) #40; デモンストレーション手順 & #41 です。](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md)||  
|**シナリオ: 分類を使用して、データに関する洞察を取得します。**<br /><br />データおよび記憶域リソースへの依存をでほとんどの組織の重要度を増し続けています。 IT 管理者課題に直面して拡大の妥当な水準に保つ、難しさ総保有コストを確認する責任が中よりも大規模かつ複雑な記憶域インフラストラクチャを監視します。 記憶域リソースの管理がほぼボリュームや可用性されなくなりますが、データが、会社のポリシーとを効率的な使用率とリスクを軽減するためにコンプライアンスが有効にするストレージの使用状況を把握の強制について ファイル分類インフラストラクチャは、お客様のデータをより効率的に管理できるように分類プロセスを自動化することによって、データに関する洞察を提供します。 次の分類方法は、ファイル分類インフラストラクチャで利用可能な: 手動、プログラム、および自動します。 このシナリオでは、自動ファイル分類方法について説明します。|[シナリオ: 分類を使用して、データに関する洞察を取得します。](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)|[自動ファイル分類を計画します。](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)|[展開の自動ファイル分類 (&) #40; デモンストレーション手順 & #41 です。](Deploy-Automatic-File-Classification--Demonstration-Steps-.md)||  
|**シナリオ: ファイル サーバー上の情報の保持を実装します。**<br /><br />保有期間がドキュメントをする必要があります時間期限が切れるまでに保存します。 組織によっては、保有期間が異なるできます。 短い、中、または長い保持期間を持つものとしてフォルダーにファイルを分類し、それぞれの期間に対して、期限を割り当てることができます。 訴訟ホールド上に配置して、ファイルを無期限に保持することがあります。 <br />ファイル分類インフラストラクチャおよびファイル サーバー リソース マネージャーは、一連のファイルの保存期間を適用するのにファイル管理タスクおよびファイル分類を使用します。 フォルダーの保持期間を割り当てたし、最後に、割り当てられた保持期間は、どのくらいの期間を構成するファイル管理タスクを使用できます。 フォルダー内のファイルが切れそうになると、ファイルの所有者は電子メールによる通知を取得します。 また、できるように、ファイル管理タスクがファイル有効期限はありません、訴訟ホールドにすると、ファイルを分類できます。|[シナリオ: ファイル サーバー上の情報の保持を実装します。](Scenario--Implement-Retention-of-Information-on-File-Servers.md)|[ファイル サーバー上の情報の保持を計画します。](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)|[展開の情報の保持を実装するのには、ファイル サーバー (&) #40; デモンストレーション手順 & #41 です。](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md)||  
  
> [!NOTE]  
> ダイナミック アクセス制御は ReFS (Resilient File System) でサポートされていません。  
  
## <a name="BKMK_LINKS"></a>参照してください。  
  
|コンテンツの種類|参照|  
|----------------|--------------|  
|**製品評価**|-   [ダイナミック アクセス制御レビュアーズ ガイドに関するページ](https://go.microsoft.com/fwlink/?LinkId=244309)<br />-   [ダイナミック アクセス制御の開発者向けガイダンスに関するページ](https://go.microsoft.com/fwlink/?LinkId=245870)|  
|**計画**|-   [集約型アクセス ポリシーの展開の計画](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<br />-   [計画ファイル アクセスの監査](Plan-for-File-Access-Auditing.md)|  
|**展開**|-   [Active Directory の展開](https://go.microsoft.com/fwlink/p/?LinkID=238318)<br />-   [ファイル サービスおよび記憶域サービスの展開](https://go.microsoft.com/fwlink/?LinkID=24430)|  
|**操作**|[ダイナミック アクセス制御 PowerShell リファレンス](https://go.microsoft.com/fwlink/?LinkId=243150)|  
|**ツールと設定**|[Data Classification Toolkit](https://go.microsoft.com/fwlink/?LinkID=244300)|  
|**コミュニティ リソース**|[ディレクトリ サービス フォーラム](https://social.technet.microsoft.com/Forums/winserverDS/threads)|  
  


