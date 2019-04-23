---
ms.assetid: 01988844-df02-4952-8535-c87aefd8a38a
title: Deploy Automatic File Classification (Demonstration Steps)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 77fb8cc6e13cb82e4d07808c3ae77757a4b2de79
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826783"
---
# <a name="deploy-automatic-file-classification-demonstration-steps"></a>Deploy Automatic File Classification (Demonstration Steps)

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Active Directory でリソース プロパティを有効にし、ファイル サーバーで分類規則を作成してから、ファイル サーバーでファイルのリソース プロパティに値を割り当てる方法について説明します。 例えば、次の分類規則を作成します。  
  
-   一連の文字列 'Contoso Confidential' のファイルを検索するコンテンツ分類規則 この文字列がファイルで見つかった場合、そのファイルの Impact リソース プロパティが High に設定されます。  
  
-   一連のファイルで正規表現が 1 つのファイルで 10 回以上社会保障番号に一致するかを検索するコンテンツ分類規則。 パターンが見つかった場合、ファイルは個人を特定できる情報と分類され、Personally Identifiable Information リソース プロパティが High に設定されます。  
  
**このドキュメントで**  
  
-   [ステップ 1: リソース プロパティ定義を作成します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)  
  
-   [手順 2:文字列のコンテンツ分類規則を作成します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step2)  
  
-   [手順 3:正規表現のコンテンツ分類規則を作成します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)  
  
-   [手順 4:ファイルが分類されていることを確認します。](Deploy-Automatic-File-Classification--Demonstration-Steps-.md#BKMK_Step4)  
  
> [!NOTE]  
> このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
## <a name="BKMK_Step1"></a>手順 1:リソース プロパティ定義を作成する  
Impact リソース プロパティおよび Personally Identifiable Information リソース プロパティを有効にして、ファイル分類インフラストラクチャがこれらのリソース プロパティを使用してネットワーク共有フォルダーでスキャンされたファイルにタグを付けることができるようにします。  
  
[Windows PowerShell を使用してこの手順を実行します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-create-resource-property-definitions"></a>リソース プロパティ定義を作成するには  
  
1.  ドメイン コントローラーで、Domain Admins セキュリティ グループのメンバーとしてサーバーにサインインします。  
  
2.  Active Directory 管理センターを開きます。 サーバー マネージャーで **[ツール]** をクリックしてから、**[Active Directory 管理センター]** をクリックします。  
  
3.  **[ダイナミック アクセス制御]** を展開してから、**[リソース プロパティ]** をクリックします。  
  
4.  **[Impact]** を右クリックし、**[有効にする]** をクリックします。  
  
5.  **[Personally Identifiable Information]** を右クリックし、**[有効にする]** をクリックします。  
  
![ソリューション ガイド](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド。  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
```  
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'   
Set-ADResourceProperty '"Enabled:$true '"Identity:'CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
```  
  
## <a name="BKMK_Step2"></a>手順 2:文字列のコンテンツ分類規則を作成する  
文字列のコンテンツ分類規則は、ファイルで特定の文字列がないかをスキャンします。 文字列が見つかった場合、リソース プロパティの値を構成できます。 この例では、ネットワーク共有フォルダー上の各ファイルをスキャンし、' Contoso Confidential ' の文字列を検索 文字列が見つかった場合、関連ファイルは、ビジネスに大きな影響を与えるものとして分類されます。  
  
[Windows PowerShell を使用してこの手順を実行します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
#### <a name="to-create-a-string-content-classification-rule"></a>文字列のコンテンツ分類規則を作成するには  
  
1.  Administrators セキュリティ グループのメンバーとしてファイル サーバーにログオンします。  
  
2.  Windows PowerShell コマンド プロンプトで「 **Update-FsrmClassificationPropertyDefinition** 」と入力してから、Enter キーを押します。 これにより、ドメイン コントローラーで作成されたプロパティ定義がファイル サーバーに同期されます。  
  
3.  ファイル サーバー リソース マネージャーを開きます。 サーバー マネージャーで **[ツール]** をクリックしてから、**[ファイル サーバー リソース マネージャー]** をクリックします。  
  
4.  **[分類管理]** を展開し、**[分類規則]** を右クリックしてから、**[分類スケジュールの構成]** をクリックします。  
  
5.  **[固定スケジュールを有効にする]** チェック ボックスを選択し、**[新しいファイルの連続分類を許可する]** チェック ボックスを選択し、分類を実行する曜日を選択してから、**[OK]** をクリックします。  
  
6.  **[分類規則]** を右クリックし、 **[分類規則の作成]** をクリックします。  
  
7.  **[全般]** タブの **[規則名]** ボックスに「 **Contoso Confidential**」などの規則名を入力します。  
  
8.  **[スコープ]** タブで **[追加]** をクリックし、この規則に含めるフォルダー (D:\Finance Documents など) を選択します。  
  
    > [!NOTE]  
    > スコープに動的な名前空間を選択することもできます。 分類規則の動的な名前空間の詳細については、次を参照してください。[新ファイル サーバー リソース マネージャーで Windows Server 2012 で\[リダイレクト\]](assetId:///d53c603e-6217-4b98-8508-e8e492d16083)します。  
  
9. **[分類]** タブで次のように構成します。  
  
    -   **[ファイルにプロパティを割り当てる方法を選択してください]** ボックスで **[コンテンツ分類子]** が選択されていることを確認します。  
  
    -   **[ファイルに割り当てるプロパティを選択してください]** ボックスで **[Impact]** をクリックします。  
  
    -   **[値の指定]** ボックスで **[High]** をクリックします。  
  
10. **[パラメーター]** 見出しで **[構成]** をクリックします。  
  
11. **[式の種類]** 列で **[文字列]** を選択します。  
  
12. **[式]** 列に「 **Contoso Confidential**」と入力してから、**[OK]** をクリックします。  
  
13. **[評価の種類]** タブで **[既存のプロパティ値を再評価する]** チェック ボックスを選択し、**[既存の値を上書きする]** をクリックしてから、**[OK]** をクリックします。  
  
![ソリューション ガイド](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド。  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
```  
$date = Get-Date  
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;$AutomaticClassificationScheduledTask  
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask  
New-FSRMClassificationRule -Name 'Contoso Confidential' -Property "Impact_MS" -PropertyValue "3000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite  
```  
  
## <a name="BKMK_Step3"></a>手順 3:正規表現のコンテンツ分類規則を作成する  
正規表現の分類規則は、正規表現に一致するパターンをファイルでスキャンします。 正規表現に一致する文字列が見つかった場合、リソース プロパティの値を構成できます。 この例では、ネットワーク共有フォルダー上の各ファイルをスキャンし、社会保障番号のパターン (XXX-XX-XXXX) に一致する文字列を検索します。 パターンが見つかった場合、関連ファイルは、個人を特定できる情報が含まれているものと分類されます。  
  
[Windows PowerShell を使用してこの手順を実行します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)  
  
#### <a name="to-create-a-regular-expression-content-classification-rule"></a>正規表現のコンテンツ分類規則を作成するには  
  
1.  Administrators セキュリティ グループのメンバーとしてファイル サーバーにサインインします。  
  
2.  Windows PowerShell コマンド プロンプトで「 **Update-FsrmClassificationPropertyDefinition**」と入力してから、Enter キーを押します。 これにより、ドメイン コントローラーで作成されたプロパティ定義がファイル サーバーに同期されます。  
  
3.  ファイル サーバー リソース マネージャーを開きます。 サーバー マネージャーで **[ツール]** をクリックしてから、**[ファイル サーバー リソース マネージャー]** をクリックします。  
  
4.  **[分類規則]** を右クリックし、 **[分類規則の作成]** をクリックします。  
  
5.  **[全般]** タブの **[規則名]** ボックスに、「PII Rule」などの分類規則名を入力します。  
  
6.  **[スコープ]** タブで **[追加]** をクリックしてから、この規則に含めるフォルダー (D:\Finance Documents など) を選択します。  
  
7.  **[分類]** タブで次のように構成します。  
  
    -   **[ファイルにプロパティを割り当てる方法を選択してください]** ボックスで **[コンテンツ分類子]** が選択されていることを確認します。  
  
    -   **[ファイルに割り当てるプロパティを選択してください]** ボックスで **[Personally Identifiable Information]** をクリックします。  
  
    -   **[値の指定]** ボックスで **[High]** をクリックします。  
  
8.  **[パラメーター]** 見出しで **[構成]** をクリックします。  
  
9. **[式の種類]** 列で **[正規表現]** を選択します。  
  
10. **式**列に「 **^ (?!000) ([0-7] \d{2}| 7([0-7]\d|7[012])) ([-]?)(?!00) \d\d\3 (?!0000) \d{4}$**  
  
11. **[最小項目]** 列に **10** と入力してから、**[OK]** をクリックします。  
  
12. **[評価の種類]** タブで **[既存のプロパティ値を再評価する]** チェック ボックスを選択し、**[既存の値を上書きする]** をクリックしてから、**[OK]** をクリックします。  
  
![ソリューション ガイド](media/Deploy-Automatic-File-Classification--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド。  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
```  
New-FSRMClassificationRule -Name "PII Rule" -Property "PII_MS" -PropertyValue "5000" -Namespace @('D:\Finance Documents') -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=10;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite  
```  
  
## <a name="BKMK_Step4"></a>手順 4:ファイルが正しく分類されていることを確認する  
分類規則で指定されているフォルダー内で作成されたファイルのプロパティを表示することで、ファイルが正しく分類されているかを確認できます。  
  
#### <a name="to-verify-that-the-files-are-classified-correctly"></a>ファイルが正しく分類されていることを確認するには  
  
1.  ファイル サーバーで、ファイル サーバー リソース マネージャーを使用して分類規則を実行します。  
  
    1.  **[分類管理]** をクリックし、**[分類規則]** を右クリックしてから、**[すべての規則で今すぐ分類を実行する]** をクリックします。  
  
    2.  **[分類の完了を待つ]** オプションをクリックしてから、**[OK]** をクリックします。  
  
    3.  自動分類レポートを閉じます。  
  
    4.  これを行うには、Windows PowerShell を使用して次のコマンドを実行します。**Start-FSRMClassification '"RunDuration 0 -Confirm:$false**  
  
2.  分類規則で指定されたフォルダー (D:\Finance Documents など) に移動します。  
  
3.  そのフォルダー内のファイルを右クリックしてから、**[プロパティ]** をクリックします。  
  
4.  **[分類]** タブをクリックし、ファイルが正しく分類されていることを確認します。  
  
## <a name="BKMK_Links"></a>参照してください。  
  
-   [シナリオ:分類を使用して、データを取得します。](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)  
  
-   [自動ファイル分類を計画します。](https://docs.microsoft.com/previous-versions/orphan-topics/ws.11/jj574209(v%3dws.11))  

  
-   [ダイナミック アクセス制御:シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  
  

