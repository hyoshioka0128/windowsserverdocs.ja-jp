---
title: 複数言語サポート用のサーバー回復 DVD の作成
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7da0f6c-9732-4784-9c28-7dad72c4071d
4author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ac547f97b48e4cd0ebf87e0935cadc2c539b4d0b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855003"
---
# <a name="create-a-server-recovery-dvd-for-multi-language-support"></a>複数言語サポート用のサーバー回復 DVD の作成

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="BKMK_MLHeadedRecovery"></a> ローカルで管理されているサーバーで、サーバーのセットアップと複数言語のサポート用のサーバー回復 DVD を作成します。  
  
> [!NOTE]
>  多言語 Windows イメージを作成する必要があります最初、[チュートリアル。多言語 Windows イメージの作成](https://technet.microsoft.com/library/jj126995)Windows Server Essentials 言語パックを install.wim に追加する前にします。  
  
 セットアップには、Windows プレインストール環境 (Windows PE) と初期構成という 2 つのフェーズがあります。 既定では、初期構成には言語選択ページは表示されません。  
  
-   OEM リモート管理インストールまたは OEM プレインストール シナリオでは、次のコマンドを使用してレジストリ キーを追加し、初期構成で言語選択ページを表示する必要があります。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
    ```  
  
    > [!IMPORTANT]
    >  OEM は実験環境でイメージを作成する際、セットアップの Windows PE フェーズで言語として **英語** を選択する必要があります。  
  
-   ROK (Reseller Option Kit) シナリオでは、顧客には DVD と場合によりハードウェアが納品されます。 顧客は、Windows PE セットアップ中に言語を選択できるため、初期構成中に言語選択ページは表示されません。  
  
 複数の言語を含む 1 枚の 2 層 DVD の出荷を選択することができます。  
  
 ここでは、言語サポートを Windows セットアップに追加する方法について説明します。 Windows PE 3.0 をカスタマイズするための主要なツールは、展開イメージのサービスと管理 (DISM) というコマンド ライン ツールです。 このソリューションでは、次のシナリオが可能になります。  
  
1.  多言語インストールの作成  
  
2.  配布可能なメディアの作成  
  
### <a name="prerequisites"></a>前提条件  
 多言語サポートを Windows セットアップに追加するには、次のものが必要です。  
  

-   カスタマイズした WinPE イメージの作成に必要なツールとソース ファイルのすべてを提供するテクニシャン コンピューター。 詳細については、「 [Prepare the Technician Computer](Prepare-the-Technician-Computer.md)」を参照してください。  

-   カスタマイズした WinPE イメージの作成に必要なツールとソース ファイルのすべてを提供するテクニシャン コンピューター。 詳細については、「 [Prepare the Technician Computer](../install/Prepare-the-Technician-Computer.md)」を参照してください。  

  
-   Windows Server Essentials DVD。  
  
-   Windows Server Essentials 言語パック DVD。  
  
###  <a name="BKMK_Steps"></a> 複数言語のサポートを追加します。  
 Windows セットアップに複数言語のサポートを追加する、Windows Server 2012 を追加することで、Install.wim を更新して、Windows Server Essentials 言語パックをします。  
  
#### <a name="update-installwim"></a>Install.wim の更新  
 この手順で Windows Server 2012 および Windows Server Essentials 言語パックを Install.wim に追加します。  
  
> [!NOTE]
>  Windows Server 2012 の言語パックをインストールすることを確認します。 これで適切なブランド化を取得できます。 Windows Server 2012 Multilingual User Interface Language Pack は[Microsoft.com](https://www.microsoft.com/OEM/en/installation/downloads/Pages/technical-downloads.aspx)します。 手順に従ってください」の説明に従って、[チュートリアル。多言語 Windows イメージの作成、多言語](https://technet.microsoft.com/library/jj126995.aspx)Windows Server Essentials 言語パックを install.wim に追加する前に、多言語 Windows イメージを作成する方法。  
>   
>  Windows Server Essentials 言語パックは、言語パック メディアの \Language パックで入手\\< CultureName\>します。  
  
> [!NOTE]
>  すべての言語パックは、Windows Server 2012 のリリース以前に使用できない可能性があります。  
  
###### <a name="to-add-language-packs-to-installwim"></a>言語パックを Install.wim に追加するには  
  
1.  次のようにオペレーティング システムと製品の言語パックを install.wim に追加します (この例では、フランス語を使用します)。  
  
    ```  
    Dism /Mount-Wim /WimFile:C:\my_distribution\sources\install.wim /index:1 /MountDir:C:\InstallMount  
    Mkdir c:\temp_Scratch  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<path_to_OS_language_packs>\fr-fr\lp.cab  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<OCD\Language Packs\FR-FR\lp.cab  
  
    ```  
  

2.  クライアント バックアップ復元 USB の作成をサポートする言語固有のファイルのフラッシュ ドライブで説明する手順を使用して追加[多言語のクライアント復元メディアのビルド](Build-Multi-Language-Client-Restore-Media.md)します。  

2.  クライアント バックアップ復元 USB の作成をサポートする言語固有のファイルのフラッシュ ドライブで説明する手順を使用して追加[多言語のクライアント復元メディアのビルド](../install/Build-Multi-Language-Client-Restore-Media.md)します。  

  
3.  `DISM /Gen-LangINI` コマンドを使用して、追加の言語サポートを反映するようにルーズ メディア内の Lang.ini ファイルを再作成します。次に例を示します。  
  
    ```  
    Dism /image:C:\InstallMount /Gen-LangINI /distribution:C:\my_distribution  
  
    ```  
  
4.  `DISM /unmount /commit` コマンドを使用して、変更をイメージに保存し直します。次に例を示します。  
  
    ```  
    Dism /Unmount-Wim /MountDir:C:\InstallMount /Commit  
    ```  
  
## <a name="see-also"></a>関連項目  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

