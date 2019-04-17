---
title: "イメージの展開の準備"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 681c6cad-7fde-494f-86a5-f4c7c15d23f9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 16411ab073e9417c52592aa9a6b13707dd461537
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="preparing-the-image-for-deployment"></a>イメージの展開の準備

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

イメージを準備するための一般的なツールは、sysprep.exe です。 このツールを実行して、イメージを一般化し、イメージを含む、サーバーが再起動されたときに、初期構成を実行するために、サーバーをシャット ダウンします。 Sysprep.exe を実行する前に、イメージに対するすべての変更が完了する必要があります。  
  
> [!NOTE]
>  Sysprep.exe を使用して Windows 製品のライセンス認証を最大 3 回までをリセットすることができます。  
  
#### <a name="to-prepare-the-image"></a>イメージを準備するには  
  
1.  追加した SkipIC.txt を削除しますか。  
  
2.  管理者特権でコマンド プロンプト ウィンドウを開きます。 をクリックして**開始**、右クリックして**コマンド プロンプト**、し、[**管理者として実行**します。  
  
3.  ユーザーがフル猶予期間、サーバーが準拠しなくなる前にできるようにするために、レジストリ キーをリセットする次のコマンドを実行します。  
  
    ```  
    %systemroot%\system32\reg.exe add HKLM\Software\Microsoft\ServerInfrastructureLicensing /v Rearm /t REG_DWORD /d 1 /f  
    ```  
  
4.  キー、言語、ロケール ページおよび EULA ページを表示するレジストリ キーを追加するには、次のコマンドを実行します。 既定では、これらのページは初期構成中に表示されません。 このため、プレインストールされたをリリースする場合は、このレジストリ キーを追加する必要があります。 ただし、DVD をリリースする場合する必要がありますしないこのキーを追加、ようにこれらのページが WinPE および初期構成中に表示されます。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
    ```  
  
5.  場合は、あらかじめキーがキーの初期構成] ページを無効にします。 キー ページは場合にのみ表示 ShowPreinstallPages = true および KeyPreInstalled! = true です。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v KeyPreInstalled /t REG_SZ /d true /f  
    ```  
  
6.  ハードウェア要件チェックを無効にする場合は、レジストリ キーを追加するには、次のコマンドを実行します。 これは、ハードウェア要件を満たさないプレインストールされている] ボックスにのみです。 DVD をリリースするか、またはをハードウェア要件を満たしている場合、は、このキーを追加しないことをお勧めします。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
    ```  
  
7.  (省略可能)下にあるログを削除する**%programdata%\Microsoft\Windows server \logs**します。  
  
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
  
9. Sysprep に対して次のコマンドを実行します。  
  
    ```  
    %systemroot%\system32\sysprep\sysprep.exe /generalize /OOBE /unattend:xxx.xml /Quit  
    ```  
  
    > [!IMPORTANT]
    >  Sysprep のパラメーターとしての代わりに、%systemdrive% の下の unattend.xml を追加することもできます。 ファイルが下にある場合は、c:\ は該当するユーザーの設定がユーザーの設定で説明していない sysprep のパラメーターとして使用する場合。 %Systemdrive% の下の unattend.xml は、サーバーを再起動するたびに削除されます。 このため、%systemdrive% の下に unattend.xml を作成した後、サーバーは再起動しないことを確認します。  
  
10. Windows OOBE キー ページをスキップするレジストリ キーを追加するには、次のコマンドを実行します。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedProductKey /t REG_DWORD /d 1 /f  
    ```  
  
11. Windows 言語の選択] ページをスキップするレジストリ キーを追加するには、次のコマンドを実行します。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedLanguageSelection /t REG_DWORD /d 1 /f  
    ```  
  
    > [!IMPORTANT]
    >  最後の 2 つの手順を実行する必要がありますが、その Windows OOBE ページがこれには、初期構成ページおよびブレーキ リモートで管理されるサーバーのシナリオに期限を可能になった。  
  
12. Sysprep の後、ボックスをシャット ダウン、イメージをキャプチャしたり、サーバーを再起動して、クライアント コンピューターから初期構成を続行できます。  
  
> [!IMPORTANT]
>  サーバー回復メディアの作成を計画しているパートナーは、イメージをキャプチャおよび、次の手順に進む前に、回復メディアを作成する必要があります。