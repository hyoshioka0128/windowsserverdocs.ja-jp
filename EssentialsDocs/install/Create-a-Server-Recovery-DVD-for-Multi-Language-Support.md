---
title: 複数言語サポート用のサーバー回復 DVD の作成
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: c7da0f6c-9732-4784-9c28-7dad72c4071d
author: daveba
ms.author: daveba
ms.openlocfilehash: 3c415155734515af004e25a07c4e61afabaa3359
ms.sourcegitcommit: 04637054de2bfbac66b9c78bad7bf3e7bae5ffb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87838011"
---
# <a name="create-a-server-recovery-dvd-for-multi-language-support"></a>複数言語サポート用のサーバー回復 DVD の作成

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="create-a-server-setup-and-server-recovery-dvd-for-multiple-language-support-on-locally-administered-servers"></a><a name="BKMK_MLHeadedRecovery"></a>ローカルで管理されているサーバーで複数の言語をサポートするためのサーバーセットアップとサーバー回復 DVD の作成

> [!NOTE]
>  まず、「[チュートリアル:](/previous-versions/windows/it-pro/windows-8.1-and-8/jj126995(v=win.10)) Windows Server Essentials install.wim pack をインストールする前に、多言語 windows イメージの作成」の説明に従って、多言語の windows イメージを作成する必要があります。

 セットアップには、Windows プレインストール環境 (Windows PE) と初期構成という 2 つのフェーズがあります。 既定では、初期構成には言語選択ページは表示されません。

- OEM リモート管理インストールまたは OEM プレインストール シナリオでは、次のコマンドを使用してレジストリ キーを追加し、初期構成で言語選択ページを表示する必要があります。

  ```
  %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f
  ```

  > [!IMPORTANT]
  >  OEM は実験環境でイメージを作成する際、セットアップの Windows PE フェーズで言語として **英語** を選択する必要があります。

- ROK (Reseller Option Kit) シナリオでは、顧客には DVD と場合によりハードウェアが納品されます。 顧客は、Windows PE セットアップ中に言語を選択できるため、初期構成中に言語選択ページは表示されません。

  複数の言語を含む 1 枚の 2 層 DVD の出荷を選択することができます。

  ここでは、言語サポートを Windows セットアップに追加する方法について説明します。 Windows PE 3.0 をカスタマイズするための主要なツールは、展開イメージのサービスと管理 (DISM) というコマンド ライン ツールです。 このソリューションでは、次のシナリオが可能になります。

1.  多言語インストールの作成

2.  配布可能なメディアの作成

### <a name="prerequisites"></a>前提条件
 多言語サポートを Windows セットアップに追加するには、次のものが必要です。


-   カスタマイズした WinPE イメージの作成に必要なツールとソース ファイルのすべてを提供するテクニシャン コンピューター。 詳細については、「[テクニシャン コンピューターの準備](Prepare-the-Technician-Computer.md)」を参照してください。

-   カスタマイズした WinPE イメージの作成に必要なツールとソース ファイルのすべてを提供するテクニシャン コンピューター。 詳細については、「[テクニシャン コンピューターの準備](../install/Prepare-the-Technician-Computer.md)」を参照してください。


-   Windows Server Essentials DVD。

-   Windows Server Essentials 言語パック DVD。

###  <a name="adding-multiple-language-support"></a><a name="BKMK_Steps"></a>複数言語サポートの追加
 Windows セットアップに複数の言語サポートを追加するには、Windows Server 2012 および Windows Server Essentials 言語パックを追加して、インストール .wim を更新します。

#### <a name="update-installwim"></a>Install.wim の更新
 この手順では、Windows Server 2012 および Windows Server Essentials 言語パックをインストール .wim に追加します。

> [!NOTE]
>  Windows Server 2012 の言語パックがインストールされていることを確認します。 これで適切なブランド化を取得できます。 Windows Server 2012 多言語ユーザーインターフェイス言語パックは、 [Microsoft.com](https://www.microsoft.com/OEM/en/installation/downloads/Pages/technical-downloads.aspx)で入手できます。 「[チュートリアル:](/previous-versions/windows/it-pro/windows-8.1-and-8/jj126995(v=win.10))多言語の windows イメージの作成」で説明されている手順に従って、Windows Server Essentials 言語パックをインストール .wim に追加します。
>
>  Windows Server Essentials 言語パックは、言語パックメディア () の言語パックメディアで利用できます。この言語パックは、 \\<の選別 \> します。

> [!NOTE]
>  Windows Server 2012 のリリース以前は、すべての言語パックを利用できない場合があります。

###### <a name="to-add-language-packs-to-installwim"></a>言語パックを Install.wim に追加するには

1.  次のようにオペレーティング システムと製品の言語パックを install.wim に追加します (この例では、フランス語を使用します)。

    ```
    Dism /Mount-Wim /WimFile:C:\my_distribution\sources\install.wim /index:1 /MountDir:C:\InstallMount
    Mkdir c:\temp_Scratch
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<path_to_OS_language_packs>\fr-fr\lp.cab
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<OCD\Language Packs\FR-FR\lp.cab

    ```


2.  「[複数言語のクライアント復元メディアの作成](Build-Multi-Language-Client-Restore-Media.md)」で説明されている手順に従って、クライアントバックアップ復元 USB フラッシュドライブの作成をサポートする言語固有のファイルを追加します。

2.  「[複数言語のクライアント復元メディアの作成](../install/Build-Multi-Language-Client-Restore-Media.md)」で説明されている手順に従って、クライアントバックアップ復元 USB フラッシュドライブの作成をサポートする言語固有のファイルを追加します。


3.  `DISM /Gen-LangINI` コマンドを使用して、追加の言語サポートを反映するようにルーズ メディア内の Lang.ini ファイルを再作成します。次に例を示します。

    ```
    Dism /image:C:\InstallMount /Gen-LangINI /distribution:C:\my_distribution

    ```

4.  `DISM /unmount /commit` コマンドを使用して、変更をイメージに保存し直します。次に例を示します。

    ```
    Dism /Unmount-Wim /MountDir:C:\InstallMount /Commit
    ```

## <a name="see-also"></a>参照

 [イメージの作成とカスタマイズ追加の](Creating-and-Customizing-the-Image.md)[カスタマイズ](Additional-Customizations.md)[展開のイメージの準備](Preparing-the-Image-for-Deployment.md)[カスタマーエクスペリエンスのテスト](Testing-the-Customer-Experience.md)