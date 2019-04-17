---
title: "共有フォルダーをカスタマイズします。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: bcdd43183512bb225dd4afa916f2782c6eb79d7e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="customize-shared-folders"></a>共有フォルダーをカスタマイズします。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

既定では、サーバー フォルダーはディスク 0 の最大のデータ パーティションに作成されます。 パートナーは、場所をカスタマイズおよび、次の手順を使用して追加のサーバー フォルダーを指定できます。  
  
1.  カスタム パーティション構成を使用して、工場出荷時イメージを作成し、sysprep を使用する前に新しい Storage レジストリ キーを作成します。 初期構成 (IC) 中に、記憶域の IC タスクは、このレジストリ キーを確認します。 存在する場合、既定のサーバー フォルダーが C:\ServerFolders ディレクトリに作成されます。  
  
    #### <a name="to-create-a-new-storage-registry-key"></a>新しい Storage レジストリ キーを作成するには  
  
    1.  サーバーで、マウスを移動して、画面の右上隅とクリックして**検索**します。  
  
    2.  検索ボックスに次のように入力します。**regedit**、クリックして、**Regedit**アプリケーション。  
  
    3.  ナビゲーション ウィンドウで [ **HKEY_LOCAL_MACHINE**、展開**ソフトウェア**、し、展開**Microsoft**します。  
  
    4.  右クリック**Windows Server**、] をクリックして**新規**、] をクリックし、**キー**します。  
  
    5.  キーの名前**記憶域**します。  
  
    6.  新しい Storage レジストリ キーをクリックを右クリックし、ナビゲーション ウィンドウで、**新規**、] をクリックし、**DWORD (32 ビット) 値**します。  
  
    7.  文字列の名前**CreateFoldersOnSystem**します。  
  
    8.  右クリック**CreateFoldersOnSystem**、] をクリックし、**変更**します。 **文字列の編集**] ダイアログ ボックスが表示されます。  
  
    9. この新しいキーの値を設定**1**、] をクリックし、**[OK]**します。  
  
2.  PostIC.cmd スクリプトを使用して、フォルダーを別の場所に移動するか、追加のフォルダーを作成します。 次の例を参照してください:[例 1: カスタム フォルダーを作成し、Windows PowerShell を使用して、PostIC.cmd から新しい場所に、既定のフォルダーを移動](Customize-Shared-Folders.md#BKMK_Example1)します。  
  
3.  Windows Server Solutions SDK を使用して、フォルダーを別の場所に移動するか、追加のフォルダーを作成します。 次の例を参照してください:[例 2: カスタム フォルダーを作成し、Windows Server Solutions SDK を使用して、既存のフォルダーを移動](Customize-Shared-Folders.md#BKMK_Example2)します。  
  
 パートナーが C ドライブにデータ フォルダーを置くことが必要に応じて、これにより、エンド ユーザーまたは再販業者はデータ ドライブのデータ フォルダーのレイアウトを決定できます。  
  
###  <a name="BKMK_Example1"></a>例 1: は、カスタム フォルダーを作成し、Windows PowerShell を使用して、PostIC.cmd から新しい場所に、既定のフォルダーを移動  
  
1.  詳述するよう post 初期構成タスクを実行するための PostIC.cmd ファイルを作成、[PostIC.cmd ファイルを作成する [初期構成の投稿を実行しているタスク](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md)セクションです。  
  
2.  という名前のファイルを作成してメモ帳を使って**customizefolders.ps1** C:\Windows\Setup\Scripts フォルダー、および次 Windows PowerShell® コマンド ファイルを貼り付けて (目的の動作に応じて該当する行のマークを解除) します。  
  
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
  
3.  PostIC.cmd ファイルをこのスクリプトを実行するには、次の行を追加します。  
  
    ```  
    REM Lower the execution policy  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy RemoteSigned"  
  
    REM Execute the folder customization script  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" -NoProfile -Noninteractive -command ". %windir%\setup\scripts\customizefolders.ps1;exit $LASTEXITCODE"  
    Set error_level=%ERRORLEVEL%  
  
    REM Restore the execution policy to deafult  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy Restricted"  
    Set ERRORLEVEL=%error_level%  
    ```  
  
###  <a name="BKMK_Example2"></a>例 2: カスタム フォルダーを作成し、Windows Server Solutions SDK を使用して、既存のフォルダーを移動します。  
 作成するコード、実行可能ファイルとしてコンパイルしし、PostIC.cmd ファイルから呼び出すかにインストールされているアドインから直接呼び出すなります。  
  
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
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)