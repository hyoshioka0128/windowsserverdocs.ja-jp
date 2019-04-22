---
title: DNS に WEB1 のエイリアス (CNAME) レコードを作成する
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: bfae23f0-ae12-486b-94fe-50a137e141a5
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 442ee8b70311eaad3f0b3f263003786b6beab8bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813163"
---
# <a name="create-an-alias-cname-record-in-dns-for-web1"></a>エイリアスを作成\(CNAME\) WEB1 の dns レコード

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

この手順を使用するにはエイリアスの正規名を追加する\(CNAME\)ドメイン コント ローラー上で DNS ゾーンに、Web サーバーのリソース レコード。 単一のホストを簡単にファイル転送プロトコルなどのホストの両方を行うことをポイントする 1 つ以上の名前を使用する CNAME レコードでは、 \(FTP\)サーバーと同じコンピューター上の Web サーバー。   
  
このためは、Web サーバーを使用して、証明書失効リストをホストする自由\(CRL\)証明機関の\(CA\)および FTP または Web サーバーなどの追加サービスを実行するためです。  
  
この手順を実行するときに置き換える**エイリアス名**と展開に適切な値を持つその他の変数。  
  
この手順を実行する**Domain Admins**します。  
  
## <a name="to-add-an-alias-cname-resource-record-to-a-zone"></a>別名を追加する\(CNAME\)リソース レコードをゾーン  
  
>[!NOTE]  
>この手順を実行するには、Windows PowerShell を使用して、参照してください。[追加 DnsServerResourceRecordCName](https://technet.microsoft.com/library/jj649894(v=wps.630).aspx)します。  
  
1.  Dc1 のサーバー マネージャーで、**ツール** をクリックし、 **DNS**します。 DNS マネージャー Microsoft 管理コンソール (MMC) を開きます。  
  
2.  コンソール ツリーで、ダブルクリック**前方参照ゾーン**をクリックして、エイリアス リソース レコードを追加する前方参照ゾーンを右クリックして**新しいエイリアス\(CNAME\)** . **新しいリソース レコード** ダイアログ ボックスが表示されます。  
  
3.  **エイリアス名**、エイリアス名を入力**pki**します。  
  
4.  値を入力する**エイリアス名**、**完全修飾ドメイン名\(FQDN\)**   ダイアログ ボックスの自動塗りつぶし。 たとえば、エイリアス名が"pki"とドメインの場合は、corp.contoso.com の場合、値**pki.corp.contoso.com**を自動的に入力されます。  
  
5.  **完全修飾ドメイン名\(FQDN\)ターゲット ホスト用**、Web サーバーの FQDN を入力します。 たとえば、WEB1 という名前の Web サーバーは、ドメインが corp.contoso.com の場合は、「 **WEB1.corp.contoso.com**します。  
  
6.  クリックして**OK**をゾーンに新しいレコードを追加します。  
  

