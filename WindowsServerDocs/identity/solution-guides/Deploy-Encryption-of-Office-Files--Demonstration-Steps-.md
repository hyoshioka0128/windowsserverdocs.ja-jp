---
ms.assetid: 2c76e81a-c2eb-439f-a89f-7d3d70790244
title: "展開 (デモンストレーション手順) に Office ファイルの暗号化"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 529000c60a80ee33fc2aa7d09370d8ac1e06311c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="deploy-encryption-of-office-files-demonstration-steps"></a>展開 (デモンストレーション手順) に Office ファイルの暗号化

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Contoso's Finance Department has a number of file servers that store their documents. These documents can be general documentation or they can have a high-business impact (HBI). For example, any document that contains confidential information is deemed, by Contoso, to have a high-business impact. Contoso wants to ensure that all their documentation has a minimum amount of protection and that their HBI documentation is restricted to the appropriate people. To accomplish this, Contoso is exploring using the File Classification Infrastructure (FCI) and AD RMS that is available in  Windows Server 2012 . By using FCI, Contoso will classify all of the documents on their file server, based on the content, and then use AD RMS to apply the appropriate rights policy.  
  
In this scenario, you'll perform the following steps:  
  
|タスク|説明|  
|--------|---------------|  
|[Enable resource properties](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_1.1)|Enable the **Impact** and **Personally Identifiable Information** resource properties.|  
|[Create classification rules](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_2)|Create the following classification rules: **HBI Classification Rule** and **PII Classification Rule**.|  
|[Use file management tasks to automatically protect documents with AD RMS](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_3)|Create a file management task that automatically used AD RMS to protect documents with high personally identifiable information (PII). Only members of the FinanceAdmin group will have access to documents that contain high PII.|  
|[View the results](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_4)|Examine the classification of documents and observe how they change as you change the content in the document. Also verify how the document gets protected by AD RMS.|  
|[Verify AD RMS protection](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_5)|Verify that the document is protected with AD RMS.|  
|||  
  
## <a name="BKMK_1.1"></a>Step 1: Enable resource properties  
  
#### <a name="to-enable-resource-properties"></a>To enable resource properties  
  
1.  In Hyper-V Manager, connect to server ID_AD_DC1. Sign in to the server by using Contoso\Administrator with the password **pass@word1**.  
  
2.  Open Active Directory Administrative Center, and click **Tree View**.  
  
3.  Expand **DYNAMIC ACCESS CONTROL**, and select **Resource Properties**.  
  
4.  Scroll down to the **Impact** property in the **Display name** column. Right-click **Impact**, and then click **Enable**.  
  
5.  Scroll down to the **Personally Identifiable Information** property in the **Display name** column. Right-click **Personally Identifiable Information**, and then click **Enable**.  
  
6.  To publish the resource properties in the **Global Resource List**, in the left pane, click **Resource Property Lists**, and then double-click **Global Resource Property List**.  
  
7.  Click **Add**, and then scroll down to and click **Impact** to add it to the list. Do the same for **Personally Identifiable Information**. Click **OK** twice to finish.  
  
![ソリューション ガイド](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。  
  
```  
Set-ADResourceProperty -Enabled:$true -Identity:"CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com"  
Set-ADResourceProperty -Enabled:$true -Identity:"CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com" 
```  
  
## <a name="BKMK_2"></a>Step 2: Create classification rules  
This step explains how to create the **High Impact** classification rule. This rule will search the content of documents and if the string "Contoso Confidential" is found, it will classify this document as having high-business impact. This classification will override any previously assigned classification of low-business impact.  
  
You will also create a **High PII** rule. This rule searches the content of documents, and if a Social Security number is found, it classifies the document as having high PII.  
  
#### <a name="to-create-the-high-impact-classification-rule"></a>To create the high-impact classification rule  
  
1.  In Hyper-V Manager, connect to server ID_AD_FILE1. Sign in to the server by using Contoso\Administrator with the password **pass@word1**.  
  
2.  You need to refresh the Global Resource Properties from Active Directory. Open Windows PowerShell and type: `Update-FSRMClassificationPropertyDefinition`, and then press ENTER. Windows PowerShell を閉じます。  
  
3.  ファイル サーバー リソース マネージャーを開きます。 ファイル サーバー リソース マネージャーを開くにはクリックして**開始**、種類**ファイル サーバー リソース マネージャー**、] をクリックし、**ファイル サーバー リソース マネージャー**します。  
  
4.  In the left pane of File Server Resource Manager, expand **Classification Management**, and then select **Classification Rules**.  
  
5.  In the **Actions** pane, click **Configure Classification Schedule**. On the **Automatic Classification** tab, select **Enable fixed schedule**, select a **Day of the week**, and then select the **Allow continuous classification for new files** check box. をクリックして**OK**します。  
  
6.  In the **Actions** pane, click **Create Classification Rule**. This opens the **Create Classification Rule** dialog box.  
  
7.  In the **Rule name** box, type **High Business Impact**.  
  
8.  In the **Description** box, type **Determines if the document has a high business impact based on the presence of the string "Contoso Confidential"**  
  
9. On the **Scope** tab, click **Set Folder Management Properties**, select **Folder Usage**, click **Add**, then click **Browse**, browse to D:\Finance Documents as the path, click **OK**, and then choose a property value named **Group Files** and click **Close**. Once management properties are set, on the **Rule Scope** tab select **Group Files**.  
  
10. をクリックして、**分類**] タブ。  Under **Choose a method to assign the property to files**, select **Content Classifier** from the drop-down list.  
  
11. Under **Choose a property to assign to files**, select **Impact** from the drop-down list.  
  
12. Under **Specify a value**, select **High** from the drop-down list.  
  
13. Click **Configure** under **Parameters**.  In the **Classification Parameters** dialog box, in the **Expression Type** list, select **String**. In the **Expression** box, type: **Contoso Confidential**, and then click **OK**.  
  
14. Click the **Evaluation Type** tab.  Click **Re-evaluate existing property values**, click **Overwrite**the existing value, and then click **OK** to finish.  
  
![ソリューション ガイド](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。  
  
```  
Update-FSRMClassificationPropertyDefinition  
$date = Get-Date  
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;  
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask  
New-FSRMClassificationRule -Name "High Business Impact" -Property "Impact_MS" -Description "Determines if the document has a high business impact based on the presence of the string 'Contoso Confidential'" -PropertyValue "3000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite  
```  
  
#### <a name="to-create-the-high-pii-classification-rule"></a>To create the high-PII classification rule  
  
1.  In Hyper-V Manager, connect to server ID_AD_FILE1. Sign in to the server by using Contoso\Administrator with the password **pass@word1**.  
  
2.  On the desktop, open the folder named **Regular Expressions**, and then open the text document named **RegEx-SSN**. Highlight and copy the following regular expression string:  **^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$**. This string will be used later in this step so keep it on your clipboard.  
  
3.  ファイル サーバー リソース マネージャーを開きます。 ファイル サーバー リソース マネージャーを開くにはクリックして**開始**、種類**ファイル サーバー リソース マネージャー**、] をクリックし、**ファイル サーバー リソース マネージャー**します。  
  
4.  In the left pane of File Server Resource Manager, expand **Classification Management**, and then select **Classification Rules**.  
  
5.  In the **Actions** pane, click **Configure Classification Schedule**. On the **Automatic Classification** tab, select **Enable fixed schedule**, select a **Day of the week**, and then select the **Allow continuous classification for new files** check box. [Ok] をクリックします。  
  
6.  In the **Rule name** box, type **High PII**. In the **Description** box, type **Determines if the document has a high PII based on the presence of a Social Security Number.**  
  
7.  Click the **Scope** tab, select the **Group Files** check box.  
  
8.  をクリックして、**分類**] タブ。  Under **Choose a method to assign the property to files**, select **Content Classifier** from the drop-down list.  
  
9. Under **Choose a property to assign to files**, select **Personally Identifiable Information** from the drop-down list.  
  
10. Under **Specify a value**, select **High** from the drop-down list.  
  
11. Click **Configure** under **Parameters**.   
    In the **Classification Parameters**window, in the **Expression Type** list, select **Regular Expression**. In the **Expression** box, paste the text from your clipboard: **^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$**, and then click **OK**.  
  
    > [!NOTE]  
    > This expression will allow invalid Social Security numbers. This allows us to use fictitious Social Security numbers in the demonstration.  
  
12. Click the **Evaluation Type** tab.  Select **Re-evaluate existing property values**, **Overwrite**the existing value, and then click **OK** to finish.  
  
![ソリューション ガイド](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。  
  
```  
New-FSRMClassificationRule -Name "High PII" -Description "Determines if the document has a high PII based on the presence of a Social Security Number." -Property "PII_MS" -PropertyValue "5000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=1;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite  
```  
  
You should now have two classification rules:  
  
-   High Business Impact  
  
-   High PII  
  
## <a name="BKMK_3"></a>Step 3: Use file management tasks to automatically protect documents with AD RMS  
コンテンツに基づいてドキュメントを自動的に分類する規則を作成したら、これで、次の手順では、AD RMS を使用して、分類に基づいて、特定のドキュメントを自動的に保護するファイル管理タスクを作成します。 この手順では、すべてのドキュメントを高 PII を自動的に保護されるファイル管理タスクを作成します。 Only members of the FinanceAdmin group will have access to documents that contain high PII.  
  
#### <a name="to-protect-documents-with-ad-rms"></a>AD RMS でドキュメントを保護するには  
  
1.  In Hyper-V Manager, connect to server ID_AD_FILE1. Sign in to the server by using Contoso\Administrator with the password **pass@word1**.  
  
2.  ファイル サーバー リソース マネージャーを開きます。 ファイル サーバー リソース マネージャーを開くにはクリックして**開始**、種類**ファイル サーバー リソース マネージャー**、] をクリックし、**ファイル サーバー リソース マネージャー**します。  
  
3.  左側のウィンドウで選択**ファイル管理タスク**します。 **アクション**ウィンドウで、**ファイル管理タスクの作成**します。  
  
4.  **タスク名:**フィールドを入力**High PII**します。 **説明**フィールドを入力**高 PII ドキュメントの自動 RMS 保護**します。  
  
5.  Click the **Scope** tab, select the **Group Files** check box.  
  
6.  をクリックして、**アクション**] タブ。 **種類**[ **RMS 暗号化**します。 をクリックして**参照**テンプレートを選択し、選択、**Contoso Finance Admin のみ**テンプレート。  
  
7.  をクリックして、**条件**タブをクリックし、をクリックして**追加**します。 **プロパティ**[ **Personally Identifiable Information**します。 **演算子**[**等しい**します。 **値**[**高**します。 をクリックして**OK**します。  
  
8.  をクリックして、**スケジュール**] タブ。 **スケジュール**セクションで、をクリックして**毎週**、し、[**日曜日**します。 1 回、週、タスクを実行しているはされなかった可能性がサービスの停止などの中断イベントのためのドキュメントをキャッチすることを確認します。  
  
9. **継続的な操作**セクションで、**に継続的に新しいファイルのタスクを実行**、] をクリックし、**OK**します。 High PII という名前のファイル管理タスクが作成されました。  
  
![ソリューション ガイド](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。  
  
```  
$fmjRmsEncryption = New-FSRMFmjAction -Type 'Rms' -RmsTemplate 'Contoso Finance Admin Only'  
$fmjCondition1 = New-FSRMFmjCondition -Property 'PII_MS' -Condition 'Equal' -Value '5000'  
$date = get-date  
$schedule = New-FsrmScheduledTask -Time $date -Weekly @('Sunday')    
$fmj1=New-FSRMFileManagementJob -Name "High PII" -Description "Automatic RMS protection for high PII documents" -Namespace @('D:\Finance Documents') -Action $fmjRmsEncryption -Schedule $schedule -Continuous -Condition @($fmjCondition1)  
```  
  
## <a name="BKMK_4"></a>手順 4: 結果を表示します。  
時間を見て、新規自動分類および AD RMS 保護規則の動作をすることをお勧めします。 この手順では、ドキュメントの分類を調べし、どのように変更されるように、ドキュメントの内容を変更することを確認します。  
  
#### <a name="to-view-the-results"></a>結果を表示するには  
  
1.  In Hyper-V Manager, connect to server ID_AD_FILE1. Sign in to the server by using Contoso\Administrator with the password **pass@word1**.  
  
2.  エクスプ ローラーで D:\Finance Documents に移動します。  
  
3.  Finance Memo ドキュメントを右クリックし、をクリックして**プロパティ**します。をクリックして、**分類**] タブ、および、Impact プロパティ現在値を持たない通知します。 をクリックして**キャンセル**します。  
  
4.  右クリックし、**Approval to Hire ドキュメントの要求**、し、[**プロパティ**します。  
  
5.  をクリックして、**分類**タブをクリックし、いることを確認**Personally Identifiable Information プロパティ**値は現在ありません。 をクリックして**キャンセル**します。  
  
6.  CLIENT1 に切り替えます。 では、ログオンしている任意のユーザーからサインオフし、パスワードを使用して contoso \mreid としてサインイン**pass@word1**します。  
  
7.  デスクトップで開き、**Finance Documents**共有フォルダー。  
  
8.  開いている、**Finance Memo**ドキュメントです。 ドキュメントの下部で、単語が表示されます**社外秘**します。 変更を読み取る: **Contoso Confidential**します。 ドキュメントを保存して閉じます。  
  
9. 開いている、**Request for Approval to Hire**ドキュメントです。 **Social Security #:**セクションで、入力: 777-77-7777 します。 ドキュメントを保存して閉じます。  
  
    > [!NOTE]  
    > 発生する、分類の 30 秒間待機する必要があります。  
  
10. ID_AD_FILE1 に切り替えて戻ります。 エクスプ ローラーで D:\Finance Documents に移動します。  
  
11. Finance Memo ドキュメントを右クリックし、をクリックして**プロパティ**します。 をクリックして、**分類**] タブ。 いることを確認、**影響**プロパティに設定できるようになりました**高**します。 をクリックして**キャンセル**します。  
  
12. Hire ドキュメント] をクリックして、Request for Approval を右クリックして**プロパティ**します。  
  
13. . をクリックして、**分類**] タブ。 いることを確認、**Personally Identifiable Information**プロパティに設定できるようになりました**高**します。 をクリックして**キャンセル**します。  
  
## <a name="BKMK_5"></a>手順 5: は、AD RMS による保護を確認します。  
  
#### <a name="to-verify-that-the-document-is-protected"></a>ドキュメントが保護されていることを確認するには  
  
1.  ID_AD_CLIENT1 に切り替えて。  
  
2.  開いている、**to Hire 承認依頼**ドキュメントです。  
  
3.  をクリックして**OK**、ドキュメントが AD RMS サーバーへの接続を許可するようにします。  
  
4.  今すぐ、社会保障番号が含まれているために、AD RMS でドキュメントを保護されていることを確認できます。  
  

