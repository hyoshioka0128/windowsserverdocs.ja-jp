---
ms.assetid: 846c3680-b321-47da-8302-18472be42421
title: フォレスト間にわたる信頼性情報の展開 (デモンストレーション手順)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3bab7a396061ecae8a187cc6986d6d026a9e4b32
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830353"
---
# <a name="deploy-claims-across-forests-demonstration-steps"></a>フォレスト間にわたる信頼性情報の展開 (デモンストレーション手順)

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、信頼されていると、信頼される側のフォレスト間の要求の変換を構成する方法を説明する基本的なシナリオを取り上げます。 信頼性情報変換ポリシー オブジェクトを作成し、信頼する側のフォレストと信頼されたフォレストの信頼にリンクされている方法を学習します。 シナリオを検証します。  
  
## <a name="scenario-overview"></a>シナリオの概要  
Adatum Corporation では、Contoso, Ltd. の金融サービスContoso, Ltd. にあるファイル サーバー上のフォルダーに、各四半期 Adatum 士のコピーはワークシートのアカウントContoso から Adatum に設定する双方向の信頼があります。 Contoso, Ltd. Adatum 従業員だけが、そのリモート共有にアクセスできるように、共有を保護したいです。  
  
この場合、次の処理が実行されます。  
  
1.  [前提条件と、テスト環境を設定します。](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_1.1)  
  
2.  [信頼されたフォレスト (Adatum) で設定するクレームの変換](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_3)  
  
3.  [信頼する側のフォレスト (Contoso) を設定するクレームの変換](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_4)  
  
4.  [シナリオを検証します。](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_5)  
  
## <a name="BKMK_1.1"></a>前提条件と、テスト環境を設定します。  
テスト構成には、2 つのフォレストの設定が含まれます。Adatum Corporation と Contoso, Ltd と Contoso および Adatum の間で双方向の信頼を持ちます。 "ある adatum.com"が信頼されたフォレストと信頼する側のフォレストは"contoso.com"です。  
  
クレームの変換シナリオでは、信頼されているフォレストを信頼する側のフォレスト内の要求の要求の変換を示します。 これを行うには、adatum.com という新規フォレストを設定して、会社の値 'Adatum' のテスト ユーザーのフォレストを設定する必要があります。 Contoso.com と adatum.com 間の双方向の信頼を設定する必要があるとします。  
  
> [!IMPORTANT]  
> Contoso および Adatum フォレストを設定する場合、両方のルート ドメインが Windows Server 2012 ドメインの機能レベルのクレームの変換動作することを確認する必要があります。  
  
ラボは、次を設定する必要があります。 これらの手順で詳しく説明は[付録 b:テスト環境のセットアップ](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
このシナリオでラボを設定するには、次の手順を実装する必要があります。  
  
1.  [Adatum に信頼されたフォレスト Contoso に設定します。](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
2.  [Contoso に"Company"要求の種類を作成します。](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.8)  
  
3.  [Contoso に"Company"リソース プロパティを有効にします。](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.55)  
  
4.  [集約型アクセス規則を作成します。](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.9)  
  
5.  [集約型アクセス ポリシーを作成します。](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.10)  
  
6.  [グループ ポリシーを使って新しいポリシーを発行します。](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.11)  
  
7.  [ファイル サーバーで Earnings フォルダーを作成します。](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.12)  
  
8.  [分類を設定し、新しいフォルダーで集約型アクセス ポリシーを適用](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.13)  
  
このシナリオを完了するのにには、次の情報を使用します。  
  
|オブジェクト|詳細|  
|-----------|-----------|  
|Users|Jeff Low、Contoso|  
|Adatum と Contoso のユーザーの信頼性情報|ID: ad://ext/Company:ContosoAdatum,<br /><br />基になる属性: 会社<br /><br />提案される値:Contoso, Adatum**重要です。** 両方 Contoso および Adatum クレームの変換を同じにする操作で、"Company"の ID 要求の種類を設定する必要があります。|  
|Contoso の集約型アクセス規則|AdatumEmployeeAccessRule|  
|Contoso の集約型アクセス ポリシー|Adatum 専用アクセス ポリシー|  
|Adatum と Contoso の信頼性情報変換ポリシー|DenyAllExcept 会社|  
|Contoso のファイル フォルダー|D:\EARNINGS|  
  
## <a name="BKMK_3"></a>信頼されたフォレスト (Adatum) で設定するクレームの変換  
この手順では、Contoso に渡す"Company"を除くすべての要求を拒否する Adatum で変換ポリシーを作成します。  
  
Windows PowerShell 用 Active Directory モジュールの提供、 **DenyAllExcept**引数で、変換ポリシーで指定したクレームを除くすべてを削除します。  
  
クレームの変換を設定するには、信頼性情報変換ポリシーを作成し、信頼できる、信頼する側のフォレスト間にリンクする必要があります。  
  
### <a name="BKMK_2.2"></a>Adatum に信頼性情報変換ポリシーを作成します。  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-claims-except-company"></a>"Company"を除くすべての要求を拒否する Adatum 変換ポリシーを作成するには  
  
1.  ドメイン コント ローラー、パスワードを使用して、管理者として adatum.com にサインイン **pass@word1**します。  
  
2.  Windows PowerShell で管理者特権のコマンド プロンプトを開き、次に入力します。  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except Company"`  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"adatum.com" `  
  
    ```  
  
### <a name="BKMK_2.3"></a>Adatum の信頼ドメインのオブジェクトに、要求変換のリンクを設定します。  
この手順では Contoso の Adatum の信頼ドメインのオブジェクトで新しく作成されたクレーム変換ポリシーを適用します。  
  
##### <a name="to-apply-the-claims-transformation-policy"></a>信頼性情報変換ポリシーを適用するには  
  
1.  ドメイン コント ローラー、パスワードを使用して、管理者として adatum.com にサインイン **pass@word1**します。  
  
2.  Windows PowerShell で管理者特権のコマンド プロンプトを開き、次に入力します。  
  
    ```  
  
      Set-ADClaimTransformLink `  
    -Identity:"contoso.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    '"TrustRole:Trusted `  
  
    ```  
  
## <a name="BKMK_4"></a>信頼する側のフォレスト (Contoso) を設定するクレームの変換  
この手順では、'会社です ' を除くすべての要求を拒否する Contoso (信頼する側のフォレスト) での信頼性情報変換ポリシーを作成します。 信頼性情報変換ポリシーを作成し、フォレストの信頼にリンクする必要があります。  
  
### <a name="BKMK_4.1"></a>Contoso で信頼性情報変換ポリシーを作成します。  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-except-company"></a>"Company"を除くすべてを拒否する Adatum 変換ポリシーを作成するには  
  
1.  ドメイン コント ローラー、パスワードを使用して Administrator として contoso.com にサインイン **pass@word1**します。  
  
2.  Windows PowerShell で管理者特権のコマンド プロンプトを開き、次に入力します。  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except company" `  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"contoso.com" `  
  
    ```  
  
### <a name="BKMK_4.2"></a>Contoso 社の信頼ドメインのオブジェクトに、要求変換のリンクを設定します。  
新しく作成された適用では、"Company"を許可する Adatum の contoso.com 信頼ドメイン オブジェクトの信頼性情報変換ポリシー contoso.com に渡されます。 信頼ドメインのオブジェクトは、adatum.com という名前です。  
  
##### <a name="to-set-the-claims-transformation-policy"></a>クレームの変換ポリシーを設定するには  
  
1.  ドメイン コント ローラー、パスワードを使用して Administrator として contoso.com にサインイン **pass@word1**します。  
  
2.  Windows PowerShell で管理者特権のコマンド プロンプトを開き、次に入力します。  
  
    ```  
  
      Set-ADClaimTransformLink   
    -Identity:"adatum.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    -TrustRole:Trusting `  
  
    ```  
  
## <a name="BKMK_5"></a>シナリオを検証します。  
この手順でユーザーが共有フォルダーへのアクセスを持っているかを検証するファイル サーバー FILE1 に設定した D:\EARNINGS フォルダーにアクセスしようとします。  
  
#### <a name="to-ensure-that-the-adatum-user-can-access-the-shared-folder"></a>Adatum ユーザーが共有フォルダーにアクセスできるようにするには  
  
1.  コンピューターのクライアントへのサインイン、Jeff Low をパスワードとして CLIENT1  **pass@word1**します。  
  
2.  フォルダーを参照\\\FILE1.contoso.com\Earnings します。  
  
3.  Jeff Low をフォルダーにアクセスすることがあります。  
  
## <a name="additional-scenarios-for-claims-transformation-policies"></a>信頼性情報変換ポリシーの他のシナリオ  
クレームの変換でその他の一般的なケースの一覧を次に示します。  
  
|シナリオ|ポリシー|  
|------------|----------|  
|Contoso Adatum を経由する Adatum から送信されるすべての要求を許可します。|コード- <br />新しい ADClaimTransformPolicy \`<br /> 説明:「要求の変換ポリシーすべてクレームを許可する」 \`<br />-Name:"AllowAllClaimsPolicy" \`<br />-AllowAll \`<br />-Server:"contoso.com" \`<br />セット ADClaimTransformLink \`<br />-Identity:"adatum.com" \`<br />-Policy:"AllowAllClaimsPolicy" \`<br />-TrustRole:Trusting \`<br />-Server:"contoso.com" `|  
|Contoso Adatum を経由する Adatum から送信されるすべての要求を拒否します。|コード- <br />新しい ADClaimTransformPolicy \`<br />説明:「要求の変換ポリシーすべて要求を拒否する」 \`<br />-Name:"DenyAllClaimsPolicy" \`<br /> -DenyAll \`<br />-Server:"contoso.com" \`<br />セット ADClaimTransformLink \`<br />-Identity:"adatum.com" \`<br />-Policy:"DenyAllClaimsPolicy" \`<br />-TrustRole:Trusting \`<br />-Server:"contoso.com"`|  
|Contoso Adatum を経由するには、"Company"および"Department"を除く Adatum から送信されるすべての要求を許可します。|コード <br />- New-ADClaimTransformationPolicy \`<br />説明:「要求の変換ポリシー会社と部門を除くすべて要求を許可する」 \`<br /> -Name:"AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br />-AllowAllExcept:company,department \`<br />-Server:"contoso.com" \`<br />セット ADClaimTransformLink \`<br /> -Identity:"adatum.com" \`<br />-Policy:"AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br /> -TrustRole:Trusting \`<br />-Server:"contoso.com" `|  
  
## <a name="BKMK_Links"></a>参照してください。  
  
-   クレームの変換に使用できるすべての Windows PowerShell コマンドレットの一覧は、次を参照してください。 [Active Directory PowerShell コマンドレット リファレンス](https://go.microsoft.com/fwlink/?LinkId=243150)します。  
  
-   2 つのフォレストの間での構成情報の DAC のエクスポートおよびインポートに関連する高度なタスクを使用して、[ダイナミック アクセス制御 PowerShell リファレンス](https://go.microsoft.com/fwlink/?LinkId=243150)  
  
-   [フォレスト間にわたる信頼性情報を展開します。](Deploy-Claims-Across-Forests.md)  
  
-   [クレーム変換規則言語](Claims-Transformation-Rules-Language.md)  
  
-   [ダイナミック アクセス制御:シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  
  

