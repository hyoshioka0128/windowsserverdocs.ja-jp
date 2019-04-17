---
ms.assetid: 846c3680-b321-47da-8302-18472be42421
title: "要求の展開 (デモンストレーション手順) のフォレスト間で"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3bab7a396061ecae8a187cc6986d6d026a9e4b32
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-claims-across-forests-demonstration-steps"></a>要求の展開 (デモンストレーション手順) のフォレスト間で

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックの「が、信頼されていると、信頼される側のフォレスト間で信頼性情報変換を構成する方法を説明する基本的なシナリオについて説明します。 信頼性情報変換ポリシー オブジェクトを作成および信頼する側のフォレストと信頼される側のフォレストの信頼にリンクされている方法を学習します。 シナリオでは、し、検証します。  
  
## <a name="scenario-overview"></a>シナリオの概要  
Adatum Corporation provides financial services to Contoso, Ltd. Each quarter, Adatum accountants copy their account spreadsheets to a folder on a file server located at Contoso, Ltd. There is a two-way trust set up from Contoso to Adatum. Contoso, Ltd. wants to protect the share so that only Adatum employees can access the remote share.  
  
: このシナリオでは  
  
1.  [前提条件と、テスト環境をセットアップします。](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_1.1)  
  
2.  [信頼されたフォレスト (Adatum) で信頼性情報変換のセットアップします。](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_3)  
  
3.  [(Contoso) 信頼する側のフォレストで信頼性情報変換のセットアップします。](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_4)  
  
4.  [シナリオを検証します。](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_5)  
  
## <a name="BKMK_1.1"></a>前提条件と、テスト環境をセットアップします。  
テスト構成には、2 つのフォレストの設定が含まれます: Adatum Corporation と Contoso, Ltd と Contoso および Adatum 間に双方向信頼関係が発生します。 "adatum.com"信頼されたフォレストは、"contoso.com"信頼する側のフォレストです。  
  
信頼性情報変換のシナリオでは、信頼される側のフォレストに信頼する側のフォレスト内の要求への要求の変換について説明します。 これを行うには、adatum.com と呼ばれる新しいフォレストを設定し、'Adatum' の会社の値を持つテスト ユーザーのフォレストを設定する必要があります。 contoso.com と adatum.com 間で双方向信頼関係をセットアップする必要があります。  
  
> [!IMPORTANT]  
> Contoso および Adatum フォレストをセットアップするときに、両方のルート ドメインが Windows Server 2012 ドメインの機能レベルの信頼性情報変換が機能することを確認する必要があります。  
  
ラボは、次を設定する必要があります。 これらの手順の詳細に説明されている[付録 b: 設定をテスト環境](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
このシナリオでは、ラボを設定する次の手順を実行する必要があります。  
  
1.  [Contoso に信頼される側のフォレストとして Adatum を設定します。](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
2.  [Contoso で '会社' 要求の種類を作成します。](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.8)  
  
3.  [Contoso で「会社」リソース プロパティを有効にします。](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.55)  
  
4.  [集約型アクセス規則を作成します。](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.9)  
  
5.  [集約型アクセス ポリシーを作成します。](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.10)  
  
6.  [グループ ポリシーによって新しいポリシーを公開します](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.11)  
  
7.  [ファイル サーバーで Earnings フォルダーを作成します。](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.12)  
  
8.  [分類を設定し、新しいフォルダーで集約型アクセス ポリシーを適用](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.13)  
  
このシナリオを完了するのにには、次の情報を使用します。  
  
|オブジェクト|詳細|  
|-----------|-----------|  
|ユーザー|Jeff Low、Contoso|  
|Adatum と Contoso でユーザーの信頼性情報|ID: ad:/電話番号の内線/会社: ContosoAdatum<br /><br />ソース属性: 企業<br /><br />推奨値: Contoso、Adatum**重要:**必要があります ID を設定する「会社」の要求の種類両方 Contoso および Adatum 要求変換の同じにするためにします。|  
|Contoso で集約型アクセス規則|AdatumEmployeeAccessRule|  
|Contoso の集約型アクセス ポリシー|Adatum 専用アクセス ポリシー|  
|Adatum と Contoso で信頼性情報変換ポリシー|DenyAllExcept 会社|  
|Contoso でファイル フォルダー|D:\EARNINGS|  
  
## <a name="BKMK_3"></a>信頼されたフォレスト (Adatum) で信頼性情報変換のセットアップします。  
この手順では、Contoso に渡す「会社」を除くすべての要求を拒否する Adatum で変換ポリシーを作成します。  
  
Windows PowerShell 用 Active Directory モジュールを提供、**DenyAllExcept**変換ポリシーで指定された要求を除くすべての速度が低下する引数です。  
  
要求変換をセットアップするには、信頼性情報変換ポリシーを作成し、信頼されたおよび信頼する側のフォレスト間にリンクする必要があります。  
  
### <a name="BKMK_2.2"></a>Adatum に信頼性情報変換ポリシーを作成します。  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-claims-except-company"></a>[会社名] を除くすべての要求を拒否する Adatum 変換ポリシーを作成するには  
  
1.  ドメイン コントローラーに、パスワードを持つ管理者として adatum.com ログイン**pass@word1**します。  
  
2.  Windows PowerShell で管理者特権のコマンド プロンプトを開きし、次のように入力します。  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except Company"`  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"adatum.com" `  
  
    ```  
  
### <a name="BKMK_2.3"></a>Adatum の信頼関係ドメイン オブジェクトに信頼性情報変換リンクを設定します。  
この手順で Contoso の Adatum の信頼関係ドメイン オブジェクトで、新しく作成した信頼性情報変換ポリシーを適用します。  
  
##### <a name="to-apply-the-claims-transformation-policy"></a>信頼性情報変換ポリシーを適用するには  
  
1.  ドメイン コントローラーに、パスワードを持つ管理者として adatum.com ログイン**pass@word1**します。  
  
2.  Windows PowerShell で管理者特権のコマンド プロンプトを開きし、次のように入力します。  
  
    ```  
  
      Set-ADClaimTransformLink `  
    -Identity:"contoso.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    '"TrustRole:Trusted `  
  
    ```  
  
## <a name="BKMK_4"></a>(Contoso) 信頼する側のフォレストで信頼性情報変換のセットアップします。  
この手順では [会社名] を除くすべての要求を拒否する Contoso (信頼する側のフォレスト) で信頼性情報変換ポリシーを作成します。 信頼性情報変換ポリシーを作成し、フォレストの信頼にリンクする必要があります。  
  
### <a name="BKMK_4.1"></a>Contoso で信頼性情報変換ポリシーを作成します。  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-except-company"></a>[会社名] を除くすべて拒否する Adatum 変換ポリシーを作成するには  
  
1.  ドメイン コントローラーに、パスワードを持つ管理者として contoso.com ログイン**pass@word1**します。  
  
2.  Windows PowerShell で管理者特権でコマンド プロンプトを開きし、次のように入力します。  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except company" `  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"contoso.com" `  
  
    ```  
  
### <a name="BKMK_4.2"></a>Contoso の信頼関係ドメイン オブジェクトに信頼性情報変換リンクを設定します。  
In this step, you apply the newly created claims transformation policy on the contoso.com trust domain object for Adatum to allow "Company" be passed through to contoso.com. The trust domain object is named adatum.com.  
  
##### <a name="to-set-the-claims-transformation-policy"></a>信頼性情報変換ポリシーを設定するには  
  
1.  ドメイン コントローラーに、パスワードを持つ管理者として contoso.com ログイン**pass@word1**します。  
  
2.  Windows PowerShell で管理者特権でコマンド プロンプトを開きし、次のように入力します。  
  
    ```  
  
      Set-ADClaimTransformLink   
    -Identity:"adatum.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    -TrustRole:Trusting `  
  
    ```  
  
## <a name="BKMK_5"></a>シナリオを検証します。  
この手順でしようとするユーザーが共有フォルダーへのアクセスを持っていることを検証するファイル サーバー FILE1 に設定した D:\EARNINGS フォルダーにアクセスします。  
  
#### <a name="to-ensure-that-the-adatum-user-can-access-the-shared-folder"></a>Adatum ユーザーが共有フォルダーにアクセスできることを確認  
  
1.  クライアント コンピューターのパスワードを使って Jeff Low として CLIENT1 にログイン**pass@word1**します。  
  
2.  フォルダー \\\FILE1.contoso.com\Earnings を参照します。  
  
3.  Jeff Low はフォルダーにアクセスできる必要があります。  
  
## <a name="additional-scenarios-for-claims-transformation-policies"></a>信頼性情報変換ポリシーの追加のシナリオ  
要求変換の他の一般的なケースの一覧を次に示します。  
  
|シナリオ|ポリシー|  
|------------|----------|  
|Contoso Adatum を経由する Adatum から送信されるすべての要求を許可します。|コード- <br />New-ADClaimTransformPolicy \'<br /> -説明:「信頼性情報変換ポリシーすべての要求を許可するように」\'<br />-名前:"AllowAllClaimsPolicy"\'<br />-すべて許可が次 \'<br />サーバー:"contoso.com"\'<br />Set-ADClaimTransformLink \'<br />Id:"adatum.com"\'<br />ポリシー:"AllowAllClaimsPolicy"\'<br />-TrustRole: 信頼する側の \'<br />サーバー:"contoso.com"'|  
|Contoso Adatum を経由する Adatum から送信されるすべての要求を拒否します。|コード- <br />New-ADClaimTransformPolicy \'<br />-説明:「信頼性情報変換ポリシーをすべての要求を拒否する」\'<br />-名前:"DenyAllClaimsPolicy"\'<br /> -DenyAll \'<br />サーバー:"contoso.com"\'<br />Set-ADClaimTransformLink \'<br />Id:"adatum.com"\'<br />ポリシー:"DenyAllClaimsPolicy"\'<br />-TrustRole: 信頼する側の \'<br />サーバー:"contoso.com"'|  
|Contoso Adatum を経由するには、「会社」と「部門」を除く Adatum から送信されるすべての要求を許可します。|コード <br />-New-ADClaimTransformationPolicy \'<br />-説明:「信頼性情報変換ポリシー会社および部門を除くすべての要求を許可するように」\'<br /> -名前:"AllowAllClaimsExceptCompanyAndDepartmentPolicy"\'<br />-AllowAllExcept: 会社、部門 \'<br />サーバー:"contoso.com"\'<br />Set-ADClaimTransformLink \'<br /> Id:"adatum.com"\'<br />ポリシー:"AllowAllClaimsExceptCompanyAndDepartmentPolicy"\'<br /> -TrustRole: 信頼する側の \'<br />サーバー:"contoso.com"'|  
  
## <a name="BKMK_Links"></a>参照してください。  
  
-   For a list of all Windows PowerShell cmdlets that are available for claims transformation, see [Active Directory PowerShell Cmdlet Reference](https://go.microsoft.com/fwlink/?LinkId=243150).  
  
-   For advanced tasks that involve export and import of DAC configuration information between two forests, use the [Dynamic Access Control PowerShell Reference](https://go.microsoft.com/fwlink/?LinkId=243150)  
  
-   [フォレスト間にわたる要求を展開します。](Deploy-Claims-Across-Forests.md)  
  
-   [Claims Transformation Rules Language](Claims-Transformation-Rules-Language.md)  
  
-   [ダイナミック アクセス制御: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  
  

