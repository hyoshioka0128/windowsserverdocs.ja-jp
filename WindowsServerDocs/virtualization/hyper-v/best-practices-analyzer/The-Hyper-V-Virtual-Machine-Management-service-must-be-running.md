---
title: HYPER-V 仮想マシン管理サービスを実行する必要があります。
description: このベスト プラクティス アナライザー ルールによって報告された問題を解決する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: f44d6887-6458-4438-9d93-574587e3f7d1
author: KBDAzure
ms.date: 10/03/2016
ms.openlocfilehash: 58886b68ca30ddeb064fc12c6cb4c00183399715
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826113"
---
# <a name="the-hyper-v-virtual-machine-management-service-must-be-running"></a>HYPER-V 仮想マシン管理サービスを実行する必要があります。

>適用先:Windows Server 2016
  
ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|前提条件|  

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題  
  
*仮想マシンを管理するために必要なサービスが実行されていません。*  
  
## <a name="impact"></a>影響  
  
*仮想マシンの管理操作は実行されません。*  
  
実行されている仮想マシンは引き続き実行します。 ただし、バーチャル マシンを管理または作成またはサービスが実行されるまでは、それらを削除することはできません。  
  
## <a name="resolution"></a>解決方法  
  
*サービス スナップインまたは Sc config コマンド ライン ツールを使用して、自動的に開始するサービスを再構成します。*  
  
> [!TIP]  
> デスクトップ アプリで、サービスが見つからないか、コマンド ライン ツールをレポートしたサービスが存在しない、HYPER-V 管理ツール可能性がありますがインストールされていません。 [スタート] メニューから HYPER-V MMC コンソールが表示されない場合は、HYPER-V 管理ツールをインストールする必要があります。

HYPER-V 管理ツールをインストールするには。  
>   
> - Windows Server で、サーバー マネージャーを開き 役割と機能のウィザードを使用します。 詳細については、次を参照してください。 [Windows Server 2016 に Hyper-v の役割をインストール](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md)します。  PowerShell を使用して、ツールをインストールすることもできます (`Install-WindowsFeature -Name Hyper-V-Tools, Hyper-V-PowerShell`) 
> - Windows では、デスクトップで、入力を開始 **プログラム**, 、 をクリックして **プログラムと機能** (コントロール パネル) > **に Windows の機能のオンとオフ** > **HYPER-V** > **HYPER-V 管理ツール**します。 クリックして **OK**します。  
  
### <a name="to-reconfigure-the-service-to-start-automatically-using-the-services-desktop-app"></a>サービスのデスクトップ アプリを使用して自動的に開始するサービスを再構成するには  
  
1.  サービスのデスクトップ アプリを開きます。 (をクリックして **開始**, 、内をクリックして、 **検索の開始** ボックスに、入力 **services.msc**, 、ENTER キーを押します)。  
  
2.  詳細ペインで右クリック **HYPER-V 仮想マシン管理**, 、 をクリックし、 **プロパティ**します。  
  
3.  **全般** ] タブの [ **スタートアップ** をクリックして、入力 **自動**です。  
  
4.  サービスを開始するにはクリックして **開始**します。  
  
### <a name="to-reconfigure-the-service-to-start-automatically-using-sc-config"></a>SC Config を自動的に使用を開始するサービスを再構成するには  
  
1.  Windows PowerShell を開きます。 (デスクトップで、次のようにクリックします**開始**の入力を開始および**Windows PowerShell**。)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  サービスを再構成するには、次のように入力します。  
  
    ```  
    sc config vmms start=auto  
    ```  
  
4.  サービスを開始するには、次のように入力します。  
  
    ```  
    sc start vmms  
    ```  
  
自動的に開始するサービスが既に構成されている、のみサービスを再起動する必要がある場合は、それには HYPER-V マネージャーとは"sc は、vmm を start"コマンドの前に示したからです。  
  
#### <a name="to-restart-the-service-from-hyper-v-manager"></a>HYPER-V マネージャーからサービスを再起動するには  
  
1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、**[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。  
  
2.  ナビゲーション ウィンドウでは、選択されていない場合、サーバーの名前をクリックします。  
  
3.  **アクション**  ウィンドウで、をクリックして **サービスの開始**します。  
  


