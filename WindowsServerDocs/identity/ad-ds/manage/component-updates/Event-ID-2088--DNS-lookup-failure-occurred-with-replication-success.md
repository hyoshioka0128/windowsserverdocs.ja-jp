---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: イベント ID 2088-レプリケーションの成功時に DNS 参照エラーが発生しました
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: f84fd7be45995e9e0b318b42c8b4152af244a9da
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823055"
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>イベント ID 2088: DNS 参照エラーが発生しましたが、レプリケーションは成功しました

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

    
    <developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
      <introduction>
    <para>When a destination domain controller running Windows Server 2003 with Service Pack 1 (SP1) receives Event ID 2088 in the Directory Service event log, attempts to resolve the globally unique identifier (GUID) in the alias (CNAME) resource record to an IP address for the source domain controller failed. However, the destination domain controller tried other means to resolve the name and succeeded by using either the fully qualified domain name (FQDN) or the NetBIOS name of the source domain controller. Although replication was successful, the Domain Name System (DNS) problem should be diagnosed and resolved. </para>
    <para>The following is an example of the event text: </para>
    <code>Log Name: Directory Service

    Source: Microsoft-Windows-ActiveDirectory_DomainService
    Date: 3/15/2008  9:20:11 AM
    Event ID: 2088
    Task Category: DS RPC Client 
    Level: Warning
    Keywords: Classic
    User: ANONYMOUS LOGON
    Computer: DC3.contoso.com
    Description:
    Active Directory could not use DNS to resolve the IP address of the 
    source domain controller listed below. To maintain the consistency 
    of Security groups, group policy, users and computers and their passwords, 
    Active Directory Domain Services successfully replicated using the NetBIOS 
    or fully qualified computer name of the source domain controller. 

無効な DNS 構成は、ログオン認証やネットワークリソースへのアクセスなど、この Active Directory Domain Services フォレスト内のメンバーコンピューター、ドメインコントローラー、またはアプリケーションサーバーに対する他の重要な操作に影響を与える可能性があります。 

このドメインコントローラーが DNS を使用してソースドメインコントローラーの IP アドレスを解決できるように、この DNS 構成エラーを直ちに解決する必要があります。 

代替サーバー名: DC1 失敗した DNS ホスト名: _msdcs 4a8717eb-8e58-456c-995a-c92e4add7e8e 

注: 既定では、10個を超えるエラーが発生した場合でも、12時間以内に最大10個の DNS エラーのみが表示されます。  個々のエラーイベントをすべてログに記録するには、次の診断レジストリ値を1に設定します。 

レジストリパス: HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS RPC クライアント 

ユーザーの操作: 

1) ソースドメインコントローラーが機能しなくなった場合、または別のコンピューター名または NTDSDSA オブジェクト GUID を使用してそのオペレーティングシステムが再インストールされている場合は、MSKB の記事216498に記載されている手順を使用して、ソースドメインコントローラーのメタデータを ntdsutil.exe で削除します。 

2) ソースドメインコントローラが Active Directory 実行されていて、ネットワーク上でアクセス可能であることを確認するために、「net view \\&lt;source DC name&gt;」または「ping &lt;source DC name&gt;」と入力します。 

3) ソースドメインコントローラが DNS サービスに有効な DNS サーバーを使用しており、ソースドメインコントローラのホストレコードと CNAME レコードが正しく登録されていることを確認します。これには、DNS 拡張バージョンの DCDIAG を使用します。<https://www.microsoft.com/dns> で利用可能な EXE 

dcdiag/test: dns 

4) この宛先ドメインコントローラが dns 拡張バージョンの DCDIAG を実行して、DNS サービスに対して有効な DNS サーバーを使用していることを確認してください。次のように、移行先ドメインコントローラーのコンソールで EXE コマンドを実行します。 

dcdiag/test: dns 

5) DNS エラーエラーの詳細な分析については、「KB 824449: <https://support.microsoft.com/?kbid=824449>」を参照してください。 

追加データエラー値: 11004 要求された名前は有効ですが、要求された型のデータが</code> 見つかりませんでした </introduction>
  <section>
    <title>診断</title>
    <content>
      <para>Dns のエイリアス (CNAME) リソースレコードを使用してソースドメインコントローラー名を解決できない場合は、dns のデータ伝達の誤りまたは遅延が原因である可能性があります。</para>
    </content>
  </section>
  <section>
    <title>解決策</title>
    <content>
      <para>&quot;イベント ID 2087 の説明に従って DNS テストを続行します。 <link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">dns 参照が失敗したため、レプリケーションが失敗</link>しました。&quot;</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>


