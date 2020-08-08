---
ms.assetid: 1a6740e6-5b6d-41f8-9ec4-32cdbee3e1bb
title: 境界クライアントとインターネットクライアントの名前解決
author: billmath
manager: femila
ms.date: 04/13/2020
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 050d1ddd8d04e288c6e480bed2d9e24146198020
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972129"
---
# <a name="name-resolution-for-perimeter-and-internet-clients"></a>境界クライアントとインターネットクライアントの名前解決


\( \) 1 つ以上のドメインネームシステムの DNS ゾーンが境界ネットワークとインターネットクライアントの両方にサービスを提供する Active Directory フェデレーションサービス (AD FS) AD FS シナリオで、フェデレーションサーバープロキシの名前解決が正常に機能するようにするには、 \( \) 次のタスクを完了する必要があります。

-   制御するインターネットゾーンの DNS は、AD FS ホスト名に対するすべてのインターネットクライアント要求をフェデレーションサーバープロキシに解決するように構成する必要があります。 これを実現するには、ホスト \( a \) リソースレコードをフェデレーションサーバープロキシのインターネット DNS ゾーンに追加します。

-   AD FS ホスト名に対するすべての受信クライアント要求をフェデレーションサーバーに解決するように、境界ネットワークの DNS を構成する必要があります。 これを実現するには、ホスト \( a \) リソースレコードをフェデレーションサーバープロキシの境界 DNS ゾーンに追加します。

> [!NOTE]
> \( \) フェデレーションサーバーのリソースレコードが、企業ネットワークの DNS に既に作成されていることを前提としています。 このレコードがまだ存在しない場合は、このレコードを作成してから、次の手順を実行します。 フェデレーションサーバーのホスト a リソースレコードを作成する方法の詳細につい \( \) ては、「 [Add A host &#40;a&#41; resource Record To a federation server](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)」を参照してください。

## <a name="add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>\( \) フェデレーションサーバープロキシのインターネット DNS ゾーンにホスト a リソースレコードを追加する
インターネット上のクライアントコンピューターが、新しく展開されたフェデレーションサーバープロキシを使用してフェデレーションサーバーに正常にアクセスできるようにするには、まず、 \( \) 制御するインターネット DNS ゾーンにホスト a リソースレコードを作成する必要があります。 このリソースレコードは、アカウントフェデレーションサーバーのホスト名を解決し \( ます。たとえば、fs.fabrikam.com は、 \) \( 境界ネットワーク内の131.107.27.68 など、アカウントフェデレーションサーバープロキシの IP アドレス \) です。

> [!NOTE]
> Windows 2000 Server、Windows Server 2003、または Windows Server 2008 を実行する DNS サーバーを DNS サーバーサービスと共に使用して、インターネット DNS ゾーンを制御することを前提としています。

**Administrators**、またはそれと同等のメンバーシップが、この手順を実行するために最低限必要なメンバーシップです。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。

#### <a name="to-add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>ホスト a \( \) リソースレコードをフェデレーションサーバープロキシのインターネット DNS ゾーンに追加するには

1.  インターネット DNS ゾーンの DNS サーバーで、DNS スナップインを開き \- ます。

2.  コンソールツリーで、 \- 該当する前方参照ゾーンを右クリックし、[**新しいホスト \( A または AAAA \) **] をクリックします。

3.  [**名前**] に、フェデレーションサーバーのコンピューター名のみを入力します。 たとえば、完全修飾ドメイン名 FQDN fs.fabrikam.com の場合は、 \( \) 「 **fs**」と入力します。

4.  [ **Ip アドレス**] に、新しいフェデレーションサーバープロキシの ip アドレス (たとえば、131.107.27.68) を入力します。

5.  **[ホストの追加]** をクリックします。

## <a name="add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>\( \) フェデレーションサーバープロキシの境界 DNS ゾーンにホスト a リソースレコードを追加する
インターネットクライアント要求がフェデレーションサーバープロキシによって正常に処理され、インターネット DNS ゾーンによって解決された後にフェデレーションサーバーに接続できるように、 \( \) 境界 DNS ゾーン内にホスト a リソースレコードを作成する必要があります。 このリソースレコードは、アカウントフェデレーションサーバー \( (たとえば、fs) のホスト名を解決します。 fabrikam.com は、 \) \( 企業ネットワーク内の192.168.1.4 など、アカウントフェデレーションサーバーの IP アドレスに \) なります。

> [!NOTE]
> &reg;境界 dns ゾーンを制御するために、Dns サーバーサービスを使用して、windows 2000 server、Windows server 2003、Windows server 2008、または Windows server 2012 を実行している dns サーバーを使用していることを前提としています。

**Administrators**、またはそれと同等のメンバーシップが、この手順を実行するために最低限必要なメンバーシップです。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。

#### <a name="to-add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>ホスト a \( \) リソースレコードをフェデレーションサーバープロキシの境界 DNS ゾーンに追加するには

1.  境界ネットワークの DNS サーバーで、 **dns スナップイン \- を**開きます。

2.  コンソールツリーで、 \- 該当する前方参照ゾーンを右クリックし、[**新しいホスト \( A または AAAA \) **] をクリックします。

3.  [**名前**] に、フェデレーションサーバーのコンピューター名のみを入力します。 たとえば、完全修飾ドメイン名 fs.fabrikam.com の場合は、「**fs**」と入力します。

4.  [ **Ip アドレス**] ボックスに、企業ネットワーク内のフェデレーションサーバーの ip アドレス (たとえば、192.168.1.4) を入力します。

5.  **[ホストの追加]** をクリックします。

## <a name="additional-references"></a>その他の参照情報
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)

[フェデレーション サーバー プロキシの名前解決の要件](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807055(v=ws.11))

