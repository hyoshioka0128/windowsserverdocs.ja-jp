---
ms.assetid: 846c3680-b321-47da-8302-18472be42421
title: フォレスト間にわたる信頼性情報の展開 (デモンストレーション手順)
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 05ca21f343d2ad3db4ce00b53a66b3cd6dd6de16
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861245"
---
# <a name="deploy-claims-across-forests-demonstration-steps"></a>フォレスト間にわたる信頼性情報の展開 (デモンストレーション手順)

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、信頼する側のフォレストと信頼される側のフォレストの間で要求の変換を構成する方法を説明する基本的なシナリオについて説明します。 要求変換ポリシーオブジェクトを作成し、信頼する側のフォレストと信頼される側のフォレストの信頼にリンクする方法について説明します。 次に、シナリオを検証します。  

## <a name="scenario-overview"></a>シナリオの概要  
Adatum Corporation は、Contoso, Ltd. に金融サービスを提供しています。各四半期の Adatum 経理担当者は、アカウントスプレッドシートを Contoso, Ltd. にあるファイルサーバー上のフォルダーにコピーします。Contoso から Adatum への双方向の信頼が設定されています。 Contoso, Ltd. は、Adatum の従業員だけがリモート共有にアクセスできるように、共有を保護したいと考えています。  

この場合、次の処理が実行されます。  

1.  [前提条件とテスト環境を設定する](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_1.1)  

2.  [信頼されているフォレスト (Adatum) で要求変換を設定する](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_3)  

3.  [信頼する側のフォレスト (Contoso) に要求の変換を設定します。](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_4)  

4.  [シナリオを検証する](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_5)  

## <a name="set-up-the-prerequisites-and-the-test-environment"></a><a name="BKMK_1.1"></a>前提条件とテスト環境を設定する  
テスト構成では、Adatum Corporation と Contoso, Ltd. という2つのフォレストを設定し、Contoso と Adatum の間に双方向の信頼関係を持たせます。 "adatum.com" は信頼される側のフォレストで、"contoso.com" は信頼する側のフォレストです。  

要求変換のシナリオでは、信頼されているフォレスト内の要求を信頼する側のフォレストのクレームに変換する方法を示します。 これを行うには、adatum.com という名前の新しいフォレストを設定し、company 値が "Adatum" のテストユーザーをフォレストに設定する必要があります。 次に、contoso.com と adatum.com の間に双方向の信頼を設定する必要があります。  

> [!IMPORTANT]  
> Contoso と Adatum フォレストを設定する場合は、要求変換が機能するように、両方のルートドメインが Windows Server 2012 ドメインの機能レベルであることを確認する必要があります。  

ラボ用に次の設定を行う必要があります。 これらの手順の詳細につい[ては、「付録 B: テスト環境の](Appendix-B--Setting-Up-the-Test-Environment.md)セットアップ」をご覧ください。  

このシナリオのラボを設定するには、次の手順を実装する必要があります。  

1.  [Adatum を信頼されたフォレストとして Contoso に設定する](Appendix-B--Setting-Up-the-Test-Environment.md)  

2.  [Contoso で "Company" 要求の種類を作成する](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.8)  

3.  [Contoso で "Company" リソースプロパティを有効にする](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.55)  

4.  [集約型アクセス規則を作成する](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.9)  

5.  [集約型アクセスポリシーを作成する](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.10)  

6.  [グループポリシーを使用して新しいポリシーを発行する](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.11)  

7.  [ファイルサーバーでの [所得] フォルダーの作成](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.12)  

8.  [分類を設定し、新しいフォルダーに集約型アクセスポリシーを適用する](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.13)  

このシナリオを完了するには、次の情報を使用します。  

|オブジェクト|詳細|  
|-----------|-----------|  
|Users|Jeff 安値、Contoso|  
|Adatum および Contoso でのユーザー要求|ID: ad://ext/Company:ContosoAdatum、<p>ソース属性: company<p>提案される値: Contoso, Adatum**重要:** 要求変換が機能するためには、Contoso と adatum の両方で "Company" 要求の種類の ID を同じに設定する必要があります。|  
|Contoso の集約型アクセス規則|Adatumemployeeaccessrule が|  
|Contoso の集約型アクセスポリシー|Adatum Only アクセスポリシー|  
|Adatum と Contoso の要求変換ポリシー|DenyAllExcept 会社|  
|Contoso のファイルフォルダー|D:\EARNINGS|  

## <a name="set-up-claims-transformation-on-trusted-forest-adatum"></a><a name="BKMK_3"></a>信頼されているフォレスト (Adatum) で要求変換を設定する  
このステップでは、Adatum で変換ポリシーを作成して、Contoso に渡す "Company" 以外のすべての要求を拒否します。  

Windows PowerShell の Active Directory モジュールには、 **Denyallexcept**引数が用意されています。これにより、変換ポリシー内の指定された要求以外のすべてが削除されます。  

要求変換を設定するには、要求変換ポリシーを作成して、信頼されているフォレストと信頼する側のフォレスト間でリンクする必要があります。  

### <a name="create-a-claims-transformation-policy-in-adatum"></a><a name="BKMK_2.2"></a>Adatum で要求変換ポリシーを作成する  

##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-claims-except-company"></a>"Company" 以外のすべての要求を拒否するように変換ポリシーの Adatum を作成するには  

1. Adatum.com という<strong>pass@word1</strong>パスワードを使用して、管理者としてドメインコントローラーにサインインします。  

2. Windows PowerShell で管理者特権でのコマンドプロンプトを開き、次のように入力します。  

   ```  
   New-ADClaimTransformPolicy `  
   -Description:"Claims transformation policy to deny all claims except Company"`  
   -Name:"DenyAllClaimsExceptCompanyPolicy" `  
   -DenyAllExcept:company `  
   -Server:"adatum.com" `  

   ```  

### <a name="set-a-claims-transformation-link-on-adatums-trust-domain-object"></a><a name="BKMK_2.3"></a>Adatum の信頼ドメインオブジェクトで要求変換リンクを設定する  
この手順では、新しく作成された要求変換ポリシーを、Contoso の Adatum の信頼ドメインオブジェクトに適用します。  

##### <a name="to-apply-the-claims-transformation-policy"></a>要求変換ポリシーを適用するには  

1. Adatum.com という<strong>pass@word1</strong>パスワードを使用して、管理者としてドメインコントローラーにサインインします。  

2. Windows PowerShell で管理者特権でのコマンドプロンプトを開き、次のように入力します。  

   ```  

     Set-ADClaimTransformLink `  
   -Identity:"contoso.com" `  
   -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
   '"TrustRole:Trusted `  

   ```  

## <a name="set-up-claims-transformation-in-the-trusting-forest-contoso"></a><a name="BKMK_4"></a>信頼する側のフォレスト (Contoso) に要求の変換を設定します。  
このステップでは、Contoso (信頼する側のフォレスト) の要求変換ポリシーを作成して、"Company" 以外のすべての要求を拒否します。 要求変換ポリシーを作成し、それをフォレストの信頼にリンクする必要があります。  

### <a name="create-a-claims-transformation-policy-in-contoso"></a><a name="BKMK_4.1"></a>Contoso で要求変換ポリシーを作成する  

##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-except-company"></a>"Company" 以外のすべてを拒否する変換ポリシーの Adatum を作成するには  

1. Contoso.com という<strong>pass@word1</strong>パスワードを使用して、管理者としてドメインコントローラーにサインインします。  

2. Windows PowerShell で管理者特権でのコマンドプロンプトを開き、次のように入力します。  

   ```  
   New-ADClaimTransformPolicy `  
   -Description:"Claims transformation policy to deny all claims except company" `  
   -Name:"DenyAllClaimsExceptCompanyPolicy" `  
   -DenyAllExcept:company `  
   -Server:"contoso.com" `  

   ```  

### <a name="set-a-claims-transformation-link-on-contosos-trust-domain-object"></a><a name="BKMK_4.2"></a>Contoso の信頼ドメインオブジェクトで要求変換リンクを設定する  
この手順では、Adatum の contoso.com trust ドメインオブジェクトに新しく作成された要求変換ポリシーを適用して、"Company" を contoso.com に渡すことができるようにします。 信頼ドメインオブジェクトの名前は adatum.com です。  

##### <a name="to-set-the-claims-transformation-policy"></a>要求変換ポリシーを設定するには  

1. Contoso.com という<strong>pass@word1</strong>パスワードを使用して、管理者としてドメインコントローラーにサインインします。  

2. Windows PowerShell で管理者特権でのコマンドプロンプトを開き、次のように入力します。  

   ```  

     Set-ADClaimTransformLink   
   -Identity:"adatum.com" `  
   -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
   -TrustRole:Trusting `  

   ```  

## <a name="validate-the-scenario"></a><a name="BKMK_5"></a>シナリオを検証する  
このステップでは、ファイルサーバー FILE1 にセットアップされた D:\EARNINGS フォルダーにアクセスして、ユーザーが共有フォルダーにアクセスできることを検証します。  

#### <a name="to-ensure-that-the-adatum-user-can-access-the-shared-folder"></a>Adatum ユーザーが共有フォルダーにアクセスできるようにするには  

1. パスワード<strong>pass@word1</strong>を使用して、クライアントコンピューター CLIENT1 に Jeff Low としてサインインします。  

2. \FILE1.contoso.com\Earnings. フォルダーを参照して \\  

3. Jeff Low はフォルダーにアクセスできる必要があります。  

## <a name="additional-scenarios-for-claims-transformation-policies"></a>要求変換ポリシーのその他のシナリオ  
要求変換のその他の一般的なケースの一覧を次に示します。  


|                                                 シナリオ                                                 |                                                                                                                                                                                                                                           ポリシー                                                                                                                                                                                                                                            |
|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                  Adatum から Contoso Adatum に送られるすべての要求を許可します                  |                                                          コード <br />新規-ADClaimTransformPolicy \`<br /> -Description: "すべての要求を許可する要求変換ポリシー" \`<br />-Name: "AllowAllClaimsPolicy" \`<br />-AllowAll \`<br />-サーバー "contoso .com" \`<br />Set-ADClaimTransformLink \`<br />-Identity: com "\`<br />-ポリシー: "AllowAllClaimsPolicy" \`<br />-TrustRole: \` の信頼<br />-サーバー "contoso .com" \`                                                          |
|                  Adatum から Contoso Adatum に送られるすべての要求を拒否します                   |                                                            コード <br />新規-ADClaimTransformPolicy \`<br />-Description: "すべての要求を拒否する要求変換ポリシー" \`<br />-Name: "DenyAllClaimsPolicy" \`<br /> -DenyAll \`<br />-サーバー "contoso .com" \`<br />Set-ADClaimTransformLink \`<br />-Identity: com "\`<br />-ポリシー: "DenyAllClaimsPolicy" \`<br />-TrustRole: \` の信頼<br />-サーバー "contoso .com"\`                                                             |
| Adatum に由来する "Company" と "Department" 以外のすべての要求を Contoso Adatum に移行できるようにします。 | コード <br />-New-Adclaimトランスポリシー \`<br />-Description: "company と department 以外のすべての要求を許可する要求の変換ポリシー" \`<br /> -Name: "AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br />-AllowAllExcept: company、department \`<br />-サーバー "contoso .com" \`<br />Set-ADClaimTransformLink \`<br /> -Identity: com "\`<br />-ポリシー: "AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br /> -TrustRole: \` の信頼<br />-サーバー "contoso .com" \` |

## <a name="see-also"></a><a name="BKMK_Links"></a>関連項目  

-   要求変換に使用できるすべての Windows PowerShell コマンドレットの一覧については、「 [Active Directory PowerShell コマンドレットリファレンス](https://go.microsoft.com/fwlink/?LinkId=243150)」を参照してください。  

-   2つのフォレスト間で DAC の構成情報をエクスポートおよびインポートする高度なタスクについては、[動的 Access Control PowerShell のリファレンス](https://go.microsoft.com/fwlink/?LinkId=243150)を使用してください。  

-   [フォレスト間にわたる要求の展開](Deploy-Claims-Across-Forests.md)  

-   [要求変換規則言語](Claims-Transformation-Rules-Language.md)  

-   [動的 Access Control: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  


