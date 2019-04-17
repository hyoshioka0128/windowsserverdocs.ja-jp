---
title: CA1 で CDP および AIA 拡張機能を構成します。
description: このトピックの「802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部である
manager: brianlic
ms.topic: article
ms.assetid: f77a3989-9f92-41ef-92a8-031651dd73a8
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 80f6d68816a58b2ac30010e0917ce0f816a30234
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-cdp-and-aia-extensions-on-ca1"></a>CA1 で CDP および AIA 拡張機能を構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

CA1 で証明書失効リスト (CRL) 配布ポイント (CDP) および機関情報アクセス (AIA) の設定を構成するのには、この手順を使用することができます。  
  
この手順を実行するには、Domain Admins のメンバーがあります。  
  
#### <a name="to-configure-the-cdp-and-aia-extensions-on-ca1"></a>CA1 で CDP および AIA 拡張機能を構成するには  
  
1.  サーバー マネージャーで、クリックして**ツール**] をクリックし、**証明機関**します。  
  
2.  証明機関のコンソール ツリーで、右クリック**corp-CA CA1**、] をクリックし、**プロパティ**します。  
  
    > [!NOTE]  
    > CA1 コンピューターの名前をされませんでしたし、ドメイン名がこの例では異なる場合は、CA の名前は異なります。 CA 名の形式が*ドメイン*-*CAComputerName*CA です。  
  
3.  をクリックして、**拡張機能:** ] タブであることを確認**拡張子を選択**に設定されている**CRL 配布ポイント (CDP)**、し、[、ユーザーが証明書失効リスト (CRL)、次の操作します。  
  
    1.  エントリを選択`file:\/\/\\\\<ServerDNSName>\/CertEnroll\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`、] をクリックし、**削除**します。 **、削除の確認**、] をクリックして**はい**します。  
  
    2.  エントリを選択`http:\/\/<ServerDNSName>\/CertEnroll\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`、] をクリックし、**削除**します。 **、削除の確認**、] をクリックして**はい**します。  
  
    3.  パスで始まるエントリを選択して`ldap:\/\/CN\=<CATruncatedName><CRLNameSuffix>,CN\=<ServerShortName>`、] をクリックし、**削除**します。 **、削除の確認**、] をクリックして**はい**します。  
  
4.  **証明書失効リスト (CRL) を取得する元の場所を指定**、] をクリックして**追加**します。 **場所の追加**] ダイアログ ボックスが開きます。  
  
5.  **場所の追加**で、**場所**、型`http:\/\/pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`、] をクリックし、 **OK**します。 CA のプロパティ] ダイアログ ボックスに戻ります。  
  
6.  **拡張機能:** ] タブで、次のチェック ボックスをオンにします。  
  
    -   **[Crl が含まれます。 クライアントでは、これを使って Delta CRL の場所を検索するには**  
  
    -   **発行された証明書の CDP 拡張機能に含める**  
  
7.  **証明書失効リスト (CRL) を取得する元の場所を指定**、] をクリックして**追加**します。 **場所の追加**] ダイアログ ボックスが開きます。  
  
8.  **場所の追加**で、**場所**、型`file:\/\/\\\\pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`、] をクリックし、 **OK**します。 CA のプロパティ] ダイアログ ボックスに戻ります。  
  
9. **拡張機能:** ] タブで、次のチェック ボックスをオンにします。  
  
    -   **この場所に Crl を公開します。**  
  
    -   **この場所への Delta Crl を公開します。**  
  
10. 変更**拡張子を選択**に**機関情報アクセス (AIA)**、し、[、**証明書失効リスト (CRL) を取得する元の場所を指定**、次の操作します。  
  
    1.  パスで始まるエントリを選択して`ldap:\/\/CN\=<CATruncatedName>,CN\=AIA,CN\=Public Key Services`、] をクリックし、**削除**します。 **、削除の確認**、] をクリックして**はい**します。  
  
    2.  エントリを選択`http:\/\/<ServerDNSName>\/CertEnroll\/<ServerDNSName>\_<CaName><CertificateName>.crt`、] をクリックし、**削除**します。 **、削除の確認**、] をクリックして**はい**します。  
  
    3.  エントリを選択`file:\/\/\\\\<ServerDNSName>\/CertEnroll\/<ServerDNSName>\_<CaName><CertificateName>.crt`、] をクリックし、**削除**します。 **、削除の確認**、] をクリックして**はい**します。  
  
11. **証明書失効リスト (CRL) を取得する元の場所を指定**、] をクリックして**追加**します。 **場所の追加**] ダイアログ ボックスが開きます。  
  
12. **場所の追加**で、**場所**、型`http:\/\/pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`、] をクリックし、 **OK**します。 CA のプロパティ] ダイアログ ボックスに戻ります。  
  
13. **拡張機能:** ] タブで [**発行された証明書の AIA に含める**します。  
  
14. **場所の追加**で、**場所**、型`file:\/\/\\\\pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`、] をクリックし、 **OK**します。 CA のプロパティ] ダイアログ ボックスに戻ります。  
  
    > [!IMPORTANT]  
    > いることを確認**発行された証明書の AIA 拡張機能に含める**が選択されていません。  
  
15. Active Directory 証明書サービスを再起動するメッセージが表示されたら、] をクリックして**いいえ**します。 サービスは後で再起動されます。  
  


