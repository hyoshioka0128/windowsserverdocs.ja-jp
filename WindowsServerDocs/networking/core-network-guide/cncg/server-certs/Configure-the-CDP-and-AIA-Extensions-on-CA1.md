---
title: CA1 で CDP および AIA 拡張機能を構成する
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: dougkim
ms.topic: article
ms.assetid: f77a3989-9f92-41ef-92a8-031651dd73a8
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.date: 07/26/2018
ms.openlocfilehash: 6434b05d45cf9b8309fac4f6cd5cb5d6d149a7c2
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318401"
---
# <a name="configure-the-cdp-and-aia-extensions-on-ca1"></a>CA1 で CDP および AIA 拡張機能を構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、CA1 で証明書失効リスト (CRL) 配布ポイント (CDP) と機関情報アクセス (AIA) の設定を構成できます。  
  
この手順を実行するには、Domain Admins のメンバーである必要があります。  
  
#### <a name="to-configure-the-cdp-and-aia-extensions-on-ca1"></a>CA1 で CDP および AIA 拡張機能を構成するには  
  
1.  サーバー マネージャーで、 **[ツール]** をクリックし、 **[証明機関]** をクリックします。  
  
2.  証明機関 コンソールツリーで、 **CA1** を右クリックし、**プロパティ** をクリックします。  
  
    > [!NOTE]  
    > コンピューターに CA1 という名前を指定しておらず、この例で使用しているドメイン名と異なる場合、CA の名前は異なります。 CA 名は、*ドメイン*-*CAComputerName*の形式になっています。  
  
3.  **[拡張]** タブをクリックします。 [**拡張機能**が**CRL 配布ポイント (CDP)** ] に設定されていることを確認し、 **[ユーザーが証明書失効リスト (Crl) を取得できる場所を指定]** してください で、次の操作を行います。  
  
    1.  `file://\\<ServerDNSName>\CertEnroll\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`エントリを選択し、 **[削除]** をクリックします。 **[削除の確認]** で、 **[はい]** をクリックします。  
  
    2.  `http://<ServerDNSName>/CertEnroll/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`エントリを選択し、 **[削除]** をクリックします。 **[削除の確認]** で、 **[はい]** をクリックします。  
  
    3.  パス `ldap:///CN=<CATruncatedName><CRLNameSuffix>,CN=<ServerShortName>`で始まるエントリを選択し、 **[削除]** をクリックします。 **[削除の確認]** で、 **[はい]** をクリックします。  
  
4.  **[ユーザーが証明書失効リスト (CRL) を取得できる場所を指定]** します で、 **[追加]** をクリックします。 **[場所の追加]** ダイアログボックスが表示されます。  
  
5.  **[場所の追加]** の **[場所]** に「`http://pki.corp.contoso.com/pki/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`」と入力し、[ **OK]** をクリックします。 これにより、[CA のプロパティ] ダイアログボックスが表示されます。  
  
6.  **[拡張]** タブで、次のチェックボックスをオンにします。  
  
    -   **Crl に含めます。クライアントはこれを使用して Delta CRL の場所を検索します**  
  
    -   **発行された証明書の CDP 拡張機能に含める**  
  
7.  **[ユーザーが証明書失効リスト (CRL) を取得できる場所を指定]** します で、 **[追加]** をクリックします。 **[場所の追加]** ダイアログボックスが表示されます。  
  
8.  **[場所の追加]** の **[場所]** に「`file://\\pki.corp.contoso.com\pki\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`」と入力し、[ **OK]** をクリックします。 これにより、[CA のプロパティ] ダイアログボックスが表示されます。  
  
9. **[拡張]** タブで、次のチェックボックスをオンにします。  
  
    -   **Crl をこの場所に公開する**  
  
    -   **Delta Crl をこの場所に公開する**  
  
10. **[拡張機能の選択] を [** **機関情報アクセス (AIA)** ] に変更します。 [**ユーザーが証明書失効リスト (CRL) を取得できる場所を指定**してください] で、次の操作を行います。  
  
    1.  パス `ldap:///CN=<CATruncatedName>,CN=AIA,CN=Public Key Services`で始まるエントリを選択し、 **[削除]** をクリックします。 **[削除の確認]** で、 **[はい]** をクリックします。  
  
    2.  `http://<ServerDNSName>/CertEnroll/<ServerDNSName>_<CaName><CertificateName>.crt`エントリを選択し、 **[削除]** をクリックします。 **[削除の確認]** で、 **[はい]** をクリックします。  
  
    3.  `file://\\<ServerDNSName>\CertEnroll\<ServerDNSName><CaName><CertificateName>.crt`エントリを選択し、 **[削除]** をクリックします。 **[削除の確認]** で、 **[はい]** をクリックします。  
  
11. **[ユーザーがこの CA の証明書を取得できる場所を指定]** します で、 **[追加]** をクリックします。 **[場所の追加]** ダイアログボックスが表示されます。  
  
12. **[場所の追加]** の **[場所]** に「`http://pki.corp.contoso.com/pki/<ServerDNSName>_<CaName><CertificateName>.crt`」と入力し、[ **OK]** をクリックします。 これにより、[CA のプロパティ] ダイアログボックスが表示されます。  
  
13. **[拡張]** タブで、発行された **[証明書の AIA に含める]** を選択します。  
  
14. Active Directory 証明書サービスの再起動を求めるメッセージが表示されたら、 **[いいえ]** をクリックします。 サービスは、後で再起動します。  
  

