---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: イベント ID 2088-レプリケーションの成功時に DNS 参照エラーが発生しました
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 9dbb7debbca8d1625ebe975a051ed8b607d1ddd0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943287"
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>イベント ID 2088: DNS 参照エラーが発生しましたが、レプリケーションは成功しました

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Windows Server 2003 Service Pack 1 (SP1) を実行している移行先ドメインコントローラーが、ディレクトリサービスイベントログでイベント ID 2088 を受信すると、は、エイリアス (CNAME) リソースレコードのグローバル一意識別子 (GUID) をソースドメインコントローラーの IP アドレスに解決しようとして失敗します。 ただし、宛先ドメインコントローラは、名前を解決するための他の手段を試して、完全修飾ドメイン名 (FQDN) またはソースドメインコントローラの NetBIOS 名のいずれかを使用して成功しました。 レプリケーションは成功しましたが、ドメインネームシステム (DNS) の問題を診断して解決する必要があります。

イベントテキストの例を次に示します。

```
Log Name: Directory Service
Source: Microsoft-Windows-ActiveDirectory_DomainService
Date: 3/15/2008  9:20:11 AM
Event ID: 2088
Task Category: DS RPC Client
Level: Warning
Keywords: Classic
User: ANONYMOUS LOGON
Computer: DC3.contoso.com
Description:
Active Directory could not use DNS to resolve the IP address of the source domain controller listed below. To maintain the consistency of Security groups, group policy, users and computers and their passwords, Active Directory Domain Services successfully replicated using the NetBIOS or fully qualified computer name of the source domain controller.
```

無効な DNS 構成は、ログオン認証やネットワークリソースへのアクセスなど、この Active Directory Domain Services フォレスト内のメンバーコンピューター、ドメインコントローラー、またはアプリケーションサーバーに対する他の重要な操作に影響を与える可能性があります。

このドメインコントローラーが DNS を使用してソースドメインコントローラーの IP アドレスを解決できるように、この DNS 構成エラーを直ちに解決する必要があります。

代替サーバー名: DC1 失敗した DNS ホスト名: _msdcs 4a8717eb-8e58-456c-995a-c92e4add7e8e

注: 既定では、10個を超えるエラーが発生した場合でも、12時間以内に最大10個の DNS エラーのみが表示されます。  個々のエラーイベントをすべてログに記録するには、次の診断レジストリ値を1に設定します。

レジストリパス: HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS RPC クライアント

ユーザーの操作:

1) ソースドメインコントローラーが機能しなくなった場合、または別のコンピューター名または NTDSDSA オブジェクト GUID を使用してそのオペレーティングシステムが再インストールされている場合は、MSKB の記事216498に記載されている手順に従って、ntdsutil.exe でソースドメインコントローラーのメタデータを削除します。

2) ソースドメインコントローラが Active Directory 実行されていて、ネットワーク上で "net view \\ <source DC name> " または "ping" と入力してアクセス可能であることを確認し <source DC name> ます。

3) ソースドメインコントローラが DNS サービスに有効な DNS サーバーを使用しており、ソースドメインコントローラのホストレコードと CNAME レコードが正しく登録されていることを確認します。これには、で利用可能な DCDIAG.EXE の DNS 拡張バージョンを使用します。<https://www.microsoft.com/dns>

dcdiag/test: dns

4) 次のように、宛先ドメインコントローラのコンソールで DCDIAG.EXE コマンドの DNS 拡張バージョンを実行して、dns サービスに対して有効な DNS サーバーを使用していることを確認します。

dcdiag/test: dns

5) DNS エラーエラーの詳細な分析については、KB 824449 を参照してください。<https://support.microsoft.com/?kbid=824449>

追加データエラー値: 11004 要求された名前は有効ですが、要求された種類のデータが見つかり </code> ませんでした</introduction>
  <section>
    <title>診断</title>
    <content>
      <para>Dns のエイリアス (CNAME) リソースレコードを使用してソースドメインコントローラー名を解決できない場合は、dns のデータ伝達の誤りまたは遅延が原因である可能性があります。</para>
    </content>
  </section>
  <section>
    <title>解決方法</title>
    <content>
      <para>「 &quot; <link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">イベント ID 2087: dns 参照の失敗によってレプリケーションが失敗する原因となっ</link>た dns のテスト」の説明に従って、dns のテストを続行します。&quot;</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>
