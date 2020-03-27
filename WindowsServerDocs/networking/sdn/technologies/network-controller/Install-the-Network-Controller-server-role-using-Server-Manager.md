---
title: を使用してネットワークコントローラーのサーバーの役割をインストールサーバーマネージャー
description: このトピックでは、Windows Server 2016 のサーバーマネージャーを使用して、ネットワークコントローラーのサーバーの役割をインストールする手順について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3a6e4352-ff62-4290-b8a4-5c83740070fc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: b8a3e1ede1cdec1ca5ee66be8d53d4420bec673b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317132"
---
# <a name="install-the-network-controller-server-role-using-server-manager"></a>を使用してネットワークコントローラーのサーバーの役割をインストールサーバーマネージャー

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、サーバー マネージャーを使用して、ネットワーク コント ローラー サーバーの役割をインストールする方法の手順を示します。

>[!IMPORTANT]
>ネットワークコントローラーのサーバーの役割を物理ホストに展開しないでください。 ネットワークコントローラーを展開するには、hyper-v ホストにインストールされている VM\) \(Hyper-v 仮想マシンにネットワークコントローラーサーバーの役割をインストールする必要があります。 3つの異なる\-Hyper-v ホスト上の Vm にネットワークコントローラーをインストールした後、Windows PowerShell コマンド**NetworkControllerServer**を使用してネットワークコントローラーにホストを追加することで、ソフトウェアで定義されたネットワーク \(SDN\) 用のハイパー\-V ホストを有効にする必要があります。 これにより、SDN ソフトウェア ロード バランサーが機能するようになります。 詳細については、「 [NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)」を参照してください。
  
ネットワーク コント ローラーをインストールした後は、追加のネットワーク コント ローラー構成の Windows PowerShell コマンドを使用する必要があります。 詳細については、次を参照してください。 [展開ネットワーク コント ローラーが Windows PowerShell を使用して](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)します。  
  
### <a name="to-install-network-controller"></a>ネットワーク コント ローラーをインストールするには  
  
1.  サーバー マネージャーで、 **[管理]** をクリックし、 **[役割と機能の追加]** をクリックします。 役割と機能の追加ウィザードが開きます。 **[次へ]** をクリックします。  
  
2.  **インストールの種類**, 既定の設定を保持し、クリックして **次**します。  
  
3.  **移行先サーバーの選択**, 、ネットワーク コント ローラーをインストールするサーバーを選択して **次**します。  
  
4.  **サーバーの役割**, で、 **ロール**, をクリックして **ネットワーク コント ローラー**します。  
  
    ![ネットワーク コント ローラーのサーバーの役割](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
5.  **ネットワーク コント ローラーに必要な機能を追加**  ダイアログ ボックスが表示されます。 **[機能の追加]** をクリックします。  
  
    ![ネットワーク コント ローラーの機能を追加します。](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_06.jpg)  
  
6.  **サーバーの役割**, をクリックして **次**します。  
  
    ![[次へ] をクリックします。](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
7.  **機能の選択**, 、クリックして **次**します。  
  
8.  **ネットワーク コント ローラー** クリックして **次**します。  
  
9. **インストール オプションの確認**, 、選択内容を確認します。 ネットワーク コント ローラーのインストールでは、ウィザードを実行した後、コンピューターを再起動する必要があります。 このため、次のようにクリックします。 **ために必要な場合は、移行先サーバーを自動的に再起動**します。 **追加の役割と機能ウィザード**  ダイアログ ボックスが表示されます。 **[はい]** をクリックします。  
  
    ![役割と機能の追加ウィザード](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_11.jpg)  
  
10. **[インストール オプションの確認]** で、 **[インストール]** をクリックします。  
  
11. 移行先サーバーにネットワーク コント ローラー サーバーの役割をインストールし、サーバーを再起動します。  
  
12. コンピューターを再起動した後、コンピューターにログオンし、サーバー マネージャーを表示してネットワーク コント ローラーのインストールを確認します。  
  
    ![サーバー マネージャー](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/nc_013.jpg)  
  
## <a name="see-also"></a>参照  
[ネットワーク コントローラー](Network-Controller.md)  
  


