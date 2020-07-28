---
title: DNS クライアントのトラブルシューティング
description: この記事では、クライアント側からの DNS の問題をトラブルシューティングする方法について説明します。
manager: dcscontentpm
ms.technology: networking-dns
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: 2a9b44807ae6bc9f4c446d4af2150caf09955899
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182338"
---
# <a name="troubleshooting-dns-clients"></a>DNS クライアントのトラブルシューティング

この記事では、DNS クライアントからの問題をトラブルシューティングする方法について説明します。

## <a name="check-ip-configuration"></a>IP 構成の確認

1. クライアントコンピューターで管理者としてコマンドプロンプトウィンドウを開きます。

2. 次のコマンドを実行します。

   ```cmd
   ipconfig /all
   ```

3. クライアントが接続されて使用されているネットワークの有効な IP アドレス、サブネットマスク、およびデフォルトゲートウェイを持っていることを確認します。

4. 出力に表示されている DNS サーバーを確認し、表示されている IP アドレスが正しいことを確認します。

5. 出力の接続固有の DNS サフィックスを確認し、それが正しいことを確認します。

クライアントに有効な TCP/IP 構成がない場合は、次のいずれかの方法を使用します。

* 動的に構成されたクライアントの場合は、コマンドを使用して `ipconfig /renew` 手動でクライアントに対して、DHCP サーバーによる IP アドレス構成の更新を強制します。

* 静的に構成されたクライアントの場合は、クライアントの TCP/IP プロパティを変更して、有効な構成設定を使用するようにするか、またはネットワークに対する DNS 構成を行います。

## <a name="check-network-connection"></a>ネットワーク接続の確認

### <a name="ping-test"></a>Ping テスト

優先 DNS サーバーに IP アドレスで ping を実行して、クライアントが優先する (または代替の) DNS サーバーに接続できることを確認します。

たとえば、クライアントが優先 DNS サーバー10.0.0.1 を使用する場合は、コマンドプロンプトで次のコマンドを実行します。

```cmd
ping 10.0.0.1
```

構成済みの DNS サーバーが IP アドレスの直接 ping に応答しない場合は、問題の原因がクライアントと DNS サーバー間のネットワーク接続の可能性が高いことを示しています。 その場合は、TCP/IP ネットワークのトラブルシューティングの基本的な手順に従って、問題を解決してください。 Ping コマンドを機能させるには、ファイアウォールを介して ICMP トラフィックを許可する必要があることに注意してください。

### <a name="dns-query-tests"></a>DNS クエリテスト

Dns クライアントが DNS サーバーコンピューターに対して ping を実行できる場合は、次のコマンドを使用して、 `nslookup` サーバーが dns クライアントに応答できるかどうかをテストします。 Nslookup ではクライアントの DNS キャッシュを使用しないため、名前解決では、クライアントの構成済みの DNS サーバーが使用されます。

#### <a name="test-a-client"></a>クライアントをテストする

```cmd
nslookup <client>
```

たとえば、クライアントコンピューターに**client1**という名前が付けられている場合は、次のコマンドを実行します。

```cmd
nslookup client1
```

正常な応答が返されない場合は、次のコマンドを実行してみてください。

```cmd
nslookup <fqdn of client>
```

たとえば、FQDN が**client1.corp.contoso.com**の場合は、次のコマンドを実行します。

```cmd
nslookup client1.corp.contoso.com.
```

> [!NOTE]
> このテストを実行するときは、末尾のピリオドを含める必要があります。

FQDN が正常に検出されても、短い名前が見つからない場合は、NIC の [TCP/IP の詳細設定] の [DNS] タブで DNS サフィックスの構成を確認します。 詳細については、「 [DNS 解決の構成](/previous-versions/tn-archive/dd163570(v=technet.10)#configuring-dns-resolution)」を参照してください。

#### <a name="test-the-dns-server"></a>DNS サーバーをテストする

```cmd
nslookup <DNS Server>
```

たとえば、DNS サーバーに DC1 という名前が付けられている場合は、次のコマンドを実行します。

```cmd
nslookup dc1
```
前のテストが成功した場合は、このテストも成功する必要があります。 このテストが成功しなかった場合は、DNS サーバーへの接続を確認します。

#### <a name="test-the-failing-record"></a>失敗したレコードをテストする

```cmd
nslookup <failed internal record>
```

たとえば、失敗したレコードが**app1.corp.contoso.com**であった場合は、次のコマンドを実行します。

```cmd
nslookup app1.corp.contoso.com
```

#### <a name="test-a-public-internet-address"></a>パブリックインターネットアドレスをテストする

```cmd
nslookup <external name>
```

次に例を示します。
```cmd
nslookup bing.com
```

これらの4つのテストがすべて成功した場合は、を実行して、失敗した `ipconfig /displaydns` 名前の出力を確認します。 失敗した名前の下に "名前が存在しません" と表示される場合は、否定応答が DNS サーバーから返され、クライアントにキャッシュされていました。

この問題を解決するには、を実行してキャッシュをクリアし `ipconfig /flushdns` ます。

## <a name="next-step"></a>次のステップ

名前解決がまだ失敗する場合は、「 [DNS サーバーのトラブルシューティング](troubleshoot-dns-server.md)」セクションを参照してください。
