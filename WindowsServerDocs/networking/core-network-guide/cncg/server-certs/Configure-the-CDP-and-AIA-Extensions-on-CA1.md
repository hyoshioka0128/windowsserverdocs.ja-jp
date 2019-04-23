---
title: CA1 で CDP および AIA 拡張機能を構成する
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: dougkim
ms.topic: article
ms.assetid: f77a3989-9f92-41ef-92a8-031651dd73a8
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.date: 07/26/2018
ms.openlocfilehash: 2bdd03636d1cbbcf5b0355358cbedeb63f97af1b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834223"
---
# <a name="configure-the-cdp-and-aia-extensions-on-ca1"></a>CA1 で CDP および AIA 拡張機能を構成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

CA1 で証明書失効リスト (CRL) 配布ポイント (CDP) および機関情報アクセス (AIA) の設定を構成するのには、この手順を使用することができます。  
  
この手順を実行するには、Domain Admins のメンバーがあります。  
  
#### <a name="to-configure-the-cdp-and-aia-extensions-on-ca1"></a>CA1 で CDP および AIA 拡張機能を構成するには  
  
1.  サーバー マネージャーで、**[ツール]** をクリックし、**[証明機関]** をクリックします。  
  
2.  証明機関のコンソール ツリーで、右クリック**corp-CA CA1**、 をクリックし、**プロパティ**します。  
  
    > [!NOTE]  
    > 名前を指定しなかった CA1 コンピューターとドメイン名がこの例では異なる場合は、CA の名前は異なります。 CA の名前は、形式*ドメイン*-*CAComputerName*CA。  
  
3.  **[拡張]** タブをクリックします。いることを確認**拡張機能の選択**に設定されている**CRL 配布ポイント (CDP)**、し、**ユーザーが証明書失効リスト (CRL) を入手できる場所を指定**、次の操作を行います。  
  
    1.  エントリを選択します`file://\\<ServerDNSName>\CertEnroll\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`、 をクリックし、**削除**します。 **削除の確認**、 をクリックして**はい**します。  
  
    2.  エントリを選択します`https://<ServerDNSName>/CertEnroll/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`、 をクリックし、**削除**します。 **削除の確認**、 をクリックして**はい**します。  
  
    3.  パスで始まるエントリを選択`ldap:///CN=<CATruncatedName><CRLNameSuffix>,CN=<ServerShortName>`、 をクリックし、**削除**します。 **削除の確認**、 をクリックして**はい**します。  
  
4.  **ユーザーが証明書失効リスト (CRL) を入手できる場所を指定**、 をクリックして**追加**します。 **場所の追加** ダイアログ ボックスが表示されます。  
  
5.  **場所の追加**で、**場所**、型`https://pki.corp.contoso.com/pki/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`、順にクリックします**OK**します。 CA のプロパティ ダイアログ ボックスに戻ります。  
  
6.  **拡張** タブで、次のチェック ボックスをオンします。  
  
    -   **Crl に含まれます。クライアントでは、これを使って Delta CRL の場所を検索するには**  
  
    -   **発行された証明書の CDP 拡張機能に含める**  
  
7.  **ユーザーが証明書失効リスト (CRL) を入手できる場所を指定**、 をクリックして**追加**します。 **場所の追加** ダイアログ ボックスが表示されます。  
  
8.  **場所の追加**で、**場所**、型`file://\\pki.corp.contoso.com\pki\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`、順にクリックします**OK**します。 CA のプロパティ ダイアログ ボックスに戻ります。  
  
9. **拡張** タブで、次のチェック ボックスをオンします。  
  
    -   **この場所に Crl を公開します。**  
  
    -   **Delta Crl をこの場所に公開します。**  
  
10. 変更**拡張機能の選択**に**機関情報アクセス (AIA)**、し、**ユーザーが証明書失効リスト (CRL) を入手できる場所を指定**、操作を行います次:  
  
    1.  パスで始まるエントリを選択`ldap:///CN=<CATruncatedName>,CN=AIA,CN=Public Key Services`、 をクリックし、**削除**します。 **削除の確認**、 をクリックして**はい**します。  
  
    2.  エントリを選択します`https://<ServerDNSName>/CertEnroll/<ServerDNSName>_<CaName><CertificateName>.crt`、 をクリックし、**削除**します。 **削除の確認**、 をクリックして**はい**します。  
  
    3.  エントリを選択します`file://\\<ServerDNSName>\CertEnroll\<ServerDNSName><CaName><CertificateName>.crt`、 をクリックし、**削除**します。 **削除の確認**、 をクリックして**はい**します。  
  
11. **元となるユーザーは、この CA の証明書を入手できる場所を指定**、 をクリックして**追加**します。 **場所の追加** ダイアログ ボックスが表示されます。  
  
12. **場所の追加**で、**場所**、型`https://pki.corp.contoso.com/pki/<ServerDNSName>_<CaName><CertificateName>.crt`、順にクリックします**OK**します。 CA のプロパティ ダイアログ ボックスに戻ります。  
  
13. **拡張**] タブで [**発行された証明書の AIA に含める**します。  
  
14. Active Directory 証明書サービスを再起動するメッセージが表示されたら、クリックして**いいえ**します。 サービスは、後で再起動されます。  
  

