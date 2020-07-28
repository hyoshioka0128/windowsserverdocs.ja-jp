---
ms.assetid: 7b22adfa-298d-413c-88d0-1231825b7d4d
title: 'ダイナミック アクセス制御: シナリオの概要'
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 4d39ee3053133286c07a93d18b5c3bd5809e3b54
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182398"
---
# <a name="dynamic-access-control-scenario-overview"></a>ダイナミック アクセス制御:シナリオの概要

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

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

## <a name="dynamic-access-control-content-roadmap"></a><a name="BKMK_APP"></a>ダイナミック アクセス制御: コンテンツ ロードマップ

|シナリオ|Evaluate|プラン|配置|動作|
|------------|------------|--------|----------|-----------|
|**シナリオ: 集約型アクセス ポリシー**<p>ファイルの集約型アクセス ポリシーを作成すると、組織は、ユーザーの信頼性情報、デバイスの信頼性情報、およびリソース プロパティを使用した条件式を含む承認ポリシーを一元的に展開および管理できるようになります。 集約型アクセス ポリシーは、コンプライアンス上およびビジネス上の法的要件に基づきます。 また、Active Directory 内で作成およびホストされるため、容易に管理および展開できます。<p>**フォレスト間にわたる信頼性情報の展開**<p>Windows Server 2012 では、AD DS が各フォレストで "要求ディクショナリ" を保持し、フォレスト内で使用されているすべての要求の種類が Active Directory フォレストレベルで定義されています。 プリンシパルが信頼の境界を越える必要があるシナリオは多数あります。 このシナリオでは信頼性情報が信頼の境界を越える方法について説明します。|[ダイナミック アクセス制御: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)<p>[フォレスト間にわたる要求の展開](Deploy-Claims-Across-Forests.md)|[計画: 集約型アクセスポリシーの展開](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<p>-   [ビジネス要求を集約型アクセスポリシーにマップするプロセス](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_1)<br />-   [動的 Access Control の管理の委任](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.1)<br />-   [集約型アクセスポリシーを計画するための例外メカニズム](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.2)<p>ユーザーの信頼性情報を使う場合のベスト プラクティス<p>-   [ユーザードメインでの要求を有効にする適切構成の選択](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DC_OP3)<br />-   [ユーザーの要求を有効にする操作](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.4.2)<br />-   [ファイルサーバーの随意 Acl で集約型アクセスポリシーを使用せずにユーザー要求を使用する場合の考慮事項](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_5)<p>[デバイスの信頼性情報とデバイスのセキュリティ グループの使用](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DeviceClaims)<p>-   [静的デバイスの信頼性情報の使用に関する考慮事項](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.1)<br />-   [デバイスの信頼性情報を有効にする操作](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.3)<p>展開用ツール<p>-   [データ分類ツールキット](https://go.microsoft.com/fwlink/?LinkId=%20244300)|[集約型アクセスポリシー &#40;デモンストレーション手順をデプロイする&#41;](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)<p>[フォレスト間での要求の展開 &#40;デモンストレーションの手順&#41;](Deploy-Claims-Across-Forests--Demonstration-Steps-.md)|-集約型アクセスポリシーのモデリング|
|**シナリオ: ファイル アクセスの監査**<p>セキュリティ監査は、企業のセキュリティ維持の最も強力なサポート手段の 1 つです。 セキュリティ監査の重要な目標の 1 つがコンプライアンス遵守です。 たとえば、Sarbanes Oxley、HIPAA、および Payment Card Industry (PCI) などの業界標準は、データ セキュリティとプライバシーに関する厳格なルール セットへの準拠を企業に要求します。 セキュリティ監査によってこれらのポリシーが存在するかどうかが明確化されます。つまり、監査ポリシーによって各種の標準に準拠しているかどうかが証明されます。 さらにセキュリティ監査は、異常な動作の検出、セキュリティ ポリシー内のギャップの特定と解消、さらに、ユーザー アクティビティの記録を作成し、これを使用して法的分析を実施することで、法的責任を問われる可能性のある動作の防止にも役立ちます。|[シナリオ: ファイル アクセスの監査](Scenario--File-Access-Auditing.md)|[ファイル アクセスの監査の計画](Plan-for-File-Access-Auditing.md)|[全体監査ポリシーを使用してセキュリティ監査を展開する &#40;デモンストレーション手順&#41;](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md)|-   [ファイルサーバーに適用される集約型アクセスポリシーを監視する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574188(v=ws.11))<br />-   [ファイルとフォルダーに関連付けられた集約型アクセスポリシーを監視する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574198(v=ws.11))<br />-   [ファイルとフォルダーのリソース属性の監視](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574208(v=ws.11))<br />-   [要求の種類を監視する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574086(v=ws.11))<br />-   [サインイン時のユーザーとデバイスの信頼性情報の監視](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574082(v=ws.11))<br />-   [集約型アクセスポリシーと規則の定義の監視](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574115(v=ws.11))<br />-   [リソース属性の定義の監視](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574155(v=ws.11))<br />-   [リムーバブル記憶装置の使用を監視](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574128(v=ws.11))します。|
|**シナリオ: アクセス拒否アシスタンス**<p>現在は、ユーザーがファイル サーバー上のリモート ファイルにアクセスを試みた場合、アクセスが拒否されたことだけが示されます。 このことが、問題を特定する必要があるヘルプデスクや IT 管理者への要求を増やしています。また、管理者がユーザーから適切なコンテキストを得るのが難しい場合が多いということが、この問題の解決を難しくしています。 <br />Windows Server 2012 では、データのインフォメーションワーカーおよびビジネスオーナーが、関与する前にアクセス拒否の問題を処理し、関連するときに、迅速な解決に必要なすべての情報を提供することを目的としています。 この目標を達成するうえでの課題の1つは、アクセス拒否を処理する一元的な方法がなく、すべてのアプリケーションが異なる方法で対処することです。そのため、windows Server 2012 では、Windows Explorer のアクセス拒否エクスペリエンスを向上させることが目的の1つです。|[シナリオ: アクセス拒否アシスタンス](Scenario--Access-Denied-Assistance.md)|[アクセス拒否アシスタンスの計画](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)<p>-   [アクセス拒否アシスタンスモデルの決定](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.1)<br />-   [アクセス要求を処理するユーザーを決定する](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_12)<br />-   [アクセス拒否アシスタンスのメッセージをカスタマイズする](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_13)<br />-   [例外の計画](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.4)<br />-   [アクセス拒否アシスタンスの展開方法を決定する](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.5)|[アクセス拒否アシスタンスのデプロイ &#40;デモンストレーション手順&#41;](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md)||
|**シナリオ: Office ドキュメントに対する分類ベースの暗号化**<p>機密情報を保護する主な目的は組織のリスクを低減することです。 HIPAA や Payment Card Industry Data Security Standard (PCI-DSS) などのさまざまなコンプライアンス規定が情報の暗号化を義務付けており、その他にも数多くのビジネス上の理由で機密情報が暗号化されています。 一方、情報の暗号化は高コストであるだけでなく、ビジネスの生産性を低下させる原因にもなります。 このためさまざまな組織がさまざまなアプローチを採用して、暗号化する情報に優先順位を設定しています。 <br />このシナリオをサポートするために、Windows Server 2012 では、機密性の高い Windows Office ファイルを分類に基づいて自動的に暗号化する機能が用意されています。 これはファイル管理タスクを通じて実行されます。ファイル管理タスクは、ファイル サーバー上のファイルを機密性が高いと認識した数秒後に Active Directory Rights Management サーバー (AD RMS) 保護を起動します。|[シナリオ: Office ドキュメントに対する分類ベースの暗号化](Scenario--Classification-Based-Encryption-for-Office-Documents.md)|[ドキュメントに対する分類ベースの暗号化の展開計画](assetId:///14714ba6-d6a2-45e4-aae5-d3318817e52a)|[デモンストレーション手順 &#40;の Office ファイルの暗号化を展開する&#41;](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md)||
|**シナリオ: 分類を使用してデータの情報を得る**<p>データおよび記憶域リソースへの依存は、ほとんどの組織で重要度を増し続けています。 IT 管理者は、従来よりも大規模かつ複雑な記憶域インフラストラクチャを監視しながら総保有コストを妥当な水準に保つ責任を負うという、難しさを増す課題に直面しています。 記憶域リソースの管理はデータのボリュームや可用性だけに関することではなくなり、企業のポリシーを適用し、記憶域の消費用途を知ることで、効率的な使用率とリスク軽減のためのコンプライアンスを実現することも含まれるようになりました。 ファイル分類インフラストラクチャは、データを効率よく管理できるように分類プロセスを自動化することによって、データの性質を理解できるようにします。 ファイル分類インフラストラクチャでは、手動、プログラム、自動の 3 つの分類方法を使用できます。 このシナリオでは自動ファイル分類方法について扱います。|[シナリオ: 分類を使用してデータの情報を得る](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)|[自動ファイル分類の計画](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)|[デモンストレーションの手順を &#40;自動ファイル分類をデプロイする&#41;](Deploy-Automatic-File-Classification--Demonstration-Steps-.md)||
|**シナリオ: ファイル サーバーでの情報の保持の実装**<p>保持期間とは、ドキュメントの有効期限が切れるまでに保存される時間の長さです。 組織によって、保持期間が異なる場合があります。 フォルダー内のファイルを、短い保持期間のファイル、中間の保持期間のファイル、または長い保持期間のファイルとして分類し、それぞれの期間に対して期限を割り当てることができます。 訴訟ホールドにすることでファイルを無期限に保持することもできます。 <br />ファイル分類インフラストラクチャおよびファイル サーバー リソース マネージャーは、ファイル管理タスクおよびファイル分類を使用して一連のファイルに保持期間を適用します。 フォルダーに保持期間を割り当てた後にファイル管理タスクを使用することで、割り当てられた保持期間をいつまで適用するかを構成できます。 フォルダー内のファイルの有効期限が切れそうになると、ファイルの所有者に電子メールによる通知が届きます。 ファイルを訴訟ホールドとして分類し、ファイル管理タスクでファイルの有効期限が切れないように設定できます。|[シナリオ: ファイル サーバーでの情報の保持の実装](Scenario--Implement-Retention-of-Information-on-File-Servers.md)|[ファイル サーバーでの情報の保持の計画](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)|[ファイルサーバーでの情報の保持の実装を展開する &#40;デモンストレーションの手順&#41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md)||

> [!NOTE]
> ダイナミック アクセス制御は ReFS (Resilient File System) ではサポートされません。

## <a name="see-also"></a>関連項目

|コンテンツ タイプ|参考資料|
|----------------|--------------|
|**製品評価**|- [動的 Access Control レビュー担当者ガイド](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc732148(v=ws.10))<br>- [動的 Access Control 開発者向けガイダンス](https://docs.microsoft.com/previous-versions/windows/desktop/dacx/dynamic-access-control-developer-extensibility-roadmap)|
|**計画**|- [集約型アクセスポリシーの展開の計画](https://docs.microsoft.com/windows-server/identity/solution-guides/scenario--central-access-policy)<br>- [ファイルアクセスの監査の計画](Plan-for-File-Access-Auditing.md)|
|**配置**|- [Active Directory の展開](https://docs.microsoft.com/windows-server/identity/ad-ds/deploy/ad-ds-deployment)<br>- [ファイルサービスおよび記憶域サービスの展開](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831487(v=ws.11))|
|**操作**|[ダイナミック アクセス制御 PowerShell リファレンスに関するページ](https://docs.microsoft.com/powershell/module/addsadministration/?view=win10-ps)|
|**ツールと設定**|[Data Classification Toolkit に関するページ](https://www.microsoft.com/download/details.aspx?id=27123)|
|**コミュニティ リソース**|[ディレクトリ サービス フォーラムに関するページ](https://docs.microsoft.com/answers/topics/windows-active-directory.html)|
