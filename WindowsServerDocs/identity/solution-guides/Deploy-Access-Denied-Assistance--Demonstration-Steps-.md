---
ms.assetid: b035e9f8-517f-432a-8dfb-40bfc215bee5
title: "アクセス拒否アシスタンス (デモンストレーション手順) の展開します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5201441ba884fe4658b917919e60c7d20530341b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-access-denied-assistance-demonstration-steps"></a>アクセス拒否アシスタンス (デモンストレーション手順) の展開します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、アクセス拒否アシスタンスを構成し、正しく機能していることを確認する方法について説明します。  
  
**このドキュメントで**  
  
-   [手順 1: アクセス拒否アシスタンスを構成します。](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_1)  
  
-   [手順 2: 電子メール通知設定を構成します。](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_2)  
  
-   [手順 3: は、アクセス拒否アシスタンスが正しく構成されていることを確認します。](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_3)  
  
> [!NOTE]  
> このトピックには、説明する手順の一部を自動化するのに使用できるサンプル Windows PowerShell コマンドレットが含まれています。 詳細については、次を参照してください。[コマンドレットを使用した](https://go.microsoft.com/fwlink/p/?linkid=230693)します。  
  
## <a name="BKMK_1"></a>手順 1: アクセス拒否アシスタンスを構成します。  
グループ ポリシーを使用して、ドメイン内でアクセス拒否アシスタンスを構成することができますか、アシスタンスをファイル サーバー リソース マネージャーのコンソールを使用してファイル サーバーごとに個別に構成できます。 ファイル サーバー上の特定の共有フォルダーのアクセス拒否メッセージを変更することもできます。  
  
次のようにグループ ポリシーを使用して、ドメインのアクセス拒否アシスタンスを構成できます。  
  
[Do this step using Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-configure-access-denied-assistance-by-using-group-policy"></a>グループ ポリシーを使用してアクセス拒否アシスタンスを構成するには  
  
1.  グループ ポリシーの管理。 サーバー マネージャーで、クリックして**ツール**、] をクリックし、**グループ ポリシーの管理**します。  
  
2.  適切なグループ ポリシーを右クリックし、をクリックして**編集**します。  
  
3.  をクリックして**コンピューターの構成**、] をクリックして**ポリシー**、] をクリックして**管理用テンプレート**、] をクリックして**システム**、] をクリックし、**アクセス拒否アシスタンス**します。  
  
4.  右クリック**アクセス拒否エラーのメッセージをカスタマイズする**、] をクリックし、**編集**します。  
  
5.  選択、**有効**オプションです。  
  
6.  次のオプションを構成します。  
  
    1.  **アクセスが拒否されたユーザーに、次のメッセージを表示**ボックスに、ユーザーがファイルまたはフォルダーへのアクセスが拒否されたときに表示されるメッセージを入力します。  
  
        マクロは、カスタマイズしたテキストを挿入するメッセージを追加できます。 マクロは次のとおりです。  
  
        -   **[Original File Path]**ユーザーによってアクセスされた元のファイル パス。  
  
        -   **[Original File Path Folder]**ユーザーによってアクセスされた元のファイル パスの親フォルダー。  
  
        -   **[Admin Email]**管理者の電子メール受信者リスト。  
  
        -   **[Data Owner Email]**データ所有者の電子メール受信者リスト。  
  
    2.  選択、**アシスタンスを要求するユーザーを有効にする**チェック ボックスをオンします。  
  
    3.  残りの既定の設定をそのまま使用します。  
  
![ソリューション ガイド](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。  
  
```  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName AllowEmailRequests -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName GenerateLog -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName IncludeDeviceClaims -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName IncludeUserClaims -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName PutAdminOnTo -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName PutDataOwnerOnTo -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName ErrorMessage -Type MultiString -value "Type the text that the user will see in the error message dialog box."  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName Enabled -Type DWORD -value 1 
  
```  
  
または、ファイル サーバー リソース マネージャーのコンソールを使用して各ファイル サーバーには個別にアクセス拒否アシスタンスを構成できます。  
  
[Do this step using Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1a)  
  
#### <a name="to-configure-access-denied-assistance-by-using-file-server-resource-manager"></a>ファイル サーバー リソース マネージャーを使用してアクセス拒否アシスタンスを構成するには  
  
1.  ファイル サーバー リソース マネージャーを開きます。 In Server Manager, click **Tools**, and then click **File Server Resource Manager**.  
  
2.  右クリック**ファイル サーバー リソース マネージャー (ローカル)**、] をクリックし、**オプションの構成**します。  
  
3.  をクリックして、**アクセス拒否アシスタンス**] タブ。  
  
4.  選択、**アクセス拒否アシスタンスを有効にする**チェック ボックスをオンします。  
  
5.  **フォルダーまたはファイルへのアクセスが拒否されたユーザーに、次のメッセージを表示**ボックスに、ユーザーがファイルまたはフォルダーへのアクセスが拒否されたときに表示されるメッセージを入力します。  
  
    マクロは、カスタマイズしたテキストを挿入するメッセージを追加できます。 マクロは次のとおりです。  
  
    -   **[Original File Path]**ユーザーによってアクセスされた元のファイル パス。  
  
    -   **[Original File Path Folder]**ユーザーによってアクセスされた元のファイル パスの親フォルダー。  
  
    -   **[Admin Email]**管理者の電子メール受信者リスト。  
  
    -   **[Data Owner Email]**データ所有者の電子メール受信者リスト。  
  
6.  をクリックして**電子メール要求の構成**を選択、**アシスタンスを要求するユーザーを有効にする**チェック ボックスをオンにし**OK**します。  
  
7.  をクリックして**プレビュー**エラー メッセージがユーザーにどのように表示する場合。  
  
8.  をクリックして**OK**します。  
  
![ソリューション ガイド](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。
  
```  
Set-FSRMAdrSetting -Event "AccessDenied" -DisplayMessage "Type the text that the user will see in the error message dialog box." -Enabled:$true -AllowRequests:$true  
```  
  
アクセス拒否アシスタンスを構成した後、グループ ポリシーを使用して有効すべてのファイルの種類の必要があります。  
  
[Do this step using Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1c)  
  
#### <a name="to-configure-access-denied-assistance-for-all-file-types-by-using-group-policy"></a>グループ ポリシーを使用してすべてのファイルの種類についてアクセス拒否アシスタンスを構成するには  
  
1.  グループ ポリシーの管理。 サーバー マネージャーで、クリックして**ツール**、] をクリックし、**グループ ポリシーの管理**します。  
  
2.  適切なグループ ポリシーを右クリックし、をクリックして**編集**します。  
  
3.  をクリックして**コンピューターの構成**、] をクリックして**ポリシー**、] をクリックして**管理用テンプレート**、] をクリックして**システム**、] をクリックし、**アクセス拒否アシスタンス**します。  
  
4.  右クリック**すべてのファイルの種類については、クライアントでアクセス拒否アシスタンスを有効にする**、] をクリックし、**編集**します。  
  
5.  をクリックして**有効**、] をクリックし、**OK**します。  
  
![ソリューション ガイド](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。 
  
```  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Explore" -ValueName EnableShellExecuteFileStreamCheck -Type DWORD -value 1  
  
```  
  
ファイル サーバー リソース マネージャーのコンソールを使用して、ファイル サーバー上の各共有フォルダーは個別のアクセス拒否メッセージも指定できます。  
  
[Do this step using Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1b)  
  
#### <a name="to-specify-a-separate-access-denied-message-for-a-shared-folder-by-using-file-server-resource-manager"></a>ファイル サーバー リソース マネージャーを使用して別の共有フォルダーのアクセス拒否メッセージを指定するには  
  
1.  ファイル サーバー リソース マネージャーを開きます。 In Server Manager, click **Tools**, and then click **File Server Resource Manager**.  
  
2.  展開**ファイル サーバー リソース マネージャー (ローカル)**、] をクリックし、**分類管理**します。  
  
3.  右クリック**分類プロパティ**、] をクリックし、**フォルダー管理プロパティの設定**します。  
  
4.  **プロパティ**ボックスで、をクリックして**アクセス拒否アシスタンス メッセージ**、] をクリックし、**追加**します。  
  
5.  をクリックして**参照**、カスタム アクセス拒否メッセージを持つ必要があるフォルダーを選択します。  
  
6.  **値**ボックスに、そのフォルダー内のリソースにアクセスすることはできないときに、ユーザーに表示されるメッセージを入力します。  
  
    マクロは、カスタマイズしたテキストを挿入するメッセージを追加できます。 マクロは次のとおりです。  
  
    -   **[Original File Path]**ユーザーによってアクセスされた元のファイル パス。  
  
    -   **[Original File Path Folder]**ユーザーによってアクセスされた元のファイル パスの親フォルダー。  
  
    -   **[Admin Email]**管理者の電子メール受信者リスト。  
  
    -   **[Data Owner Email]**データ所有者の電子メール受信者リスト。  
  
7.  をクリックして**OK**、] をクリックし、**閉じる**します。  
  
![ソリューション ガイド](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。 
  
```  
Set-FSRMMgmtProperty -Namespace "folder path" -Name "AccessDeniedMessage_MS" -Value "Type the text that the user will see in the error message dialog box."  
```  
  
## <a name="BKMK_2"></a>手順 2: 電子メール通知設定を構成します。  
アクセス拒否アシスタンス メッセージを送信する各ファイル サーバーで電子メール通知設定を構成する必要があります。  
  
[Do this step using Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
1.  ファイル サーバー リソース マネージャーを開きます。 In Server Manager, click **Tools**, and then click **File Server Resource Manager**.  
  
2.  右クリック**ファイル サーバー リソース マネージャー (ローカル)**、] をクリックし、**オプションの構成**します。  
  
3.  をクリックして、**電子メール通知**] タブ。  
  
4.  次の設定を構成します。  
  
    -   **SMTP サーバー名または IP アドレス**ボックスに、組織内の SMTP サーバーの IP アドレスの名前を入力します。  
  
    -   **既定の管理者の受信者**と**既定の '電子メール アドレスのから'**ボックスに、ファイル サーバー管理者の電子メール アドレスを入力します。  
  
5.  をクリックして**テスト電子メールの送信**に電子メール通知が正しく構成されていることを確認します。  
  
6.  をクリックして**OK**します。  
  
![ソリューション ガイド](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。
  
```  
set-FSRMSetting -SMTPServer "server1" -AdminEmailAddress "fileadmin@contoso.com" -FromEmailAddress "fileadmin@contoso.com"  
```  
  
## <a name="BKMK_3"></a>手順 3: は、アクセス拒否アシスタンスが正しく構成されていることを確認します。  
共有へのアクセスがない共有またはファイルにアクセスしようと Windows 8 を実行しているユーザーによってアクセス拒否アシスタンスが正しく構成されているを確認することができます。 ときに、アクセス拒否メッセージが表示されたら、ユーザーに表示する必要があります、**サポートの要求**ボタンをクリックします。 サポートの要求] ボタンをクリックすると、ユーザーがアクセスする理由を指定し、フォルダー所有者またはファイル サーバー管理者に電子メールを送信できます。 フォルダーの所有者またはファイル サーバー管理者は、電子メールが到着し、適切な詳細が含まれてするを確認できます。  
  
> [!IMPORTANT]  
> Windows Server 2012 を実行しているユーザーを使用してアクセス拒否アシスタンスを確認する場合、ファイル共有に接続する前にデスクトップ エクスペリエンスをインストールする必要があります。  
  
## <a name="BKMK_Links"></a>参照してください。  
  
-   [シナリオ: アクセス拒否アシスタンス](Scenario--Access-Denied-Assistance.md)  
  
-   [アクセス拒否アシスタンスを計画します。](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)  
  
-   [ダイナミック アクセス制御: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  
  

