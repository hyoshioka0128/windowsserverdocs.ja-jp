---
title: 共有フォルダーのカスタマイズ
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47bc4986-14eb-4a29-9930-83a25704a3a0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 552a76ba9c2ff385f1ff09d4869eaeb6613027a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823473"
---
# <a name="customize-shared-folders"></a>共有フォルダーのカスタマイズ

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

既定では、サーバー フォルダーはディスク 0 の最大のデータ パーティションに作成されます。 パートナーは次の手順で、場所をカスタマイズし、追加のサーバー フォルダーを指定できます。  
  
1.  カスタム パーティション構成を使用して、工場出荷時イメージを作成し、sysprep を使用する前に新しい Storage レジストリ キーを作成します。 初期構成 (IC) 中に、記憶域の IC タスクがこのレジストリ キーを確認します。 レジストリ キーが存在する場合、既定のサーバー フォルダーが C:\ServerFolders ディレクトリに作成されます。  
  
    #### <a name="to-create-a-new-storage-registry-key"></a>新しい Storage レジストリ キーを作成するには  
  
    1.  サーバーで、カーソルを画面の右上隅に移動して、**[検索]** をクリックします。  
  
    2.  検索ボックスに「**regedit**」と入力して、**[Regedit]** アプリケーションをクリックします。  
  
    3.  ナビゲーション ウィンドウで、**[HKEY_LOCAL_MACHINE]**、**[SOFTWARE]**、**[Microsoft]** の順に展開します。  
  
    4.  **[Windows Server]** を右クリックし、**[新規]** をクリックし、**[キー]** をクリックします。  
  
    5.  キーの名前を「**Storage**」にします。  
  
    6.  ナビゲーション ウィンドウで、新しい **Storage**レジストリ キーを右クリックし、**[DWORD (32 ビット) 値]** をクリックします。  
  
    7.  文字列の名前を「**CreateFoldersOnSystem**」にします。  
  
    8.  **[CreateFoldersOnSystem]** を右クリックし、**[修正]** をクリックします。 **[文字列の編集]** ダイアログ ボックスが表示されます。  
  
    9. この新しいキーの値を **1** に設定し、**[OK]** をクリックします。  
  
2.  PostIC.cmd スクリプトを使用して、フォルダーを別の場所に移動するか、追加のフォルダーを作成します。 次の例を参照してください。[例 1:カスタム フォルダーを作成し、Windows PowerShell を使用して、既定のフォルダーを PostIC.cmd から新しい場所に移動](Customize-Shared-Folders.md#BKMK_Example1)します。  
  
3.  Windows Server Solutions SDK を使用して、フォルダーを別の場所に移動するか、追加のフォルダーを作成します。 次の例を参照してください。[例 2:カスタム フォルダーを作成し、Windows Server Solutions SDK を使用して既存のフォルダーを移動](Customize-Shared-Folders.md#BKMK_Example2)します。  
  
 パートナーは必要に応じてデータ フォルダーをドライブ C に残しておくことができます。これにより、エンド ユーザーまたは再販業者はデータ ドライブのデータ フォルダーのレイアウトを決定できるようになります。  
  
###  <a name="BKMK_Example1"></a> 例 1:Windows PowerShell を使用して、カスタム フォルダーを作成し、既定のフォルダーを PostIC.cmd から新しい場所に移動する  
  
1.  「 [Create the PostIC.cmd File for Running Post Initial Configuration Tasks](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md) 」セクションの説明に従って、初期構成後のタスクを実行するための PostIC.cmd ファイルを作成します。  
  
2.  メモ帳を使用して、 **customizefolders.ps1** という名前のファイルを C:\Windows\Setup\Scripts フォルダー内に作成し、次の Windows PowerShell® コマンドをファイルに貼り付けます (目的の動作に応じて該当する行のマークを解除します)。  
  
    ```  
    # Move the Documents folder to D:\ServerFolders  
    #Get-WssFolder -name Documents| Move-WssFolder - NewDrive D:\ -Force  
  
    # Check for last error. If last error is not null, exit with return code 1  
    #If ($error[0] -ne $null) { exit 1}   
  
    # Move all folders to D:\ServerFolders  
    #foreach( $folder in Get-WssFolder )  
    #{  
    #    Move-WssFolder $folder -NewDrive D:\ -Force  
    #}  
  
    # Check for last error. If last error is not null, exit with return code 1  
    #If ($error[0] -ne $null) { exit 1}   
  
    # Create a custom folder named Custom Folder  
    #Add-WssFolder -Name CustomFolder -Path D:\ServerFolders\CustomFolder -Description "Custom Folder"  
  
    # Check for last error. If last error is not null, exit with return code 1  
    #If ($error[0] -ne $null) { exit 1}   
  
    exit 0  
    ```  
  
3.  このスクリプトを実行するために、PostIC.cmd ファイルに次の行を追加します。  
  
    ```  
    REM Lower the execution policy  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy RemoteSigned"  
  
    REM Execute the folder customization script  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" -NoProfile -Noninteractive -command ". %windir%\setup\scripts\customizefolders.ps1;exit $LASTEXITCODE"  
    Set error_level=%ERRORLEVEL%  
  
    REM Restore the execution policy to default  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy Restricted"  
    Set ERRORLEVEL=%error_level%  
    ```  
  
###  <a name="BKMK_Example2"></a> 例 2:Windows Server Solutions SDK を使用して、カスタム フォルダーを作成し、既存のフォルダーを移動する  
 作成したコードは、実行可能ファイルとしてコンパイルし、PostIC.cmd ファイルから呼び出すか、インストール済みのアドインから直接呼び出すことができます。  
  
```  
static void Main(string[] args)  
{  
 StorageManager storageManager = new StorageManager();  
 //Connect to the StorageManager  
 storageManager.Connect();  
  
 //Move the Documents folder to D:\ServerFolders  
 Folder targetFolder = storageManager.Folders.First(folder => folder.Name == "Documents");  
  
 MoveFolderRequest moveRequest = targetFolder.GetMoveRequest(@"D:\");  
 moveRequest.MoveFolder();  
  
 //Verify operation was successful, if so print result  
 if (moveRequest.Status == OperationStatus.Succeeded)  
 {  
  Console.WriteLine("Folder {0} now located at {1}", targetFolder.Name, targetFolder.Path);  
 }  
  
 string newFolderName = "New Custom Folder";  
 string newFolderLocation = @"C:\ServerFolders\New Custom Folder";  
  
 //Create add request based with specific name and location  
 CreateFolderRequest request = storageManager.GetCreateFolderRequest(newFolderName, newFolderLocation);  
  
 //Give Guest user read only permission to folder  
 request.PermissionsByName.Add(new NamePermission("Guest", Permission.ReadOnly));  
  
 //Create the new folders  
 request.CreateFolder();  
  
 //Verify operation was successful, if so print result  
 if( request.Status == OperationStatus.Succeeded)  
 {  
  Folder newFolder = storageManager.Folders.First(folder => folder.Path == newFolderLocation);  
  
  Console.WriteLine("Folder {0} created at {1}", newFolder.Name, newFolder.Path);  
 }  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)
