---
title: DNS に WEB1 のエイリアス (CNAME) レコードを作成する
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: bfae23f0-ae12-486b-94fe-50a137e141a5
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 77b8e464d2d8fab8803477e59826c3e715c0a6d2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406293"
---
# <a name="create-an-alias-cname-record-in-dns-for-web1"></a>WEB1 の DNS で \(CNAME @ no__t レコードを作成します。

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

この手順を使用して、Web サーバーのエイリアスの正規名 \(CNAME @ no__t-1 のリソースレコードを、ドメインコントローラー上の DNS 内のゾーンに追加できます。 CNAME レコードを使用すると、複数の名前を使用して1つのホストを指定することで、ファイル転送プロトコル @no__t 0FTP @ no__t サーバーと同じコンピューター上の Web サーバーの両方をホストするなどの操作を簡単に行うことができます。   
  
このため、Web サーバーを使用して、証明機関 \(CA @ no__t と、FTP や Web サーバーなどの追加サービスを実行するための証明書失効リスト \(CRL @ no__t-1 を自由にホストできます。  
  
この手順を実行するときに、**エイリアス名**とその他の変数を、配置に適した値に置き換えます。  
  
この手順を実行するには、 **Domain Admins**のメンバーである必要があります。  
  
## <a name="to-add-an-alias-cname-resource-record-to-a-zone"></a>エイリアス \(CNAME @ no__t リソースレコードをゾーンに追加するには  
  
>[!NOTE]  
>Windows PowerShell を使用してこの手順を実行するには、「 [DnsServerResourceRecordCName](https://technet.microsoft.com/library/jj649894(v=wps.630).aspx)」を参照してください。  
  
1.  DC1 の サーバーマネージャーで、 **[ツール]** をクリックし、 **[DNS]** をクリックします。 DNS マネージャー Microsoft 管理コンソール (MMC) が開きます。  
  
2.  コンソールツリーで、 **[前方参照ゾーン]** をダブルクリックし、エイリアスリソースレコードを追加する前方参照ゾーンを右クリックして、[**新しいエイリアス \(cname @ no__t**] をクリックします。 **[新しいリソースレコード]** ダイアログボックスが表示されます。  
  
3.  **[エイリアス名]** に、エイリアス名として「 **pki**」と入力します。  
  
4.  **[エイリアス名]** の値を入力すると、ダイアログボックスに**完全修飾ドメイン名 \(fqdn @ no__t が**自動入力されます。 たとえば、エイリアス名が "pki" で、ドメインが corp.contoso.com の場合、値**pki.corp.contoso.com**は自動的に入力されます。  
  
5.  **完全修飾ドメイン名 \( fqdn @ no__t-2 ターゲットホスト** に Web サーバーの fqdn を入力します。 たとえば、Web サーバーの名前が WEB1 で、ドメインが corp.contoso.com の場合は、「 **WEB1.corp.contoso.com**」と入力します。  
  
6.  **[OK]** をクリックして、新しいレコードをゾーンに追加します。  
  

