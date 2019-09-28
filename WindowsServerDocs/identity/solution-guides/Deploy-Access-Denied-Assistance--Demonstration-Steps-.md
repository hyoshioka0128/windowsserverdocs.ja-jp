---
ms.assetid: b035e9f8-517f-432a-8dfb-40bfc215bee5
title: Deploy Access-Denied Assistance (Demonstration Steps)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: afc05f395753e5c5614e92d109d71e05980d5d92
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407176"
---
# <a name="deploy-access-denied-assistance-demonstration-steps"></a>Deploy Access-Denied Assistance (Demonstration Steps)

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、アクセス拒否アシスタンスを構成し、それが正しく機能していることを確認する方法について説明します。  
  
**このドキュメントの説明**  
  
-   [ステップ 1: アクセス拒否アシスタンスを構成する @ no__t-0  
  
-   [手順 2:電子メール通知の設定を構成する @ no__t-0  
  
-   [手順 3:アクセス拒否アシスタンスが正しく構成されていることを確認する @ no__t-0  
  
> [!NOTE]  
> このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
## <a name="BKMK_1"></a>手順 1:アクセス拒否アシスタンスを構成する  
グループ ポリシーを使用して、ドメイン内でアクセス拒否アシスタンスを構成できます。あるいは、ファイル サーバー リソース マネージャーのコンソールを使用して、ファイル サーバーごとに個別にアシスタンスを構成できます。 ファイル サーバー上の特定の共有フォルダーのアクセス拒否メッセージを変更することもできます。  
  
次のようにグループ ポリシーを使用して、ドメインのアクセス拒否アシスタンスを構成できます。  
  
[Windows PowerShell を使用してこの手順を実行する](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-configure-access-denied-assistance-by-using-group-policy"></a>グループ ポリシーを使用してアクセス拒否アシスタンスを構成するには  
  
1.  グループ ポリシーの管理を開きます。 サーバー マネージャーで、 **[ツール]** をクリックし、 **[グループ ポリシーの管理]** をクリックします。  
  
2.  該当するグループ ポリシーを右クリックしてから、 **[編集]** をクリックします。  
  
3.  **[コンピューターの構成]** をクリックし、 **[ポリシー]** をクリックし、 **[管理用テンプレート]** をクリックし、 **[システム]** をクリックしてから、 **[アクセス拒否アシスタンス]** をクリックします。  
  
4.  **[アクセス拒否エラーのメッセージをカスタマイズする]** を右クリックしてから、 **[編集]** をクリックします。  
  
5.  **[有効]** オプションを選択します。  
  
6.  次のオプションを構成します。  
  
    1.  **[アクセスが拒否されたユーザーに次のメッセージを表示する]** ボックスに、ファイルまたはフォルダーへのアクセスが拒否されたときにユーザーに表示されるメッセージを入力します。  
  
        カスタマイズしたテキストを挿入するマクロをメッセージに追加できます。 マクロには次のものが含まれています。  
  
        -   **[Original File Path]** ユーザーによってアクセスされた元のファイル パス。  
  
        -   **[Original File Path Folder]** ユーザーによってアクセスされた元のファイル パスの親フォルダー。  
  
        -   **[Admin Email]** 管理者の電子メール受信者リスト。  
  
        -   **[Data Owner Email]** データ所有者の電子メール受信者リスト。  
  
    2.  **[ユーザーがアシスタントを依頼できるようにする]** チェック ボックスを選択します。  
  
    3.  残りの既定の設定をそのままにします。  
  
@no__t 0solution ガイド](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
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
  
あるいは、ファイル サーバー リソース マネージャーのコンソールを使用して、ファイル サーバーごとに個別にアクセス拒否アシスタンスを構成できます。  
  
[Windows PowerShell を使用してこの手順を実行する](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1a)  
  
#### <a name="to-configure-access-denied-assistance-by-using-file-server-resource-manager"></a>ファイル サーバー リソース マネージャーを使用してアクセス拒否アシスタンスを構成するには  
  
1.  ファイル サーバー リソース マネージャーを開きます。 サーバー マネージャーで **[ツール]** をクリックしてから、 **[ファイル サーバー リソース マネージャー]** をクリックします。  
  
2.  **[ファイル サーバー リソース マネージャー (ローカル)]** をクリックしてから、 **[オプションの構成]** をクリックします。  
  
3.  **[アクセス拒否アシスタンス]** タブをクリックします。  
  
4.  **[アクセス拒否アシスタンスを有効にする]** チェック ボックスを選択します。  
  
5.  **[フォルダーまたはファイルへのアクセスが拒否されたユーザーに次のメッセージを表示]** ボックスに、ファイルまたはフォルダーへのアクセスが拒否されたときにユーザーに表示されるメッセージを入力します。  
  
    カスタマイズしたテキストを挿入するマクロをメッセージに追加できます。 マクロには次のものが含まれています。  
  
    -   **[Original File Path]** ユーザーによってアクセスされた元のファイル パス。  
  
    -   **[Original File Path Folder]** ユーザーによってアクセスされた元のファイル パスの親フォルダー。  
  
    -   **[Admin Email]** 管理者の電子メール受信者リスト。  
  
    -   **[Data Owner Email]** データ所有者の電子メール受信者リスト。  
  
6.  **[電子メール要求の構成]** をクリックし、 **[ユーザーがアシスタンスを依頼できるようにする]** チェック ボックスを選択してから、 **[OK]** をクリックします。  
  
7.  エラー メッセージがユーザーにどのように表示されるのかを確認する場合は、 **[プレビュー]** をクリックします。  
  
8.  **[OK]** をクリックします。  
  
@no__t 0solution ガイド](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。
  
```  
Set-FSRMAdrSetting -Event "AccessDenied" -DisplayMessage "Type the text that the user will see in the error message dialog box." -Enabled:$true -AllowRequests:$true  
```  
  
アクセス拒否アシスタンスを構成した後に、グループ ポリシーを使用して、すべてのファイルの種類に対してアクセス拒否アシスタンスを有効にする必要があります。  
  
[Windows PowerShell を使用してこの手順を実行する](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1c)  
  
#### <a name="to-configure-access-denied-assistance-for-all-file-types-by-using-group-policy"></a>グループ ポリシーを使用してすべてのファイルの種類に対してアクセス拒否アシスタンスを構成するには  
  
1.  グループ ポリシーの管理を開きます。 サーバー マネージャーで、 **[ツール]** をクリックし、 **[グループ ポリシーの管理]** をクリックします。  
  
2.  該当するグループ ポリシーを右クリックしてから、 **[編集]** をクリックします。  
  
3.  **[コンピューターの構成]** をクリックし、 **[ポリシー]** をクリックし、 **[管理用テンプレート]** をクリックし、 **[システム]** をクリックしてから、 **[アクセス拒否アシスタンス]** をクリックします。  
  
4.  **[クライアントですべてのファイルの種類についてアクセス拒否アシスタンスを有効にする]** を右クリックしてから、 **[編集]** をクリックします。  
  
5.  **[有効]** をクリックし、 **[OK]** をクリックします。  
  
@no__t 0solution ガイド](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。 
  
```  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Explore" -ValueName EnableShellExecuteFileStreamCheck -Type DWORD -value 1  
  
```  
  
ファイル サーバー リソース マネージャーのコンソールを使用して、ファイル サーバー上の共有フォルダーごとに個別のアクセス拒否メッセージを指定することもできます。  
  
[Windows PowerShell を使用してこの手順を実行する](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1b)  
  
#### <a name="to-specify-a-separate-access-denied-message-for-a-shared-folder-by-using-file-server-resource-manager"></a>ファイル サーバー リソース マネージャーを使用して共有フォルダーに個別のアクセス拒否メッセージを指定するには  
  
1.  ファイル サーバー リソース マネージャーを開きます。 サーバー マネージャーで **[ツール]** をクリックしてから、 **[ファイル サーバー リソース マネージャー]** をクリックします。  
  
2.  **[ファイル サーバー リソース マネージャー (ローカル)]** を展開してから、 **[分類管理]** をクリックします。  
  
3.  **[分類プロパティ]** を右クリックしてから、 **[フォルダー管理プロパティの設定]** をクリックします。  
  
4.  **[プロパティ]** ボックスで **[アクセス拒否アシスタンス メッセージ]** をクリックしてから、 **[追加]** をクリックします。  
  
5.  **[参照]** をクリックしてから、カスタム アクセス拒否メッセージが必要なフォルダーを選択します。  
  
6.  **[値]** ボックスに、当該フォルダー内のリソースにアクセスできない場合にユーザーに表示するメッセージを入力します。  
  
    カスタマイズしたテキストを挿入するマクロをメッセージに追加できます。 マクロには次のものが含まれています。  
  
    -   **[Original File Path]** ユーザーによってアクセスされた元のファイル パス。  
  
    -   **[Original File Path Folder]** ユーザーによってアクセスされた元のファイル パスの親フォルダー。  
  
    -   **[Admin Email]** 管理者の電子メール受信者リスト。  
  
    -   **[Data Owner Email]** データ所有者の電子メール受信者リスト。  
  
7.  **[OK]** をクリックし、 **[閉じる]** をクリックします。  
  
@no__t 0solution ガイド](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。 
  
```  
Set-FSRMMgmtProperty -Namespace "folder path" -Name "AccessDeniedMessage_MS" -Value "Type the text that the user will see in the error message dialog box."  
```  
  
## <a name="BKMK_2"></a>手順 2:電子メール通知設定を構成する  
アクセス拒否アシスタンス メッセージを送信するファイル サーバーごとに電子メール通知設定を構成する必要があります。  
  
[Windows PowerShell を使用してこの手順を実行する](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
1.  ファイル サーバー リソース マネージャーを開きます。 サーバー マネージャーで **[ツール]** をクリックしてから、 **[ファイル サーバー リソース マネージャー]** をクリックします。  
  
2.  **[ファイル サーバー リソース マネージャー (ローカル)]** をクリックしてから、 **[オプションの構成]** をクリックします。  
  
3.  **[電子メールの通知]** タブをクリックします。  
  
4.  次の設定を構成します。  
  
    -   **[SMTP サーバー名または IP アドレス]** ボックスに、組織内の SMTP サーバーの IP アドレスの名前を入力します。  
  
    -   管理者の **[既定の受信]** 者 と **[既定の電子メールアドレス]** ボックスに、ファイルサーバー管理者の電子メールアドレスを入力します。  
  
5.  **[テスト電子メールの送信]** をクリックして、電子メール通知が正しく構成されていることを確認します。  
  
6.  **[OK]** をクリックします。  
  
@no__t 0solution ガイド](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。
  
```  
set-FSRMSetting -SMTPServer "server1" -AdminEmailAddress "fileadmin@contoso.com" -FromEmailAddress "fileadmin@contoso.com"  
```  
  
## <a name="BKMK_3"></a>手順 3:アクセス拒否アシスタンスが正しく構成されていることを確認する  
アクセス拒否アシスタンスが正しく構成されていることを確認するには、Windows 8 を実行しているユーザーが、アクセス権のない共有またはその共有内のファイルにアクセスしようとします。 アクセス拒否メッセージが表示された場合、ユーザーには、 **[サポートの要求]** ボタンが表示されます。 [サポートの要求] ボタンをクリックすると、ユーザーは、アクセス理由を指定してから、フォルダー所有者またはファイル サーバー管理者に電子メールを送信できます。 フォルダー所有者またはファイル サーバー管理者は、到着した電子メールに適切な詳細が含まれているかを確認できます。  
  
> [!IMPORTANT]  
> Windows Server 2012 を実行しているユーザーを使用してアクセス拒否アシスタンスを確認する場合は、ファイル共有に接続する前にデスクトップエクスペリエンスをインストールする必要があります。  
  
## <a name="BKMK_Links"></a>関連項目  
  
-   [シナリオ: アクセス拒否アシスタンス](Scenario--Access-Denied-Assistance.md)  
  
-   [アクセス拒否アシスタンスの計画](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)  
  
-   [ダイナミック アクセス制御: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  
  

