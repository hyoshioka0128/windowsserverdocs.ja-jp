---
title: Web サーバー WEB1 をインストールします。
description: このトピックの「802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f51c9e38-98bb-49c1-9d39-427d07021499
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e818eac49719b394a2c73cc125a2e7ba9ea80c82
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-web-server-web1"></a>Web サーバー WEB1 をインストールします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 で Web サーバー (IIS) 役割は、Web サイト、サービス、およびアプリケーションを確実にホストするため、セキュリティで保護された、管理が容易なモジュールで拡張性の高いプラットフォームを提供します。 Iis では、インターネット、イントラネット、またはエクストラネット上のユーザーと情報を共有できます。 IIS は、IIS、ASP.NET、FTP サービス、PHP、および Windows Communication Foundation (WCF) を一体化した統合 Web プラットフォームです。  

サーバー証明書を展開するときに、Web サーバーで、場所、証明機関 (CA) の証明書失効リスト (CRL) を公開することができます。 発行した後、CRL は、他のコンピューターによって提示される証明書が失効していないことを確認する認証プロセス中にこのリストを使用できるように、ネットワーク上のすべてのコンピューターにアクセスできます。   

失効と CRL に証明書がある場合は、認証作業は失敗し、コンピューターが保護を無効になっている証明書を持つエンティティを信頼する側からです。  

Web サーバー (IIS) 役割をインストールする前に、サーバー名と IP アドレスを構成して、コンピューターをドメインに参加することを確認します。  

## <a name="to-install-the-web-server-iis-server-role"></a>Web サーバー (IIS) サーバー役割をインストールするには  
この手順を完了するには、メンバーである、**管理者**グループ。  

>[!NOTE]  
>Windows PowerShell を使用してこの手順を実行するには、PowerShell と、次のコマンドを入力し、Enter キーを押します。  
`Install-WindowsFeature Web-Server -IncludeManagementTools`  

1.  サーバー マネージャーで、クリックして**管理**、] をクリックし、**追加の役割と機能**します。 追加の役割と機能のウィザードが開きます。  
2.  **開始する前に**、] をクリックして**次**します。  

**注:**   
**開始する前に**以前に実行した追加の役割と機能のウィザードと選択した場合、追加の役割と機能のウィザード ページは表示されません**既定でこのページをスキップ**その時点でします。  

3.  **インストールの種類**] ページで [**次**します。  
4.  **サーバーの選択**] ページで [**次**します。  
5.  **サーバーの役割**] ページで、[ **Web サーバー (IIS)**、] をクリックし、**[次へ]**します。  
6.  をクリックして**次**受け入れるまですべて、既定の web サーバーの設定] をクリック**インストール**します。  
7.  すべてのインストールが成功すると、いることを確認し、をクリックして**閉じる**します。
