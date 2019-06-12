---
ms.assetid: ee008835-7d3b-4977-adcb-7084c40e5918
title: Deploy Implementing Retention of Information on File Servers (Demonstration Steps)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0acfa6eec1d83c246c43ad32f7548ea771eb3c11
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445761"
---
# <a name="deploy-implementing-retention-of-information-on-file-servers-demonstration-steps"></a>Deploy Implementing Retention of Information on File Servers (Demonstration Steps)

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

ファイル分類インフラストラクチャおよびファイル サーバー リソース マネージャーを使用して、フォルダーの保持期間を設定したり、ファイルを訴訟ホールドにしたりすることができます。  
  
**このドキュメントで**  
  
-   [前提条件](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Prereqs)  
  
-   [ステップ 1: リソース プロパティ定義を作成します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)  
  
-   [手順 2:通知を構成します。](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step2)  
  
-   [手順 3:ファイル管理タスクを作成します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)  
  
-   [手順 4:ファイルを手動で分類します。](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step4)  
  
> [!NOTE]  
> このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
## <a name="prerequisites"></a>前提条件  
このトピックの手順では、SMTP サーバーがファイル有効期限通知用に構成されていることを前提としています。  
  
## <a name="BKMK_Step1"></a>手順 1:リソース プロパティ定義を作成する  
この手順では、Retention Period および Discoverability リソース プロパティを有効にして、ファイル分類インフラストラクチャがこれらのリソース プロパティを使用してネットワーク共有フォルダーでスキャンされたファイルにタグを付けることができるようにします。  
  
[Windows PowerShell を使用してこの手順を実行します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-create-resource-property-definitions"></a>リソース プロパティ定義を作成するには  
  
1.  ドメイン コントローラーで、Domain Admins セキュリティ グループのメンバーとしてサーバーにサインインします。  
  
2.  Active Directory 管理センターを開きます。 サーバー マネージャーで **[ツール]** をクリックしてから、 **[Active Directory 管理センター]** をクリックします。  
  
3.  **[ダイナミック アクセス制御]** を展開してから、 **[リソース プロパティ]** をクリックします。  
  
4.  **[保有期間]** を右クリックし、 **[有効にする]** をクリックします。  
  
5.  **[発見可能]** を右クリックし、 **[有効にする]** をクリックします。  
  
![ソリューション ガイド](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
```  
Set-ADResourceProperty -Enabled:$true -Identity:'CN=RetentionPeriod_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
Set-ADResourceProperty -Enabled:$true -Identity:'CN=Discoverability_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
```  
  
## <a name="BKMK_Step2"></a>手順 2:通知を構成する  
この手順では、ファイル サーバー リソース マネージャーのコンソールを使用して、SMTP サーバー、既定の管理者電子メール アドレス、およびレポート送信元の既定の電子メール アドレスを構成します。  
  
[Windows PowerShell を使用してこの手順を実行します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
#### <a name="to-configure-notifications"></a>通知を構成するには  
  
1.  Administrators セキュリティ グループのメンバーとしてファイル サーバーにサインインします。  
  
2.  Windows PowerShell コマンド プロンプトで「 **Update-FsrmClassificationPropertyDefinition**」と入力してから、Enter キーを押します。 これにより、ドメイン コントローラーで作成されたプロパティ定義がファイル サーバーに同期されます。  
  
3.  ファイル サーバー リソース マネージャーを開きます。 サーバー マネージャーで **[ツール]** をクリックしてから、 **[ファイル サーバー リソース マネージャー]** をクリックします。  
  
4.  **[ファイル サーバー リソース マネージャー (ローカル)]** をクリックしてから、 **[オプションの構成]** をクリックします。  
  
5.  **[電子メールの通知]** タブで次のように構成します。  
  
    -   **[SMTP サーバー名または IP アドレス]** ボックスに、ネットワーク上の SMTP サーバーの名前を入力します。  
  
    -   **[管理者である既定の受信者]** ボックスに、通知を受け取る管理者の電子メール アドレスを入力します。  
  
    -   **既定の「差出人」電子メール アドレス**ボックスに、通知の送信に使用する電子メール アドレスを入力します。  
  
6.  **[OK]** をクリックします。  
  
![ソリューション ガイド](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
```  
Set-FsrmSetting -SmtpServer IP address of SMTP server -FromEmailAddress "FromEmailAddress" -AdminEmailAddress "AdministratorEmailAddress"  
```  
  
## <a name="BKMK_Step3"></a>手順 3:ファイル管理タスクを作成する  
この手順では、ファイル サーバー リソース マネージャーのコンソールを使用して、月の末日に実行されるファイル管理タスクを作成し、次の条件でファイルを有効期限切れにします。  
  
-   ファイルが訴訟ホールドとして分類されていない。  
  
-   ファイルが長期保持期間を持つものとして分類されている。  
  
-   ファイルが過去 10 年間に変更されていない。  
  
[Windows PowerShell を使用してこの手順を実行します。](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)  
  
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
  
11. **[OK]** をクリックします。  
  
![ソリューション ガイド](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
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
  
## <a name="BKMK_Step4"></a>手順 4:ファイルを手動で分類する  
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
  
## <a name="BKMK_Links"></a>参照してください。  
  
-   [シナリオ: ファイル サーバーでの情報の保持の実装](Scenario--Implement-Retention-of-Information-on-File-Servers.md)  
  
-   [ファイル サーバー上の情報の保有期間を計画します。](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)  
  
-   [ダイナミック アクセス制御: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  
  

