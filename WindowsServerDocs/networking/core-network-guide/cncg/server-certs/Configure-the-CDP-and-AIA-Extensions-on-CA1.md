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
ms.openlocfilehash: 74d77347e0ca1dffbca4e2cf6f17b9faa25d55bf
ms.sourcegitcommit: 23a6e83b688119c9357262b6815c9402c2965472
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69560498"
---
# <a name="configure-the-cdp-and-aia-extensions-on-ca1"></a>CA1 で CDP および AIA 拡張機能を構成する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、CA1 で証明書失効リスト (CRL) 配布ポイント (CDP) と機関情報アクセス (AIA) の設定を構成できます。  
  
この手順を実行するには、Domain Admins のメンバーである必要があります。  
  
#### <a name="to-configure-the-cdp-and-aia-extensions-on-ca1"></a>CA1 で CDP および AIA 拡張機能を構成するには  
  
1.  サーバー マネージャーで、 **[ツール]** をクリックし、 **[証明機関]** をクリックします。  
  
2.  [証明機関] コンソールツリーで、[ **CA1**] を右クリックし、[**プロパティ**] をクリックします。  
  
    > [!NOTE]  
    > コンピューターに CA1 という名前を指定しておらず、この例で使用しているドメイン名と異なる場合、CA の名前は異なります。 Ca 名は、*ドメイン*-*CAComputerName*の形式になっています。  
  
3.  **[拡張]** タブをクリックします。 **[拡張機能の選択] が [** **crl 配布ポイント (CDP)** ] に設定されていることを確認し、[**ユーザーが証明書失効リスト (crl) を取得できる場所を指定**してください] で、次の操作を行います。  
  
    1.  エントリ`file://\\<ServerDNSName>\CertEnroll\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`を選択し、[**削除**] をクリックします。 [**削除の確認**] で、[**はい**] をクリックします。  
  
    2.  エントリ`http://<ServerDNSName>/CertEnroll/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`を選択し、[**削除**] をクリックします。 [**削除の確認**] で、[**はい**] をクリックします。  
  
    3.  パス`ldap:///CN=<CATruncatedName><CRLNameSuffix>,CN=<ServerShortName>`で始まるエントリを選択し、[**削除**] をクリックします。 [**削除の確認**] で、[**はい**] をクリックします。  
  
4.  [**ユーザーが証明書失効リスト (CRL) を取得できる場所を指定**します] で、[**追加**] をクリックします。 [**場所の追加**] ダイアログボックスが表示されます。  
  
5.  [**場所の追加**]の [場所`http://pki.corp.contoso.com/pki/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`] に「」と入力し、[ **OK]** をクリックします。 これにより、[CA のプロパティ] ダイアログボックスが表示されます。  
  
6.  [**拡張**] タブで、次のチェックボックスをオンにします。  
  
    -   **Crl に含めます。クライアントはこれを使用して Delta CRL の場所を検索します。**  
  
    -   **発行された証明書の CDP 拡張機能に含める**  
  
7.  [**ユーザーが証明書失効リスト (CRL) を取得できる場所を指定**します] で、[**追加**] をクリックします。 [**場所の追加**] ダイアログボックスが表示されます。  
  
8.  [**場所の追加**]の [場所`file://\\pki.corp.contoso.com\pki\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`] に「」と入力し、[ **OK]** をクリックします。 これにより、[CA のプロパティ] ダイアログボックスが表示されます。  
  
9. [**拡張**] タブで、次のチェックボックスをオンにします。  
  
    -   **Crl をこの場所に公開する**  
  
    -   **Delta Crl をこの場所に公開する**  
  
10. **[拡張機能の選択] を [** **機関情報アクセス (AIA)** ] に変更します。 [**ユーザーが証明書失効リスト (CRL) を取得できる場所を指定**してください] で、次の操作を行います。  
  
    1.  パス`ldap:///CN=<CATruncatedName>,CN=AIA,CN=Public Key Services`で始まるエントリを選択し、[**削除**] をクリックします。 [**削除の確認**] で、[**はい**] をクリックします。  
  
    2.  エントリ`http://<ServerDNSName>/CertEnroll/<ServerDNSName>_<CaName><CertificateName>.crt`を選択し、[**削除**] をクリックします。 [**削除の確認**] で、[**はい**] をクリックします。  
  
    3.  エントリ`file://\\<ServerDNSName>\CertEnroll\<ServerDNSName><CaName><CertificateName>.crt`を選択し、[**削除**] をクリックします。 [**削除の確認**] で、[**はい**] をクリックします。  
  
11. [**ユーザーがこの CA の証明書を取得できる場所を指定**します] で、[**追加**] をクリックします。 [**場所の追加**] ダイアログボックスが表示されます。  
  
12. [**場所の追加**]の [場所`http://pki.corp.contoso.com/pki/<ServerDNSName>_<CaName><CertificateName>.crt`] に「」と入力し、[ **OK]** をクリックします。 これにより、[CA のプロパティ] ダイアログボックスが表示されます。  
  
13. [**拡張**] タブで、[発行された**証明書の AIA に含める**] を選択します。  
  
14. Active Directory 証明書サービスの再起動を求めるメッセージが表示されたら、[**いいえ**] をクリックします。 サービスは、後で再起動します。  
  

