---
title: "複数言語サポート用のサーバー回復 DVD を作成します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-server-recovery-dvd-for-multi-language-support"></a>複数言語サポート用のサーバー回復 DVD を作成します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

##  <a name="BKMK_MLHeadedRecovery"></a>ローカルで管理されるサーバー上で、サーバーのセットアップと多言語サポート用のサーバー回復 DVD を作成します。  
  
> [!NOTE]
>  多言語 Windows イメージを作成する必要があります最初、[チュートリアル: 多言語 Windows イメージの作成](https://technet.microsoft.com/library/jj126995)、Windows Server Essentials の言語パックを install.wim に追加する前にします。  
  
 セットアップの 2 つのフェーズがある: Windows プレインストール環境 (Windows PE) と初期構成します。 既定では、初期構成で言語選択ページは表示されません。  
  
-   OEM リモート管理インストールまたは OEM プレインストール シナリオでは、レジストリ キーを使用して、次のコマンドを初期構成で言語選択ページを表示するを追加する必要があります。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
    ```  
  
    > [!IMPORTANT]
    >  Oem は、ラボでイメージを作成するときを選択する必要があります**英語**セットアップの Windows PE フェーズ中に言語として。  
  
-   リセラー オプション キット (ROK) シナリオでは、ユーザーによっては DVD と場合によりハードウェアが表示されます。 顧客は、Windows PE セットアップ中に言語を選択することと、初期構成中に言語の選択] ページが表示されなくします。  
  
 複数の言語を含む 1 つのデュアル レイヤー DVD を出荷することができます。  
  
 このセクションでは、Windows セットアップに言語のサポートを追加する方法について説明します。 Windows PE 3.0 をカスタマイズするための主要なツールは、展開イメージのサービスと管理 (DISM) コマンド ライン ツールです。 このソリューションでは、次のシナリオが有効にします。  
  
1.  多言語のインストールを作成します。  
  
2.  配布可能なメディアを作成します。  
  
### <a name="prerequisites"></a>前提条件  
 多言語サポートを Windows セットアップを追加するには、以下が必要。  
  

-   すべてのツールとカスタマイズした WinPE イメージを作成するために必要なソース ファイルを提供するテクニシャン コンピューター。 詳細については、次を参照してください。[テクニシャン コンピューターの準備](Prepare-the-Technician-Computer.md)します。  

-   すべてのツールとカスタマイズした WinPE イメージを作成するために必要なソース ファイルを提供するテクニシャン コンピューター。 詳細については、次を参照してください。[テクニシャン コンピューターの準備](../install/Prepare-the-Technician-Computer.md)します。  

  
-   Windows Server Essentials DVD します。  
  
-   Windows Server Essentials 言語パック DVD します。  
  
###  <a name="BKMK_Steps"></a>複数言語サポートを追加します。  
 Windows セットアップに複数言語サポートを追加する Windows Server 2012 を追加することで、Install.wim を更新して、Windows Server Essentials 言語パックをします。  
  
#### <a name="update-installwim"></a>Install.wim を更新します。  
 この手順で Windows Server 2012 および Windows Server Essentials 言語パックを Install.wim に追加します。  
  
> [!NOTE]
>  Windows Server 2012 用の言語パックをインストールすることを確認します。 これにより、適切なブランド化を取得することができます。 Windows Server 2012 多言語ユーザー インターフェイス言語パックがでご確認いただけます[Microsoft.com](https://www.microsoft.com/OEM/en/installation/downloads/Pages/technical-downloads.aspx)します。手順に従ってください」の説明に従って、[チュートリアル: 多言語 Windows イメージの作成、多言語](https://technet.microsoft.com/library/jj126995.aspx)に Windows Server Essentials 言語パックを追加する前に、多言語 Windows イメージを作成する方法にInstall.wim します。  
>   
>  Windows Server Essentials 言語パックとは、言語パック メディアの \Language Packs\\ < CultureName\ > で使用できます。  
  
> [!NOTE]
>  すべての言語パックが Windows Server 2012 のリリース以前に使用できない可能性があります。  
  
###### <a name="to-add-language-packs-to-installwim"></a>言語パックを Install.wim に追加するには  
  
1.  (この例では、フランス語を使用して) 次のように、オペレーティング システムと製品の言語パックを Install.wim に追加します。  
  
    ```  
    Dism /Mount-Wim /WimFile:C:\my_distribution\sources\install.wim /index:1 /MountDir:C:\InstallMount  
    Mkdir c:\temp_Scratch  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<path_to_OS_language_packs>\fr-fr\lp.cab  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<OCD\Language Packs\FR-FR\lp.cab  
  
    ```  
  

2.  フラッシュ ドライブで説明する手順を使用して、クライアント バックアップ復元用 USB の作成をサポートする言語固有ファイルを追加[多言語のクライアント復元メディアのビルド](Build-Multi-Language-Client-Restore-Media.md)します。  

2.  フラッシュ ドライブで説明する手順を使用して、クライアント バックアップ復元用 USB の作成をサポートする言語固有ファイルを追加[多言語のクライアント復元メディアのビルド](../install/Build-Multi-Language-Client-Restore-Media.md)します。  

  
3.  使用して追加の言語サポートを反映するようにルーズ メディア内の Lang.ini ファイルを作成し直す、`DISM /Gen-LangINI`コマンドの例。  
  
    ```  
    Dism /image:C:\InstallMount /Gen-LangINI /distribution:C:\my_distribution  
  
    ```  
  
4.  使用して、イメージに変更を保存、`DISM /unmount /commit`コマンドの例。  
  
    ```  
    Dism /Unmount-Wim /MountDir:C:\InstallMount /Commit  
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

