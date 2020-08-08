---
title: DNS リソース レコードの管理
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 7b66c09d-e401-4f70-9a2a-6047dd629bfa
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f648649ac4f874089c958578ff1291f0e3dc9c66
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966439"
---
# <a name="dns-resource-record-management"></a>DNS リソース レコードの管理

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、IPAM を使用して DNS リソースレコードを管理する方法について説明します。

> [!NOTE]
> このトピックに加えて、次の DNS リソースレコード管理のトピックも参照してください。
>
> -   [DNS リソースレコードを追加する](../../technologies/ipam/Add-a-DNS-Resource-Record.md)
> -   [DNS リソースレコードの削除](../../technologies/ipam/Delete-DNS-Resource-Records.md)
> -   [DNS リソースレコードのビューをフィルター処理する](../../technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)
> -   [特定の IP アドレスの DNS リソースレコードを表示する](../../technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-Address.md)

## <a name="resource-record-management-overview"></a>リソースレコード管理の概要
Windows Server 2016 で IPAM を展開するときに、サーバーの検出を実行して DHCP サーバーと DNS サーバーを IPAM サーバー管理コンソールに追加することができます。 IPAM サーバーは、管理するように構成されている DNS サーバーから6時間ごとに DNS データを動的に収集します。 IPAM は、この DNS データを格納するローカルデータベースを保持します。 IPAM は、サーバーデータが収集された日時の通知を提供するだけでなく、DNS サーバーからのデータ収集が行われる次の日と時間を通知します。

次の図の黄色のステータスバーは、IPAM 通知のユーザーインターフェイスの場所を示しています。

![IPAM 通知](../../media/DNS-Resource-Record-Management/ipam_DataCollection_01.jpg)

収集される DNS データには、DNS ゾーンとリソースレコードの情報が含まれます。 優先 DNS サーバーからゾーン情報を収集するように IPAM を構成できます。  IPAM は、ファイルベースのゾーンと Active Directory ゾーンの両方を収集します。

> [!NOTE]
> IPAM は、ドメインに参加している Microsoft DNS サーバーからのみデータを収集します。 サードパーティの DNS サーバーとドメインに参加していないサーバーは、IPAM ではサポートされていません。

IPAM によって収集される DNS リソースレコードの種類の一覧を次に示します。

-   AFS データベース

-   ATM アドレス

-   CNAME

-   DHCID

-   DNAME

-   ホスト A または AAAA

-   ホスト情報

-   回線

-   MX

-   ネーム サーバー

-   ポインター (PTR)

-   責任者

-   ルート

-   サービスの場所

-   SOA

-   SRV

-   テキスト

-   よく知られているサービス

-   WINS

-   WINS-R

-   X.25

Windows Server 2016 では、IPAM は IP アドレスインベントリ、DNS ゾーン数、DNS リソースレコード間の統合を提供します。

-   IPAM を使用すると、DNS リソースレコードから IP アドレスインベントリを自動的に作成できます。

-   IP アドレスインベントリは、DNS A と AAAA リソースレコードから手動で作成できます。

-   特定の DNS ゾーンの DNS リソースレコードを表示し、種類、IP アドレス、リソースレコードデータ、およびその他のフィルターオプションに基づいてレコードをフィルター処理できます。

-   IPAM は、IP アドレス範囲と DNS 逆引き参照ゾーン間のマッピングを自動的に作成します。

-   逆引き参照ゾーンに存在し、その IP アドレス範囲に含まれる PTR レコードの IP アドレスが IPAM によって作成されます。 必要に応じて、このマッピングを手動で変更することもできます。

Ipam を使用すると、IPAM コンソールからリソースレコードに対して次の操作を実行できます。

-   DNS リソースレコードを作成する

-   DNS リソースレコードの編集

-   DNS リソース レコードの削除

-   関連付けられたリソースレコードの作成

Ipam では、IPAM コンソールを使用して行ったすべての DNS 構成の変更が自動的にログに記録されます。

## <a name="see-also"></a>参照
[IPAM の管理](Manage-IPAM.md)



