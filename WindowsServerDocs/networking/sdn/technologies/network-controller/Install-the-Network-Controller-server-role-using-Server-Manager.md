---
title: を使用してネットワークコントローラーのサーバーの役割をインストールサーバーマネージャー
description: このトピックでは、Windows Server 2016 のサーバーマネージャーを使用して、ネットワークコントローラーのサーバーの役割をインストールする手順について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3a6e4352-ff62-4290-b8a4-5c83740070fc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8b656bbd823a10f1e36d1757bb53c4565d4e828c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405837"
---
# <a name="install-the-network-controller-server-role-using-server-manager"></a>を使用してネットワークコントローラーのサーバーの役割をインストールサーバーマネージャー

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、サーバー マネージャーを使用して、ネットワーク コント ローラー サーバーの役割をインストールする方法の手順を示します。

>[!IMPORTANT]
>ネットワークコントローラーのサーバーの役割を物理ホストに展開しないでください。 ネットワーク コント ローラーを展開するには、ホストにインストールされている HYPER-V 仮想マシン\(VM\)でネットワーク コントローラー サーバーの役割をインストールする必要があります。 次の 3 つの異なる HYPER\-V ホスト上の VM にでネットワーク コントローラーをインストールした後、Windows PowerShell コマンド **New-NetworkControllerServer** を使用してホストをネットワーク コント ローラーに追加して、ソフトウェア定義ネットワーク\(SDN\)のHYPER\-Vホストを有効にする必要があります。 これにより、SDN ソフトウェア ロード バランサーが機能するようになります。 詳細については、[New-NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver) を参照してください。
  
ネットワーク コントローラーをインストールした後は、追加のネットワーク コントローラーの構成に Windows PowerShell コマンドを使用する必要があります。 詳細については、[Windows PowerShell を使用してネットワーク コントローラーを展開する](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md) を参照してください。  
  
### <a name="to-install-network-controller"></a>ネットワーク コント ローラーをインストールするには  
  
1.  サーバー マネージャーで、 **[管理]** をクリックし、 **[役割と機能の追加]** をクリックします。 役割と機能の追加ウィザードが開きます。 **[次へ]** をクリックします。  
  
2.  **インストールの種類**, 既定の設定を保持し、クリックして **次**します。  
  
3.  **移行先サーバーの選択**, 、ネットワーク コント ローラーをインストールするサーバーを選択して **次**します。  
  
4.  **サーバーの役割**, で、 **ロール**, をクリックして **ネットワーク コント ローラー**します。  
  
    ![ネットワーク コント ローラーのサーバーの役割](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
5.  **ネットワーク コント ローラーに必要な機能を追加**  ダイアログ ボックスが表示されます。 クリックして **機能を追加**します。  
  
    ![ネットワーク コント ローラーの機能を追加します。](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_06.jpg)  
  
6.  **サーバーの役割**, をクリックして **次**します。  
  
    ![[次へ] をクリックします。](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
7.  **機能の選択**, 、クリックして **次**します。  
  
8.  **ネットワーク コント ローラー** クリックして **次**します。  
  
9. **インストール オプションの確認**, 、選択内容を確認します。 ネットワーク コント ローラーのインストールでは、ウィザードを実行した後、コンピューターを再起動する必要があります。 このため、次のようにクリックします。 **ために必要な場合は、移行先サーバーを自動的に再起動**します。 **追加の役割と機能ウィザード**  ダイアログ ボックスが表示されます。 **[はい]** をクリックします。  
  
    ![役割および機能の追加ウィザード](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_11.jpg)  
  
10. **[インストール オプションの確認]** で、 **[インストール]** をクリックします。  
  
11. 移行先サーバーにネットワーク コント ローラー サーバーの役割をインストールし、サーバーを再起動します。  
  
12. コンピューターを再起動した後、コンピューターにログオンし、サーバー マネージャーを表示してネットワーク コント ローラーのインストールを確認します。  
  
    ![サーバー マネージャー](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/nc_013.jpg)  
  
## <a name="see-also"></a>関連項目  
[ネットワーク コントローラー](Network-Controller.md)  
  


