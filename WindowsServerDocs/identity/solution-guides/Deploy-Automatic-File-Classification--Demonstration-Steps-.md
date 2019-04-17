---
ms.assetid: 01988844-df02-4952-8535-c87aefd8a38a
title: "展開 (デモンストレーション手順) の自動ファイル分類"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1c5c0fa221e0d7375216426f838ba37bee852984
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-automatic-file-classification-demonstration-steps"></a>展開 (デモンストレーション手順) の自動ファイル分類

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Active Directory 内のリソース プロパティを有効にする、ファイル サーバーで、分類規則を作成およびファイル サーバー上のファイル リソースのプロパティに値を割り当てる方法について説明します。 この例では、次の分類規則が作成されます。  
  
-   一連の文字列「Contoso Confidential ' ファイルを検索するコンテンツ分類規則 文字列が見つかった場合、ファイルに、Impact リソース プロパティが high ファイルに設定します。  
  
-   1 つのファイルで 10 回以上社会保障番号と一致する正規表現のファイルのセットを検索するコンテンツ分類規則。 パターンが見つかった場合、ファイルは個人を特定できる情報として分類し、Personally Identifiable Information リソース プロパティが高] に設定します。  
  
**このドキュメントで**  
  
-   [Step 1: Create resource property definitions](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)  
  
-   [手順 2: 文字列のコンテンツ分類規則を作成します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step2)  
  
-   [手順 3: 正規表現のコンテンツ分類規則を作成します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)  
  
-   [手順 4: は、ファイルが分類されていることを確認します。](Deploy-Automatic-File-Classification--Demonstration-Steps-.md#BKMK_Step4)  
  
> [!NOTE]  
> このトピックには、説明する手順の一部を自動化するのに使用できるサンプル Windows PowerShell コマンドレットが含まれています。 詳細については、次を参照してください。[コマンドレットを使用した](https://go.microsoft.com/fwlink/p/?linkid=230693)します。  
  
## <a name="BKMK_Step1"></a>Step 1: Create resource property definitions  
ファイル分類インフラストラクチャは、これらのリソース プロパティを使用してネットワーク共有フォルダーでスキャンされたファイル タグを付けるにできるようにへの影響および Personally Identifiable Information リソース プロパティが有効にします。  
  
[Do this step using Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-create-resource-property-definitions"></a>To create resource property definitions  
  
1.  On the domain controller, sign in to the server as a member of the Domain Admins security group.  
  
2.  Open Active Directory Administrative Center. サーバー マネージャーで、クリックして**ツール**、] をクリックし、 **Active Directory 管理センター**します。  
  
3.  Expand **Dynamic Access Control**, and then click **Resource Properties**.  
  
4.  Right-click **Impact**, and then click **Enable**.  
  
5.  Right-click **Personally Identifiable Information**, and then click **Enable**.  
  
![ソリューション ガイド](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。  
  
```  
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'   
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
```  
  
## <a name="BKMK_Step2"></a>手順 2: 文字列のコンテンツ分類規則を作成します。  
文字列のコンテンツ分類規則では、特定の文字列用のファイルをスキャンします。 文字列が見つかった場合、リソース プロパティの値を構成できます。 この例でをネットワーク共有フォルダー上の各ファイルをスキャンし、文字列「Contoso Confidential ' を探します 文字列が見つかった場合、関連付けられたファイルは、ビジネスに大きな影響を与えるものとして分類されます。  
  
[Do this step using Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
#### <a name="to-create-a-string-content-classification-rule"></a>文字列のコンテンツ分類規則を作成するには  
  
1.  Administrators セキュリティ グループのメンバーとしてファイル サーバーにログオンします。  
  
2.  Windows PowerShell コマンド プロンプトから次のように入力します。**Update-fsrmclassificationpropertydefinition**し、Enter キーを押します。 これにより、ファイル サーバーにドメイン コントローラーで作成されたプロパティ定義が同期されます。  
  
3.  ファイル サーバー リソース マネージャーを開きます。 In Server Manager, click **Tools**, and then click **File Server Resource Manager**.  
  
4.  展開**分類管理**、右クリックして**分類規則**、] をクリックし、**分類スケジュールの構成**します。  
  
5.  選択、**固定スケジュールを有効にする**チェック ボックスで、**新しいファイルの連続分類を許可する**] チェック ボックスをクリックして、分類を実行する曜日を選択**OK**します。  
  
6.  右クリック**分類規則**、] をクリックし、**分類規則の作成**します。  
  
7.  **全般**] タブの [、**ルール名**ボックスで、規則の名前を入力します。**Contoso Confidential**します。  
  
8.  On the **Scope** tab, click **Add**, and choose the folders that should be included in this rule, such as D:\Finance Documents.  
  
    > [!NOTE]  
    > スコープの動的名前空間もできます。 分類規則のための動的な名前空間の詳細については、次を参照してください。[の新機能ファイル サーバー リソース マネージャーの Windows Server 2012 \[redirected\]](assetId:///d53c603e-6217-4b98-8508-e8e492d16083)します。  
  
9. **分類**] タブで、次の構成します。  
  
    -   **ファイルにプロパティを割り当てる方法を選択**ボックスしていることを確認するには、**コンテンツ分類子**が選択されています。  
  
    -   **ファイルに割り当てるプロパティを選択して**ボックスで、をクリックして**影響**します。  
  
    -   **値を指定して**ボックスで、をクリックして**高**します。  
  
10. 下にある、**パラメーター**見出し、] をクリックして**構成**します。  
  
11. **式の種類**列で、**文字列**します。  
  
12. **式**] 列に「**Contoso Confidential**] をクリックし、**OK**します。  
  
13. **評価の種類**タブを選択し、**既存のプロパティ値を再評価する**チェック ボックスをオン] をクリックして**、既存の値を上書き**、] をクリックし、**[OK]**します。  
  
![ソリューション ガイド](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。  
  
```  
$date = Get-Date  
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;$AutomaticClassificationScheduledTask  
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask  
New-FSRMClassificationRule -Name 'Contoso Confidential' -Property "Impact_MS" -PropertyValue "3000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite  
```  
  
## <a name="BKMK_Step3"></a>手順 3: 正規表現のコンテンツ分類規則を作成します。  
正規表現の分類規則では、正規表現に一致するパターンのファイルをスキャンします。 正規表現に一致する文字列が見つかった場合、リソース プロパティの値を構成できます。 この例では、ネットワーク共有フォルダー上の各ファイルのスキャンをし、社会保障番号 (XXX XX XXXX) のパターンに一致する文字列を検索します。 パターンが見つかった場合、関連付けられたファイルは個人を特定できる情報として分類されます。  
  
[Do this step using Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)  
  
#### <a name="to-create-a-regular-expression-content-classification-rule"></a>正規表現のコンテンツ分類規則を作成するには  
  
1.  Sign in to the file server as a member of the Administrators security group.  
  
2.  From the Windows PowerShell command prompt, type **Update-FsrmClassificationPropertyDefinition**, and then press ENTER. This will synchronize the property definitions that are created on the domain controller to the file server.  
  
3.  ファイル サーバー リソース マネージャーを開きます。 In Server Manager, click **Tools**, and then click **File Server Resource Manager**.  
  
4.  右クリック**分類規則**、] をクリックし、**分類規則の作成**します。  
  
5.  **全般的な**] タブで、**ルール名**ボックスに、PII 規則など、分類規則の名前を入力します。  
  
6.  **スコープ**] タブ、[**追加**、し、D:\Finance Documents など、この規則に含める必要があるフォルダーを選択します。  
  
7.  **分類**] タブで、次の構成します。  
  
    -   **ファイルにプロパティを割り当てる方法を選択**ボックスしていることを確認するには、**コンテンツ分類子**が選択されています。  
  
    -   **ファイルに割り当てるプロパティを選択して**ボックスで、をクリックして**Personally Identifiable Information**します。  
  
    -   **値を指定して**ボックスで、をクリックして**高**します。  
  
8.  下にある、**パラメーター**見出し、] をクリックして**構成**します。  
  
9. **式の種類**列で、**正規表現**します。  
  
10. **式**] 列に「**^ (?000)([0-7]\d{2}|7([0-7]\d|7[012])) ([-]?)(?!00) \d\d\3 (?0000) \d {4} $**  
  
11. **最小項目**] 列に「**10**、] をクリックし、**OK**します。  
  
12. **評価の種類**タブを選択し、**既存のプロパティ値を再評価する**チェック ボックスをオン] をクリックして**、既存の値を上書き**、] をクリックし、**[OK]**します。  
  
![ソリューション ガイド](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。  
  
```  
New-FSRMClassificationRule -Name "PII Rule" -Property "PII_MS" -PropertyValue "5000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=10;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite  
```  
  
## <a name="BKMK_Step4"></a>手順 4: は、ファイルが正しく分類されていることを確認します。  
分類規則で指定したフォルダーで作成されたファイルのプロパティを表示して、ファイルが正しく分類されていることを確認することができます。  
  
#### <a name="to-verify-that-the-files-are-classified-correctly"></a>ファイルが正しく分類されていることを確認するには  
  
1.  ファイル サーバーで、ファイル サーバー リソース マネージャーを使用して分類規則を実行します。  
  
    1.  をクリックして**分類管理**、右クリックして**分類規則**、] をクリックし、**実行ですべての規則で今すぐ分類**します。  
  
    2.  をクリックして、**分類の完了を待ってから**オプションをクリックして**OK**します。  
  
    3.  自動分類レポートを閉じます。  
  
    4.  次のコマンドを使って Windows PowerShell を使用してこれを行う: **Start-fsrmclassification '"RunDuration 0 - 確認: $false**  
  
2.  D:\Finance Documents など、分類規則で指定されたフォルダーに移動します。  
  
3.  そのフォルダー内のファイルを右クリックし、をクリックして**プロパティ**します。  
  
4.  をクリックして、**分類**タブをクリックし、ファイルが正しく分類されていることを確認します。  
  
## <a name="BKMK_Links"></a>参照してください。  
  
-   [シナリオ: 分類を使用して、データに関する洞察を取得します。](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)  
  
-   [自動ファイル分類を計画します。](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)  
  
-   [ダイナミック アクセス制御: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  
  

