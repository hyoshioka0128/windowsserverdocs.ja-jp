---
title: 複数の Active Directory フォレスト内のリソースを管理する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: 82f8f382-246e-4164-8306-437f7a019e0f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 39d519f0d588a7c2ba6a671eeace14cfe788f6b0
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87517917"
---
# <a name="manage-resources-in-multiple-active-directory-forests"></a>複数の Active Directory フォレスト内のリソースを管理する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、複数の Active Directory フォレスト内のドメインコントローラー、DHCP サーバー、および DNS サーバーを IPAM を使用して管理する方法について説明します。

IPAM を使用してリモート Active Directory フォレスト内のリソースを管理するには、管理する各フォレストに、IPAM がインストールされているフォレストと双方向の信頼関係がある必要があります。

異なる Active Directory フォレストの検出プロセスを開始するには、サーバーマネージャーを開き、[IPAM] をクリックします。 IPAM クライアントコンソールで、[**サーバー検出の構成**] をクリックし、[**フォレストの取得**] をクリックします。 これにより、信頼されたフォレストとそのドメインを検出するバックグラウンドタスクが開始されます。 検出プロセスが完了したら、[**サーバー検出の構成**] をクリックすると、次のダイアログボックスが開きます。

![サーバー検出の設定](../../media/Manage-Resources-in-Multiple-Active-Directory-Forests/ipam_serverdiscovery.jpg)

>[!NOTE]
>\-Active Directory フォレスト間のシナリオでグループポリシーベースのプロビジョニングを行う場合は、信頼する側のドメイン dc ではなく、IPAM サーバーで次の Windows PowerShell コマンドレットを実行してください。 たとえば、IPAM サーバーがフォレスト corp.contoso.com に参加していて、信頼する側のフォレストが fabrikam.com である場合、corp.contoso.com の IPAM サーバーで次の Windows PowerShell コマンドレットを実行して、fabrikam.com フォレストでグループポリシーベースのプロビジョニングを行うことができ \- ます。 このコマンドレットを実行するには、fabrikam.com フォレストの Domain Admins グループのメンバーである必要があります。

```powershell
    Invoke-IpamGpoProvisioning -Domain fabrikam.COM -GpoPrefixName IPAMSERVER -IpamServerFqdn IPAM.CORP.CONTOSO.COM
```

[**サーバー検出の構成**] ダイアログボックスで、[**フォレストを選択**する] をクリックし、IPAM で管理するフォレストを選択します。 また、管理するドメインを選択し、[**追加**] をクリックします。

**[検出するサーバーの役割を選択**してください] で、管理するドメインごとに、検出するサーバーの種類を指定します。 [**ドメインコントローラー**]、[ **DHCP サーバー**]、[ **DNS サーバー**] のオプションがあります。

既定では、ドメインコントローラー、DHCP サーバー、および DNS サーバーが検出されるので、これらの種類のサーバーのいずれかを検出しない場合は、そのオプションのチェックボックスをオフにしてください。

上の図の例では、IPAM サーバーが contoso.com フォレストにインストールされ、fabrikam.com フォレストのルートドメインが IPAM 管理用に追加されています。 選択したサーバーの役割により、IPAM は fabrikam.com ルートドメインと contoso.com ルートドメイン内のドメインコントローラー、DHCP サーバー、および DNS サーバーを検出して管理できます。

フォレスト、ドメイン、およびサーバーの役割を指定したら、[ **OK]** をクリックします。 IPAM によって検出が実行され、探索が完了すると、ローカルとリモートの両方のフォレストのリソースを管理できます。
