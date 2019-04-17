---
title: DNS に WEB1 のエイリアス (CNAME) レコードを作成します。
description: このトピックの「802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部である
manager: brianlic
ms.topic: article
ms.assetid: bfae23f0-ae12-486b-94fe-50a137e141a5
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 65f10efe1cfd2866fb99406bf031197f6268b05b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="create-an-alias-cname-record-in-dns-for-web1"></a>DNS に WEB1 のエイリアス \(CNAME\) レコードを作成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、Web サーバーのドメイン コントローラーで DNS ゾーンにエイリアス正規名 \(CNAME\) リソース レコードを追加します。 CNAME レコードと容易をファイル転送プロトコル \(FTP\) サーバーと同じコンピューター上の Web サーバーの両方のホストとしてこのような管理を行うには、1 つのホストを指す複数の名前を使用できます。   
  
このためは自由に証明書の失効をホストする Web サーバーを使用して \(CRL\) を証明機関の一覧を FTP または Web サーバーなどの他のサービスを実行するためにも \(CA\) します。  
  
この手順を実行するときに置き換える**エイリアス名**と展開に適切な値を持つその他の変数です。  
  
この手順を実行するには、メンバーである**Domain Admins**します。  
  
## <a name="to-add-an-alias-cname-resource-record-to-a-zone"></a>エイリアス \(CNAME\) リソース レコードをゾーンに追加するには  
  
>[!NOTE]  
>Windows PowerShell を使用してこの手順を実行する、次を参照してください。[追加 DnsServerResourceRecordCName](https://technet.microsoft.com/library/jj649894(v=wps.630).aspx)します。  
  
1.  DC1 で、サーバー マネージャーで、をクリックして**ツール**] をクリックし、**DNS**します。 DNS マネージャー Microsoft 管理コンソール (MMC) を開きます。  
  
2.  コンソール ツリーで、ダブルクリック**前方参照ゾーン**、エイリアス リソース レコードを追加したい前方参照ゾーンを右クリックして**新しいエイリアス \(CNAME\)**します。 **新しいリソース レコード**] ダイアログ ボックスが開きます。  
  
3.  **エイリアス名**、エイリアス名を入力**pki**します。  
  
4.  値を入力すると**エイリアス名**、**完全修飾ドメイン名 \(FQDN\)** ] ダイアログ ボックスでの自動塗りつぶしします。 たとえば場合は、エイリアス名は"pki"であり、ドメインは corp.contoso.com、値**pki.corp.contoso.com**はオートフィルをします。  
  
5.  **ターゲット ホストに対するする完全修飾ドメイン名 \(FQDN\)**、Web サーバーの FQDN を入力します。 たとえば、WEB1 という名前の Web サーバーは、ドメインが corp.contoso.com 場合は、入力**WEB1.corp.contoso.com**します。  
  
6.  をクリックして**OK**に新しいレコードをゾーンに追加します。  
  

