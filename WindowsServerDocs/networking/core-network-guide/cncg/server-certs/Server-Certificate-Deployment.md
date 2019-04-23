---
title: サーバー証明書の展開
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: 1ae4384b-f4e4-41e8-bc5f-9ac41953bca4
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 751c5c5958b3d06ae0f4b701e4d6e10a7fef19dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858493"
---
# <a name="server-certificate-deployment"></a>サーバー証明書の展開

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

エンタープライズ ルート証明機関 (CA) をインストールしを PEAP および EAP で使用するサーバー証明書を展開する次の手順に従います。  
  
> [!IMPORTANT]  
> Active Directory Certificate Services をインストールする前に、コンピューターの名前が静的 IP アドレスを持つコンピューターを構成、コンピューターをドメインに参加してください。 AD CS をインストールした後は、IP アドレスを変更するには、必要な場合が、コンピューター名またはコンピューターのドメインのメンバーシップを変更できません。 これらのタスクを実行する方法の詳細については、Windows Server を参照してください。&reg; 2016 [コア ネットワーク ガイド](../../Core-Network-Guide.md)します。  

  
-   [Web サーバー WEB1 をインストールします。](../../../core-network-guide/cncg/server-certs/Install-the-Web-Server-WEB1.md)  
  
-   [WEB1 の dns エイリアス (CNAME) レコードを作成します。](../../../core-network-guide/cncg/server-certs/Create-an-Alias-CNAME-Record-in-DNS-for-WEB1.md)  
  
-   [証明書失効リスト (Crl) を配布するように WEB1 を構成します。](../../../core-network-guide/cncg/server-certs/Configure-WEB1-to-Distribute-Certificate-Revocation-Lists.md)  
  
-   [CAPolicy inf ファイルを準備します。](../../../core-network-guide/cncg/server-certs/Prepare-the-CAPolicy-inf-File.md)  
  
-   [証明機関をインストールします。](../../../core-network-guide/cncg/server-certs/Install-the-Certification-Authority.md)  
  
-   [CA1 で CDP および AIA 拡張機能を構成します。](../../../core-network-guide/cncg/server-certs/Configure-the-CDP-and-AIA-Extensions-on-CA1.md)  
  
-   [CA の証明書と CRL を仮想ディレクトリにコピーします。](../../../core-network-guide/cncg/server-certs/Copy-the-CA-Certificate-and-CRL-to-the-Virtual-Directory.md)  
  
-   [サーバー証明書テンプレートを構成します。](../../../core-network-guide/cncg/server-certs/Configure-the-Server-Certificate-Template.md)  
  
-   [サーバー証明書の自動登録を構成します。](../../../core-network-guide/cncg/server-certs/Configure-Server-Certificate-Autoenrollment.md)  
  
-   [グループ ポリシーを更新](../../../core-network-guide/cncg/server-certs/Refresh-Group-Policy.md)  
  
-   [サーバー証明書のサーバーの登録を確認します。](../../../core-network-guide/cncg/server-certs/Verify-Server-Enrollment-of-a-Server-Certificate.md)  
  
> [!NOTE]  
> このガイドの手順は含まれていません場合に、 **ユーザー アカウント制御** 続行の許可を要求するダイアログ ボックスが開きます。 このダイアログ ボックスを開いているながら、このガイドの手順を実行して、お客様の操作に応答 ダイアログ ボックスが開かれた場合はクリックして場合 **続行**します。  
  


