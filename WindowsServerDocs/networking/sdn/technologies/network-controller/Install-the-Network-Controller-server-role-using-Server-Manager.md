---
title: サーバー マネージャーを使用してネットワーク コントローラー サーバーの役割をインストールします。
description: このトピックは、Windows Server 2016 でサーバー マネージャーを使用して、ネットワーク コントローラー サーバーの役割をインストールする方法について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3a6e4352-ff62-4290-b8a4-5c83740070fc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 15cb1ef3bad7038cc97784504807b44b4920def6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-network-controller-server-role-using-server-manager"></a>サーバー マネージャーを使用してネットワーク コントローラー サーバーの役割をインストールします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックは、サーバー マネージャーを使用して、ネットワーク コントローラー サーバーの役割をインストールする方法について説明します。

>[!IMPORTANT]
>物理ホスト上で、ネットワーク コントローラー サーバーの役割を展開しないでください。 ネットワーク コントローラーを展開するには、Hyper-V 仮想マシンのネットワーク コントローラー サーバーの役割をインストールする必要があります \(VM\) Hyper-V ホストにインストールされています。 Windows PowerShell コマンドを使用してネットワーク コントローラーにホストを追加することでのソフトウェアがネットワーク定義 \(SDN\) Hyper\ V ホストを有効にする必要があります Vm 上で次の 3 つの異なる Hyper\ V ホストでネットワーク コントローラーをインストールした後**新規 NetworkControllerServer**します。 これにより、有効にすると、SDN ソフトウェア ロード バランサーが機能します。 詳細については、次を参照してください。[新規 NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)します。
  
ネットワーク コントローラーをインストールした後は、追加のネットワーク コントローラー構成の Windows PowerShell コマンドを使用する必要があります。 詳細については、次を参照してください。[展開ネットワーク コントローラーが Windows PowerShell を使用して](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)します。  
  
### <a name="to-install-network-controller"></a>ネットワーク コントローラーをインストールするには  
  
1.  サーバー マネージャーで、クリックして**管理**、] をクリックし、**追加の役割と機能**します。 追加の役割と機能のウィザードが開きます。 をクリックして**次**します。  
  
2.  **[インストールの種類**既定の設定を維持し、クリックして**次**します。  
  
3.  **移行先サーバーの選択**、クリックして、ネットワーク コントローラーをインストールするサーバーを選択**次**します。  
  
4.  **サーバーの役割の選択**で、**役割**、] をクリックして**ネットワーク コントローラー**します。  
  
    ![ネットワーク コントローラー サーバーの役割](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
5.  **ネットワーク コントローラーに必要な機能を追加する**] ダイアログ ボックスが開きます。 をクリックして**機能を追加する**します。  
  
    ![ネットワーク コントローラーの機能を追加します。](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_06.jpg)  
  
6.  **サーバーの役割の選択**、] をクリックして**次**します。  
  
    ![[次へ] をクリックします。](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
7.  **機能の選択**、] をクリックして**次**します。  
  
8.  **ネットワーク コントローラー**クリックして**次**します。  
  
9. **インストール オプションの確認**、選択内容を確認します。 ネットワーク コントローラーのインストールでは、ウィザードを実行した後、コンピューターを再起動する必要があります。 このため、] をクリックして**必要な場合に、移行先サーバーを自動的に再起動**します。 **追加の役割と機能のウィザード**] ダイアログ ボックスが開きます。 をクリックして**はい**します。  
  
    ![役割と機能のウィザードを追加します。](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_11.jpg)  
  
10. **インストール オプションの確認**、] をクリックして**インストール**します。  
  
11. 移行先サーバーで、ネットワーク コントローラー サーバーの役割をインストールし、サーバーを再起動し、します。  
  
12. コンピューターが再起動したら、コンピューターにログオンし、サーバー マネージャーを表示してネットワーク コントローラーのインストールを確認します。  
  
    ![サーバー マネージャー](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/nc_013.jpg)  
  
## <a name="see-also"></a>参照してください。  
[ネットワーク コントローラー](Network-Controller.md)  
  


