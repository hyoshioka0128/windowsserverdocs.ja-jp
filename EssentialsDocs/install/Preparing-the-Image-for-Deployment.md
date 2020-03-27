---
title: イメージの展開の準備
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 681c6cad-7fde-494f-86a5-f4c7c15d23f9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: aac776253c094c4a77269720bcc5762d6c41d720
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311552"
---
# <a name="preparing-the-image-for-deployment"></a>イメージの展開の準備

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

イメージを準備するための一般的なツールは、sysprep.exe です。 イメージを保存したサーバーを再起動する際に初期構成が実行されるように、このツールを実行してイメージを一般化しサーバーをシャットダウンします。 イメージへのすべての変更は、sysprep.exe を実行する前に完了しておく必要があります。  
  
> [!NOTE]
>  sysprep.exe を使用することで、Windows 製品のライセンス認証を最大 3 回までリセットできます。  
  
#### <a name="to-prepare-the-image"></a>イメージを準備するには  
  
1.  追加した SkipIC.txt を削除します。  
  
2.  昇格した [コマンド プロンプト] ウィンドウを開きます。 **[スタート]** ボタンをクリックし、 **[コマンド プロンプト]** を右クリックして、 **[管理者として実行]** を選択します。  
  
3.  サーバーが準拠しなくなる前にユーザーに十分な猶予期間を与えるように、次のコマンドを実行してレジストリ キーをリセットします。  
  
    ```  
    %systemroot%\system32\reg.exe add HKLM\Software\Microsoft\ServerInfrastructureLicensing /v Rearm /t REG_DWORD /d 1 /f  
    ```  
  
4.  次のコマンドを実行して、キー、言語ページ、ロケール ページ、および EULA ページを表示するためのレジストリ キーを追加します。 既定では、これらのページは初期構成中に表示されません。 そのため、プレインストールされたコンピューターをリリースする場合、このレジストリ キーを追加する必要があります。 ただし、DVD をリリースする場合は、これらのページが WinPE および初期構成中に表示されるので、このキーを追加しないでください。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
    ```  
  
5.  コンピューターにあらかじめキーが設定されている場合、初期構成のキー ページを無効にします。 キー ページは、ShowPreinstallPages = true および KeyPreInstalled != true となっている場合にのみ表示されます。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v KeyPreInstalled /t REG_SZ /d true /f  
    ```  
  
6.  ハードウェア要件チェックを無効にする場合、次のコマンドを実行してレジストリ キーを追加します。 これは、ハードウェア要件を満たさないプレインストールされたコンピューター専用です。 DVD をリリースする場合や、コンピューターがハードウェア要件を満たしている場合は、このキーを追加しないことをお勧めします。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
    ```  
  
7.  (省略可能) **%programdata%\Microsoft\Windows Server\Logs** にあるログを削除します。  
  
8.  次のテンプレートに示すように sysprep に対して unattended xml ファイルを準備します。  
  
    ```  
    <unattend xmlns="urn:schemas-microsoft-com:unattend" xmlns:ms="urn:schemas-microsoft-com:asm.v3">  
  
      <settings pass="oobeSystem">  
        <component name="Microsoft-Windows-Shell-Setup" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" xmlns:wcm="https://schemas.microsoft.com/WMIConfig/2002/State" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  
          <!-- Must have -->  
          <OOBE>  
             <HideEULAPage>true</HideEULAPage>  
          </OOBE>  
          <!-- Must have -->  
          <AutoLogon>   
            <Enabled>true</Enabled>   
            <Username>Administrator</Username>   
            <Domain>.</Domain>   
            <Password>   
              <!--You can set any password you like, but keep it consistent with password settings -->       
              <Value>Admin@123</Value>   
              <PlainText>true</PlainText>   
            </Password>   
          </AutoLogon>   
          <UserAccounts>   
           <AdministratorPassword>   
             <!--You can set any password you like, but keep it consistent with auto logon settings -->       
             <Value>Admin@123</Value>   
             <PlainText>true</PlainText>   
           </AdministratorPassword>   
          </UserAccounts>  
  
          <!-- Optional -->  
          <OEMInformation>  
             <HelpCustomized>true</HelpCustomized>  
             <Manufacturer>OEM name</Manufacturer>  
             <Model>model name</Model>  
             <SupportHours>hours</SupportHours>  
             <SupportPhone>123-456-7890</SupportPhone>  
             <SupportURL>http://www.contoso.com</SupportURL>  
          </OEMInformation>  
  
        </component>  
  
      </settings>  
  
      <settings pass="specialize">  
        <component name="Microsoft-Windows-Shell-Setup" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" processorArchitecture="amd64">  
          <!-- Must have -->  
          <ComputerName>Server</ComputerName>          
          <!-- Optional -->  
          <ProductKey>XXXXX-XXXXX-XXXXX-XXXXX-XXXXX</ProductKey>  
        </component>  
      </settings>  
    </unattend>  
    ```  
  
9. sysprep に対して次のコマンドを実行します。  
  
    ```  
    %systemroot%\system32\sysprep\sysprep.exe /generalize /OOBE /unattend:xxx.xml /Quit  
    ```  
  
    > [!IMPORTANT]
    >  unattend.xml は、sysprep のパラメーターとしてではなく、%systemdrive% の下に追加することもできます。 ファイルが c:\ の下にある場合ユーザーの設定によってカバーされますが、sysprep のパラメーターとして使用される場合は、ユーザーの設定によってカバーされません。 %systemdrive% の下の unattend.xml は、サーバーを再起動するたびに削除されます。 そのため、%systemdrive% の下に unattend.xml を作成した後でサーバーが再起動されていないことを確認します。  
  
10. Windows OOBE キー ページをスキップする場合は、次のコマンドを実行してレジストリ キーを追加します。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedProductKey /t REG_DWORD /d 1 /f  
    ```  
  
11. Windows 言語の選択ページをスキップする場合は、次のコマンドを実行してレジストリ キーを追加します。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedLanguageSelection /t REG_DWORD /d 1 /f  
    ```  
  
    > [!IMPORTANT]
    >  最後の 2 つの手順を実行する必要があります。実行しないと、初期構成ページに Windows OOBE ページが表示され、リモートで管理されるサーバーのシナリオが中断します。  
  
12. sysprep の後にコンピューターをシャットダウンします。イメージをキャプチャするか、サーバーを再起動してクライアント コンピューターから初期構成を続行できます。  
  
> [!IMPORTANT]
>  サーバーの回復メディアの作成を計画しているパートナーは、次の手順に進む前に、イメージをキャプチャして回復メディアを作成する必要があります。