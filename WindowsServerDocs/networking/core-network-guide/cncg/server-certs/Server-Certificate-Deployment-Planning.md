---
title: サーバー証明書の展開の計画
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: 7eb746e0-1046-4123-b532-77d5683ded44
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1ec5bc315381f85434753f9becc94409a74271b7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356110"
---
# <a name="server-certificate-deployment-planning"></a>サーバー証明書の展開の計画

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

サーバー証明書を展開する前に、次の項目を計画する必要があります。  
  
-   [基本的なサーバー構成の計画](#bkmk_basic)  
  
-   [ドメインアクセスを計画する](#bkmk_domain)  
  
-   [Web サーバー上の仮想ディレクトリの場所と名前を計画する](#bkmk_virtual)  
  
-   [Web サーバーの DNS エイリアス (CNAME) レコードを計画する](#bkmk_cname)  
  
-   [Capolicy.inf の構成を計画する](#bkmk_capolicy)  
  
-   [CA1 で CDP および AIA 拡張機能の構成を計画する](#bkmk_cdp)  
  
-   [CA と Web サーバー間のコピー操作を計画する](#bkmk_copy)  
  
-   [CA でのサーバー証明書テンプレートの構成を計画する](#bkmk_template)  
  
## <a name="bkmk_basic"></a>基本的なサーバー構成の計画  
証明機関と Web サーバーとして使用する予定のコンピューターに Windows Server 2016 をインストールした後、コンピューターの名前を変更を割り当てると、ローカル コンピューターの静的 IP アドレスを構成してください。  
  
詳細については、Windows Server 2016 を参照してください。 [コア ネットワーク ガイド](../../../core-network-guide/Core-Network-Guide.md)します。  
  
## <a name="bkmk_domain"></a>ドメインアクセスを計画する  
ドメインにログオンするには、コンピューターがドメイン メンバー コンピューターをする必要があり、ログオン試行の前に AD DS でユーザー アカウントを作成する必要があります。 さらに、このガイドのほとんどの手順では、ユーザー アカウントが Active Directory ユーザーとコンピューターの Enterprise Admins または Domain Admins グループのメンバーを適切なグループ メンバーシップを持つアカウントを使用して CA にログオンする必要がありますのでが必要です。  
  
詳細については、Windows Server 2016 を参照してください。 [コア ネットワーク ガイド](../../../core-network-guide/Core-Network-Guide.md)します。  
  
## <a name="bkmk_virtual"></a>Web サーバー上の仮想ディレクトリの場所と名前を計画する  
CRL と他のコンピューターに CA 証明書にアクセスを提供するには、Web サーバーで、仮想ディレクトリでこれらのアイテムを格納する必要があります。 このガイドでは、仮想ディレクトリを Web サーバー WEB1 にあります。 このフォルダーは「c:」ドライブに、"pki"の名前は 展開に適切なフォルダーの場所から Web サーバーを仮想ディレクトリを検索できます。  
  
## <a name="bkmk_cname"></a>Web サーバーの DNS エイリアス (CNAME) レコードを計画する  
エイリアス (CNAME) リソース レコードは正規名リソース レコードと呼ばれることもあります。 これらのレコードと容易をファイル転送プロトコル (FTP) サーバーと同じコンピューター上の Web サーバーの両方にこのような管理操作を行うには、1 つのホストを指す複数の名前を使用できます。 たとえば、よく知られたサーバー名 (ftp、www など) はこれらのサービスをホストしている、ドメイン ネーム システム (DNS) ホスト名に WEB1 など、サーバー コンピューターにマップするエイリアス (CNAME) リソース レコードを使用して登録されます。  
  
このガイドでは、証明機関 (CA) の証明書失効リスト (CRL) をホストする Web サーバーを構成するための手順を提供します。 FTP または Web サイトをホストするなどの他の目的の Web サーバーを使用することも、ためには、Web サーバーの DNS でエイリアス リソース レコードを作成することをお勧めします。 このガイドでは、CNAME レコードには、"pki"はという名前が、展開に適切な名前を選択することができます。  
  
## <a name="bkmk_capolicy"></a>Capolicy.inf の構成を計画する  
AD CS をインストールする前に、情報が正しいことを含む CA の CAPolicy.inf を構成する必要があります。 CAPolicy.inf ファイルには、次の情報が含まれています。  
  
```  
[Version]  
Signature="$Windows NT$"  
[PolicyStatementExtension]  
Policies=InternalPolicy  
[InternalPolicy]  
OID=1.2.3.4.1455.67.89.5  
Notice="Legal Policy Statement"  
URL=https://pki.corp.contoso.com/pki/cps.txt  
[Certsrv_Server]  
RenewalKeyLength=2048  
RenewalValidityPeriod=Years  
RenewalValidityPeriodUnits=5  
CRLPeriod=weeks  
CRLPeriodUnits=1  
LoadDefaultTemplates=0  
AlternateSignatureAlgorithm=1  
```  
このファイルの次の項目を計画する必要があります。  
  
-   **URL**します。 この例の Capolicy.inf ファイルには、 **https://pki.corp.contoso.com/pki/cps.txt** の URL 値が含まれています。 これは、このガイド内の Web サーバーが WEB1 の名前は、pki の DNS の CNAME リソース レコードがあるためです。 Web サーバーは、corp.contoso.com ドメインに参加します。 さらに、仮想ディレクトリにある証明書失効リストが格納されている"pki"という名前の Web サーバー。 ドメイン内、Web サーバー上の仮想ディレクトリには、CAPolicy.inf ファイルのポイントで URL の指定した値を確認します。  
  
-   **RenewalKeyLength**します。 Windows Server 2012 で AD CS の既定の更新のキーの長さは 2048 です。 選択したキーの長さを使用するアプリケーションとの互換性を提供しながらできるだけ長くする必要があります。  
  
-   **RenewalValidityPeriodUnits**します。 CAPolicy.inf ファイルの例では、5 年の RenewalValidityPeriodUnits 値があります。 これは、CA の想定される存続期間が約 10 年であるためです。 RenewalValidityPeriodUnits の値には、CA または登録できるようにする対象となる年間の最大数の全体的な有効期間を反映する必要があります。  
  
-   **CRLPeriodUnits**します。 CAPolicy.inf ファイルの例では、1 の CRLPeriodUnits 値があります。 これは、このガイドで証明書失効リストの例の更新間隔が 1 週間であるためです。 この設定で指定した間隔の値には、CRL を格納する Web サーバーの仮想ディレクトリを CA の CRL を発行し、認証プロセスであるコンピュータへのアクセス権を提供します。  
  
-   **AlternateSignatureAlgorithm**します。 この CAPolicy.inf では、別の署名形式を実装することで、強化されたセキュリティ メカニズムを実装します。 この CA から証明書を必要とする Windows XP クライアントがある場合は、この設定を実装しないでください。  
  
すべての下位 Ca を後で、公開キー インフラストラクチャに追加する予定がないし、すべての下位 Ca を追加できないようにする場合は、値 0 は、CAPolicy.inf ファイルに PathLength キーを追加できます。 このキーを追加するには、コピーして、次のコードをファイルに貼り付けます。  
  
```  
[BasicConstraintsExtension]  
PathLength=0  
Critical=Yes  
```  
  
> [!IMPORTANT]  
> そのための特定の理由がない限り、CAPolicy.inf ファイルにその他の設定を変更することは推奨されません。  
  
## <a name="bkmk_cdp"></a>CA1 で CDP および AIA 拡張機能の構成を計画する  
CA1 で証明書失効リスト (CRL) 配布ポイント (CDP) および機関情報アクセス (AIA) の設定を構成する場合は、Web サーバーとドメイン名の名前が必要です。 証明書失効リスト (CRL) および証明機関の証明書が格納されている Web サーバーで作成した仮想ディレクトリの名前も必要です。  
  
ここでの展開時に入力する必要があります CDP の場所には、形式があります。  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl.`  
      
たとえば、WEB1 という名前の Web サーバーは、DNS、Web サーバーの CNAME レコード エイリアスは"pki"場合は、ドメインが corp.contoso.com の場合、および仮想ディレクトリの名前は pki、CDP の場所は。  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`  
      
入力する必要があります AIA の場所には、形式があります。  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<ServerDNSName>\_<CaName><CertificateName>.crt.`  
      
たとえば、WEB1 という名前の Web サーバーは、DNS、Web サーバーの CNAME レコード エイリアスは"pki"場合は、ドメインが corp.contoso.com の場合、および仮想ディレクトリの名前は pki、AIA の場所は。  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`  
      
## <a name="bkmk_copy"></a>CA と Web サーバー間のコピー操作を計画する  
CRL と CA 証明書を発行 CA から Web サーバーの仮想ディレクトリを CA の CDP および AIA の場所を構成した後は、certutil-crl コマンドを実行できます。 [CA プロパティによって正しいパスを構成するよう **拡張** ] タブのこのガイドの手順に従って、このコマンドを実行する前にします。 さらに、エンタープライズ CA 証明書を Web サーバーにコピーする必要があります Web サーバーに仮想ディレクトリを作成して共有フォルダーとしてフォルダーを構成します。  
  
## <a name="bkmk_template"></a>CA でのサーバー証明書テンプレートの構成を計画する  
自動登録サーバーの証明書を展開するには、という名前の証明書テンプレートをコピーする必要があります **RAS および IAS サーバー**します。 既定では、このコピーの名前は **コピーの RAS および IAS サーバー**します。 このテンプレートのコピーの名前を変更する場合は、この展開の手順で使用する名前を計画します。  
  
> [!NOTE]  
> 最後の 3 つの展開ガイドのセクションでこのサーバーの証明書自動登録を構成、サーバーでは、グループ ポリシーを更新して、サーバーで CA から有効なサーバー証明書が受信したことを確認するには、追加の計画手順は不要です。  
  


