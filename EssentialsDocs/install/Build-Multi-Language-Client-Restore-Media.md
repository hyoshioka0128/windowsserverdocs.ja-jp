---
title: "複数言語のクライアント復元メディアを作成します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fdbc016-d464-43cb-bd75-8a63e61588a2
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1ad934d297c3092050bd6adbb6bb0f50d1ec6f36
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="build-multi-language-client-restore-media"></a>複数言語のクライアント復元メディアを作成します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

> [!NOTE]
>  多言語 Windows イメージを作成する必要があります最初、[チュートリアル: 多言語 Windows イメージの作成](https://technet.microsoft.com/library/jj126995)、Windows Server Essentials の言語パックを install.wim に追加する前にします。  
  
 複数言語のサーバー インストール DVD を作成するときは、サーバーの install.wim 言語パックがインストールされます。 復元ウィザードのローカライズされたリソースは、言語パックの一部としてインストールされます。  
  
### <a name="to-build-a-multi-language-client-restore-media"></a>複数言語のクライアント復元メディアを作成するには  
  
1.  Install.wim をマウント クライアント復元メディアのルートとして c:\mount\Program files \Windows Server \bin\clientrestore フォルダーを呼び出して、c:\mount に: [RestoreMediaRoot] の下。  
  
    ```  
    dism /mount-wim /wimfile:install.wim /index:1 /mountdir:c:\mount  
    ```  
  
2.  [RestoreMediaRoot]\Sources\Boot.wim (同じ手順はすぎる boot_x86.wim に対して実行する必要があります) には、クライアント復元 WIM ファイルをマウントします。 コマンド ラインに示します。  
  
    ```  
    dism /mount-wim /wimfile:boot.wim /index:1 /mountdir:c:\mountRestore  
    ```  
  
3.  実行して、復元メディアに WinPE-Setup.cab パッケージを追加します。  
  
    ```  
    dism /image:c:\mountRestore /add-package /packagepath:WinPE-Setup.cab  
    ```  
  
4.  メモ帳を使用して c:\mountRestore\windows\system32\winpeshl.ini を編集し、次の内容。  
  
    ```  
    [LaunchApp]  
    AppPath = %SYSTEMDRIVE%\sources\SelectLanguage.exe  
    ```  
  
5.  言語パックは、復元メディアを追加します。 言語パックを追加するは、次のコマンドを実行中で実行できます。  
  
    ```  
    dism /image:c:\mountRestore /add-package /packagepath:[language pack path]  
    ```  
  
     次の言語パックを追加する必要があります。  
  
    1.  WinPE 言語パック (lp.cab)  
  
    2.  Winpe-setup 言語パック (winpe-setup _ [lang] .cab、WinPE-Setup_en-us.cab など)  
  
    3.  Zh-cn、zh tw、zh 香港、ko-kr の ja-jp、フォントの追加のフォント パックをインストールする必要 (winpe - fontsupport-[lang] .cab、winpe-fontsupport-zh-cn.cab など)  
  
6.  実行して、新しい Lang.ini ファイルを生成します。  
  
    ```  
    dism /image:c:\mountRestore /Gen-LangINI /distribution:mount  
    ```  
  
7.  コミットしを実行して、イメージのマウントを解除します。  
  
    ```  
    dism /unmount-wim /mountdir:c:\mountRestore /commit  
    ```  
  
8.  [RestoreMediaroot]\Sources\Boot_x86.wim に対して、手順 7 には、手順 2。  
  
9. コミットしを実行して、イメージのマウントを解除します。  
  
    ```  
    dism /unmount-wim /mountdir:c:\mount /commit  
    ```  
  
## <a name="see-also"></a>参照してください。  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

