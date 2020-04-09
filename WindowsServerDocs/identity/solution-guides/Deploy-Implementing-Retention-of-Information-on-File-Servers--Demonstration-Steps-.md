---
ms.assetid: ee008835-7d3b-4977-adcb-7084c40e5918
title: Deploy Implementing Retention of Information on File Servers (Demonstration Steps)
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a6b6a5d9e153949db6c89ef503b575039ec6022b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861215"
---
# <a name="deploy-implementing-retention-of-information-on-file-servers-demonstration-steps"></a>Deploy Implementing Retention of Information on File Servers (Demonstration Steps)

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイル分類インフラストラクチャおよびファイル サーバー リソース マネージャーを使用して、フォルダーの保持期間を設定したり、ファイルを訴訟ホールドにしたりすることができます。  
  
**このドキュメントの説明**  
  
-   [前提条件](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Prereqs)  
  
-   [手順 1: リソースプロパティの定義を作成する](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)  
  
-   [手順 2: 通知を構成する](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step2)  
  
-   [手順 3: ファイル管理タスクを作成する](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)  
  
-   [手順 4: ファイルを手動で分類する](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step4)  
  
> [!NOTE]  
> このトピックには、説明する手順の一部を自動化するために使用できるサンプルの Windows PowerShell コマンドレットが含まれます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
## <a name="prerequisites"></a>前提条件  
このトピックの手順では、SMTP サーバーがファイル有効期限通知用に構成されていることを前提としています。  
  
## <a name="step-1-create-resource-property-definitions"></a><a name="BKMK_Step1"></a>手順 1: リソースプロパティの定義を作成する  
この手順では、Retention Period および Discoverability リソース プロパティを有効にして、ファイル分類インフラストラクチャがこれらのリソース プロパティを使用してネットワーク共有フォルダーでスキャンされたファイルにタグを付けることができるようにします。  
  
[Windows PowerShell を使用してこの手順を実行する](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-create-resource-property-definitions"></a>リソース プロパティ定義を作成するには  
  
1.  ドメイン コントローラーで、Domain Admins セキュリティ グループのメンバーとしてサーバーにサインインします。  
  
2.  Active Directory 管理センターを開きます。 サーバー マネージャーで **[ツール]** をクリックしてから、 **[Active Directory 管理センター]** をクリックします。  
  
3.  **[ダイナミック アクセス制御]** を展開してから、 **[リソース プロパティ]** をクリックします。  
  
4.  **[保有期間]** を右クリックし、 **[有効にする]** をクリックします。  
  
5.  **[発見可能]** を右クリックし、 **[有効にする]** をクリックします。  
  
![ソリューションガイド](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 書式上の制約のため、複数行にわたって折り返される場合でも、各コマンドレットは 1 行に入力してください。  
  
```  
Set-ADResourceProperty -Enabled:$true -Identity:'CN=RetentionPeriod_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
Set-ADResourceProperty -Enabled:$true -Identity:'CN=Discoverability_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
```  
  
## <a name="step-2-configure-notifications"></a><a name="BKMK_Step2"></a>手順 2: 通知を構成する  
この手順では、ファイル サーバー リソース マネージャーのコンソールを使用して、SMTP サーバー、既定の管理者電子メール アドレス、およびレポート送信元の既定の電子メール アドレスを構成します。  
  
[Windows PowerShell を使用してこの手順を実行する](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
#### <a name="to-configure-notifications"></a>通知を構成するには  
  
1.  Administrators セキュリティ グループのメンバーとしてファイル サーバーにサインインします。  
  
2.  Windows PowerShell コマンド プロンプトで「**Update-FsrmClassificationPropertyDefinition**」と入力してから、Enter キーを押します。 これにより、ドメイン コントローラーで作成されたプロパティ定義がファイル サーバーに同期されます。  
  
3.  ファイル サーバー リソース マネージャーを開きます。 サーバー マネージャーで **[ツール]** をクリックしてから、 **[ファイル サーバー リソース マネージャー]** をクリックします。  
  
4.  **[ファイル サーバー リソース マネージャー (ローカル)]** をクリックしてから、 **[オプションの構成]** をクリックします。  
  
5.  **[電子メールの通知]** タブで次のように構成します。  
  
    -   **[SMTP サーバー名または IP アドレス]** ボックスに、ネットワーク上の SMTP サーバーの名前を入力します。  
  
    -   **[管理者である既定の受信者]** ボックスに、通知を受け取る管理者の電子メール アドレスを入力します。  
  
    -   **[既定の電子メールアドレス]** ボックスに、通知の送信に使用する電子メールアドレスを入力します。  
  
6.  **[OK]** をクリックすると、  
  
![ソリューションガイド](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 書式上の制約のため、複数行にわたって折り返される場合でも、各コマンドレットは 1 行に入力してください。  
  
```  
Set-FsrmSetting -SmtpServer IP address of SMTP server -FromEmailAddress "FromEmailAddress" -AdminEmailAddress "AdministratorEmailAddress"  
```  
  
## <a name="step-3-create-a-file-management-task"></a><a name="BKMK_Step3"></a>手順 3: ファイル管理タスクを作成する  
この手順では、ファイル サーバー リソース マネージャーのコンソールを使用して、月の末日に実行されるファイル管理タスクを作成し、次の条件でファイルを有効期限切れにします。  
  
-   ファイルが訴訟ホールドとして分類されていない。  
  
-   ファイルが長期保持期間を持つものとして分類されている。  
  
-   ファイルが過去 10 年間に変更されていない。  
  
[Windows PowerShell を使用してこの手順を実行する](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)  
  
#### <a name="to-create-a-file-management-task"></a>ファイル管理タスクを作成するには  
  
1.  Administrators セキュリティ グループのメンバーとしてファイル サーバーにサインインします。  
  
2.  ファイル サーバー リソース マネージャーを開きます。 サーバー マネージャーで **[ツール]** をクリックしてから、 **[ファイル サーバー リソース マネージャー]** をクリックします。  
  
3.  **[ファイル管理タスク]** を右クリックし、 **[ファイル管理タスクの作成]** をクリックします。  
  
4.  **[全般]** タブの **[タスク名]** ボックスに、「保持タスク」などのファイル管理タスク名を入力します。  
  
5.  **[スコープ]** タブで **[追加]** をクリックし、この規則に含めるフォルダー (D:\Finance Documents など) を選択します。  
  
6.  **[操作]** タブの **[種類]** ボックスで **[ファイルの有効期限]** をクリックします。 **[有効期限切れのディレクトリ]** ボックスに、有効期限が切れたファイルを移動するローカル ファイル サーバー上のフォルダーのパスを入力します。 このフォルダーには、ファイル サーバー管理者にのみアクセスを許可するアクセス制御リストがなければなりません。  
  
7.  **[通知]** タブで **[追加]** をクリックします。  
  
    -   **[次の管理者に電子メールを送信する]** チェック ボックスを選択します。  
  
    -   **[影響のあるファイルを使用するユーザーに電子メールを送信する]** チェック ボックスを選択してから、 **[OK]** をクリックします。  
  
8.  **[条件]** タブで **[追加]** をクリックし、次のプロパティを追加します。  
  
    -   **[プロパティ]** リストで **[発見可能]** をクリックします。 **[演算子]** リストで **[等しくない]** をクリックします。 **[値]** リストで **[保留]** をクリックします。  
  
    -   **[プロパティ]** リストで **[保有期間]** をクリックします。 **[演算子]** リストで **[等しい]** をクリックします。 **[値]** リストで **[長期]** をクリックします。  
  
9. **[条件]** タブで **[ファイルの最終変更からの日数]** チェック ボックスを選択してから、値を **3650** に設定します。  
  
10. **[スケジュール]** タブで **[毎月]** オプションをクリックしてから、 **[最終]** チェック ボックスを選択します。  
  
11. **[OK]** をクリックすると、  
  
![ソリューションガイド](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 書式上の制約のため、複数行にわたって折り返される場合でも、各コマンドレットは 1 行に入力してください。  
  
```  
$fmjexpiration = New-FSRMFmjAction -Type 'Expiration' -ExpirationFolder folder  
$fmjNotificationAction = New-FsrmFmjNotificationAction -Type Email -MailTo "[FileOwner],[AdminEmail]"  
$fmjNotification = New-FsrmFMJNotification -Days 10 -Action @($fmjNotificationAction)  
$fmjCondition1 = New-FSRMFmjCondition -Property 'Discoverability_MS' -Condition 'NotEqual' -Value "Hold" 
$fmjCondition2 = New-FSRMFmjCondition -Property 'RetentionPeriod_MS' -Condition 'Equal' -Value "Long-term"  
$fmjCondition3 = New-FSRMFmjCondition -Property 'File.DateLastAccessed' -Condition 'Equal' -Value 3650  
$date = get-date  
$schedule = New-FsrmScheduledTask -Time $date -Monthly @(-1)    
$fmj1=New-FSRMFileManagementJob -Name "Retention Task" -Namespace @('D:\Finance Documents') -Action $fmjexpiration -Schedule $schedule -Notification @($fmjNotification) -Condition @( $fmjCondition1, $fmjCondition2, $fmjCondition3)  
```  
  
## <a name="step-4-classify-a-file-manually"></a><a name="BKMK_Step4"></a>手順 4: ファイルを手動で分類する  
この手順では、訴訟ホールドにするファイルを手動で分類します。 このファイルの親フォルダーは、長期保持期間を使用して分類されます。  
  
#### <a name="to-manually-classify-a-file"></a>ファイルを手動で分類するには  
  
1.  Administrators セキュリティ グループのメンバーとしてファイル サーバーにサインインします。  
  
2.  手順 3 で作成したファイル管理タスクのスコープで構成したフォルダーに移動します。  
  
3.  フォルダーを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[分類]** タブで **[保有期間]** をクリックし、 **[長期]** をクリックしてから、 **[OK]** をクリックします。  
  
5.  そのフォルダー内のファイルを右クリックしてから、 **[プロパティ]** をクリックします。  
  
6.  **[分類]** タブで **[発見可能]** をクリックし、 **[保留]** をクリックし、 **[適用]** をクリックしてから、 **[OK]** をクリックします。  
  
7.  ファイル サーバーで、ファイル サーバー リソース マネージャーのコンソールを使用してファイル管理タスクを実行します。 ファイル管理タスクが完了した後に、フォルダーを検査し、ファイルが有効期限切れディレクトリに移動されていないことを確認します。  
  
8.  そのフォルダー内の同じファイルを右クリックしてから、 **[プロパティ]** をクリックします。  
  
9. **[分類]** タブで **[発見可能]** をクリックし、 **[該当なし]** をクリックし、 **[適用]** をクリックしてから、 **[OK]** をクリックします。  
  
10. ファイル サーバーで、ファイル サーバー リソース マネージャーのコンソールを使用してファイル管理タスクを再度実行します。 ファイル管理タスクが完了した後に、フォルダーを検査し、ファイルが有効期限切れディレクトリに移動されたことを確認します。  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>関連項目  
  
-   [シナリオ: ファイルサーバーでの情報の保持を実装する](Scenario--Implement-Retention-of-Information-on-File-Servers.md)  
  
-   [ファイルサーバーの情報の保持を計画する](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)  
  
-   [動的 Access Control: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  
  

