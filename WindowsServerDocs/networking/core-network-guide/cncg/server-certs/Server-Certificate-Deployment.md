---
title: サーバー証明書の展開
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: 1ae4384b-f4e4-41e8-bc5f-9ac41953bca4
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2105e2ccad69fcfdbc13e3201b4362e5c6b932e1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406275"
---
# <a name="server-certificate-deployment"></a>サーバー証明書の展開

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

エンタープライズ ルート証明機関 (CA) をインストールしを PEAP および EAP で使用するサーバー証明書を展開する次の手順に従います。  
  
> [!IMPORTANT]  
> Active Directory Certificate Services をインストールする前に、コンピューターの名前が静的 IP アドレスを持つコンピューターを構成、コンピューターをドメインに参加してください。 AD CS をインストールした後は、IP アドレスを変更するには、必要な場合が、コンピューター名またはコンピューターのドメインのメンバーシップを変更できません。 これらのタスクを実行する方法の詳細については、Windows Server を参照してください。&reg; 2016 [コア ネットワーク ガイド](../../Core-Network-Guide.md)します。  

  
-   [Web サーバー WEB1 をインストールする](../../../core-network-guide/cncg/server-certs/Install-the-Web-Server-WEB1.md)  
  
-   [DNS に WEB1 のエイリアス (CNAME) レコードを作成する](../../../core-network-guide/cncg/server-certs/Create-an-Alias-CNAME-Record-in-DNS-for-WEB1.md)  
  
-   [証明書失効リスト (Crl) を配布するように WEB1 を構成する](../../../core-network-guide/cncg/server-certs/Configure-WEB1-to-Distribute-Certificate-Revocation-Lists.md)  
  
-   [Capolicy.inf ファイルを準備する](../../../core-network-guide/cncg/server-certs/Prepare-the-CAPolicy-inf-File.md)  
  
-   [証明機関をインストールする](../../../core-network-guide/cncg/server-certs/Install-the-Certification-Authority.md)  
  
-   [CA1 で CDP および AIA 拡張機能を構成する](../../../core-network-guide/cncg/server-certs/Configure-the-CDP-and-AIA-Extensions-on-CA1.md)  
  
-   [CA 証明書と CRL を仮想ディレクトリにコピーする](../../../core-network-guide/cncg/server-certs/Copy-the-CA-Certificate-and-CRL-to-the-Virtual-Directory.md)  
  
-   [サーバー証明書テンプレートを構成する](../../../core-network-guide/cncg/server-certs/Configure-the-Server-Certificate-Template.md)  
  
-   [サーバー証明書の自動登録を構成する](../../../core-network-guide/cncg/server-certs/Configure-Server-Certificate-Autoenrollment.md)  
  
-   [グループポリシーの更新](../../../core-network-guide/cncg/server-certs/Refresh-Group-Policy.md)  
  
-   [サーバー証明書のサーバー登録を確認する](../../../core-network-guide/cncg/server-certs/Verify-Server-Enrollment-of-a-Server-Certificate.md)  
  
> [!NOTE]  
> このガイドの手順は含まれていません場合に、 **ユーザー アカウント制御** 続行の許可を要求するダイアログ ボックスが開きます。 このダイアログ ボックスを開いているながら、このガイドの手順を実行して、お客様の操作に応答 ダイアログ ボックスが開かれた場合はクリックして場合 **続行**します。  
  


