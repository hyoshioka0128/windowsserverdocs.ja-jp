---
title: Web サーバー WEB1 をインストールします。
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.technology: networking
ms.topic: article
ms.assetid: f51c9e38-98bb-49c1-9d39-427d07021499
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2d68b83f24a9948d42ee425218646cc5f44d5f4a
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409643"
---
# <a name="install-the-web-server-web1"></a>Web サーバー WEB1 をインストールします。

>適用先:Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 で Web サーバー (IIS) ロールは、信頼性の高い web サイト、サービス、およびアプリケーションをホストするため、セキュリティで保護された、管理が容易なモジュール化および拡張可能なプラットフォームを提供します。 IIS では、インターネット、イントラネットまたはエクストラネット上のユーザーと情報を共有できます。 IIS は、IIS、ASP.NET、FTP サービス、PHP、および Windows Communication Foundation (WCF) を一体化した統合 web プラットフォームです。

サーバー証明書を展開するときに、Web サーバーは証明機関 (CA) の証明書失効リスト (CRL) を公開できる場所を提供します。 発行した後、CRL は、認証プロセス中にこの一覧を別のコンピュータで提示された証明書が取り消されていないことを確認に使用できるように、ネットワーク上のすべてのコンピューターにアクセスできます。

失効と CRL に証明書がある場合は、認証作業は失敗し、コンピューターが保護を無効になっている証明書を持つエンティティを信頼します。

Web サーバー (IIS) の役割をインストールする前に、サーバー名と IP アドレスを構成して、コンピューターをドメインに参加することを確認します。

## <a name="to-install-the-web-server-iis-server-role"></a>Web サーバー (IIS) サーバーの役割をインストールするには
この手順を完了するには、**Administrators** グループのメンバーである必要があります。

>[!NOTE]
>Windows PowerShell を使用してこの手順を実行するには、PowerShell と、次のコマンドを入力し、ENTER キーを押します。
`Install-WindowsFeature Web-Server -IncludeManagementTools`

1.  サーバー マネージャーで、[**管理**] をクリックし、[**役割と機能の追加**] をクリックします。 役割と機能の追加ウィザードが起動されます。
2.  **[開始する前に]** で **[次へ]** をクリックします。

**メモ**役割と機能の追加ウィザードを以前に実行していて、[**既定でこのページ**を表示しない] を選択した場合は、役割と機能の追加ウィザードの [**開始する前に**] ページが表示されません。

3. **[インストールの種類]** ページで、**[次へ]** をクリックします。
4. [**サーバーの選択**] ページで、[**次へ**] をクリックします。
5. **サーバーの役割** ] ページで、[ **Web サーバー (IIS)**, 、] をクリックし、 **次**します。
6. 既定の Web サーバーの設定をすべて受け入れるまで **[次へ]** をクリックしてから、**[インストール]** をクリックします。
7. すべてのインストールに成功したことを確認し、**[閉じる]** をクリックします。
