---
title: DNS に WEB1 のエイリアス (CNAME) レコードを作成する
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: bfae23f0-ae12-486b-94fe-50a137e141a5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9a966ab2883e22173ecf3e64e87d2a4b7a9c57d2
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995592"
---
# <a name="create-an-alias-cname-record-in-dns-for-web1"></a>\( \) WEB1 の DNS にエイリアス CNAME レコードを作成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、 \( Web サーバーのエイリアス正規名 CNAME \) リソースレコードをドメインコントローラーの DNS 内のゾーンに追加できます。 CNAME レコードを使用すると、複数の名前を使用して1つのホストを指定することができます。これにより、ファイル転送プロトコルの \( FTP \) サーバーと Web サーバーの両方を同じコンピューターにホストするなどの操作を簡単に行うことができます。

このため、Web サーバーを使用して、証明機関の CA の証明書失効リストの CRL をホストする \( \) だけでなく、 \( \) FTP や Web サーバーなどの追加のサービスを実行することもできます。

この手順を実行するときに、**エイリアス名**とその他の変数を、配置に適した値に置き換えます。

この手順を実行するには、 **Domain Admins**のメンバーである必要があります。

## <a name="to-add-an-alias-cname-resource-record-to-a-zone"></a>エイリアス \( CNAME \) リソースレコードをゾーンに追加するには

>[!NOTE]
>Windows PowerShell を使用してこの手順を実行するには、「 [DnsServerResourceRecordCName](/powershell/module/dnsserver/add-dnsserverresourcerecordcname?view=winserver2012r2-ps)」を参照してください。

1.  DC1 の [サーバーマネージャーで、[**ツール**] をクリックし、[ **DNS**] をクリックします。 DNS マネージャー Microsoft 管理コンソール (MMC) が開きます。

2.  コンソールツリーで、[**前方参照ゾーン**] をダブルクリックし、エイリアスリソースレコードを追加する前方参照ゾーンを右クリックして、[**新しいエイリアス \( \) CNAME**] をクリックします。 [**新しいリソースレコード**] ダイアログボックスが表示されます。

3.  [**エイリアス名**] に、エイリアス名として「 **pki**」と入力します。

4.  [**エイリアス名**] の値を入力すると、**完全修飾ドメイン名の \( FQDN \) **がダイアログボックスに自動的に入力されます。 たとえば、エイリアス名が "pki" で、ドメインが corp.contoso.com の場合、値**pki.corp.contoso.com**は自動的に入力されます。

5.  [ ** \( \) ターゲットホストの完全修飾ドメイン名の fqdn**] に、Web サーバーの fqdn を入力します。 たとえば、Web サーバーの名前が WEB1 で、ドメインが corp.contoso.com の場合は、「 **WEB1.corp.contoso.com**」と入力します。

6.  [ **OK** ] をクリックして、新しいレコードをゾーンに追加します。