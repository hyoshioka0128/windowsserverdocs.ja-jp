---
title: 共有フォルダーのカスタマイズ
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 47bc4986-14eb-4a29-9930-83a25704a3a0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 861107035408fc39d0dc5e4d94a4d82d8dfba74e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818075"
---
# <a name="customize-shared-folders"></a>共有フォルダーのカスタマイズ

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

既定では、サーバー フォルダーはディスク 0 の最大のデータ パーティションに作成されます。 パートナーは次の手順で、場所をカスタマイズし、追加のサーバー フォルダーを指定できます。  
  
1. カスタム パーティション構成を使用して、工場出荷時イメージを作成し、sysprep を使用する前に新しい Storage レジストリ キーを作成します。 初期構成 (IC) 中に、記憶域の IC タスクがこのレジストリ キーを確認します。 レジストリ キーが存在する場合、既定のサーバー フォルダーが C:\ServerFolders ディレクトリに作成されます。  
  
   #### <a name="to-create-a-new-storage-registry-key"></a>新しい Storage レジストリ キーを作成するには  
  
   1.  サーバーで、カーソルを画面の右上隅に移動して、 **[検索]** をクリックします。  
  
   2.  検索ボックスに「**regedit**」と入力して、 **[Regedit]** アプリケーションをクリックします。  
  
   3.  ナビゲーション ウィンドウで、 **[HKEY_LOCAL_MACHINE]** 、 **[SOFTWARE]** 、 **[Microsoft]** の順に展開します。  
  
   4.  **[Windows Server]** を右クリックし、 **[新規]** をクリックし、 **[キー]** をクリックします。  
  
   5.  キーの名前を「**Storage**」にします。  
  
   6.  ナビゲーション ウィンドウで、新しい **Storage** レジストリ キーを右クリックし、 **[DWORD (32 ビット) 値]** をクリックします。  
  
   7.  文字列の名前を「**CreateFoldersOnSystem**」にします。  
  
   8.  **[CreateFoldersOnSystem]** を右クリックし、 **[修正]** をクリックします。 **[文字列の編集]** ダイアログ ボックスが表示されます。  
  
   9. この新しいキーの値を **1** に設定し、 **[OK]** をクリックします。  
  
2. PostIC.cmd スクリプトを使用して、フォルダーを別の場所に移動するか、追加のフォルダーを作成します。 例については、「[例 1: Windows PowerShell を使用して、カスタム フォルダーを作成し、既定のフォルダーを PostIC.cmd から新しい場所に移動する](Customize-Shared-Folders.md#BKMK_Example1)」を参照してください。  
  
3. Windows Server Solutions SDK を使用して、フォルダーを別の場所に移動するか、追加のフォルダーを作成します。 例については、「[例 2: Windows Server Solutions SDK を使用して、カスタム フォルダーを作成し、既存のフォルダーを移動する](Customize-Shared-Folders.md#BKMK_Example2)」を参照してください。  
  
   パートナーは必要に応じてデータ フォルダーをドライブ C に残しておくことができます。これにより、エンド ユーザーまたは再販業者はデータ ドライブのデータ フォルダーのレイアウトを決定できるようになります。  
  
###  <a name="example-1-create-a-custom-folder-and-move-the-default-folders-to-a-new-location-from-posticcmd-by-using-windows-powershell"></a><a name="BKMK_Example1"></a>例 1: Windows PowerShell を使用してカスタムフォルダーを作成し、Postic.cmd から新しい場所に既定のフォルダーを移動する  
  
1.  「[初期構成後のタスクを実行するための PostIC.cmd ファイルの作成](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md)」セクションで詳細に説明されているように、初期構成後のタスクを実行するための PostIC.cmd ファイルを作成します。  
  
2.  メモ帳を使用して、C:\Windows\Setup\Scripts フォルダーに**customizefolders. ps1**という名前のファイルを作成し、次の Windows PowerShell&reg; コマンドをファイルに貼り付けます (目的の動作に応じて適切な行のマークを解除します)。  
  
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
  
###  <a name="example-2-create-a-custom-folder-and-move-an-existing-folder-by-using-the-windows-server-solutions-sdk"></a><a name="BKMK_Example2"></a>例 2: Windows Server Solutions SDK を使用してカスタムフォルダーを作成し、既存のフォルダーを移動する  
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
  
## <a name="see-also"></a>参照  
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)
