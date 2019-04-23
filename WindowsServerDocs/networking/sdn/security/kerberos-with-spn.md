---
title: Kerberos とサービス プリンシパル名 (SPN)
description: ネットワーク コント ローラーには、管理クライアントとの通信用の複数の認証方法がサポートしています。 Kerberos ベースの認証、X509 を使用する証明書ベースの認証。 また、テスト デプロイでの認証を使用オプションがありません。
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 2459cfa8dfec3de4aa23da7aba192d6eeed7f8ec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828973"
---
# <a name="kerberos-with-service-principal-name-spn"></a>Kerberos とサービス プリンシパル名 (SPN)

>適用対象:Windows Server 2019

ネットワーク コント ローラーには、管理クライアントとの通信用の複数の認証方法がサポートしています。 Kerberos ベースの認証、X509 を使用する証明書ベースの認証。 また、テスト デプロイでの認証を使用オプションがありません。

System Center Virtual Machine Manager は、Kerberos ベースの認証を使用します。 Kerberos ベースの認証を使用している場合は、Active Directory でのネットワーク コント ローラーのサービス プリンシパル名 (SPN) を構成する必要があります。 SPN は、サービス インスタンスを関連付けるサービス ログイン アカウントに Kerberos 認証で使用されるネットワーク コント ローラー サービス インスタンスの一意の識別子です。 詳細については、次を参照してください。[サービス プリンシパル名](https://docs.microsoft.com/windows/desktop/ad/service-principal-names)します。

## <a name="configure-service-principal-names-spn"></a>サービス プリンシパル名 (SPN) を構成します。

ネットワーク コント ローラーには、SPN が自動的に構成されます。 行う必要があるすべては、登録およびは SPN を変更するには、ネットワーク コント ローラー コンピューターのアクセス許可を提供します。

1.  ドメイン コント ローラー コンピューターでは、開始**Active Directory ユーザーとコンピューター**します。

2.  選択**ビュー\>高度な**します。

3.  **コンピューター**をネットワーク コント ローラー コンピューター アカウントのいずれかを検索し、右クリックし、**プロパティ**します。

4.  選択、**セキュリティ** タブでをクリックし、**詳細**します。

5.  一覧で、ネットワーク コント ローラーのすべてのコンピューター アカウントまたはセキュリティ グループがネットワーク コント ローラーのすべてのコンピューター アカウントが表示されていないこと場合、 をクリックして**追加**に追加します。

6.  各ネットワーク コント ローラー コンピューター アカウントまたはネットワーク コント ローラーのコンピューター アカウントを含む 1 つのセキュリティ グループ。

    a.   アカウントまたはグループを選択し、クリックして**編集**します。

    b.   [アクセス許可の選択] で**servicePrincipalName を書き込む検証**です。

    d.  スクロール ダウンし、**プロパティ**を選択します。

       -  **サービス プリンシパル名を読み取る**

       -  **ServicePrincipalName を書き込む**

    e.  **[OK]** を 2 回クリックします。

7.  各ネットワーク コント ローラー マシンには、手順 3. ~ 6. を繰り返します。

8.  **[Active Directory ユーザーとコンピューター]** を閉じます。

## <a name="failure-to-provide-permissions-for-spn-registrationmodification"></a>SPN の登録/変更するためのアクセス許可を付与する失敗

**新規**REST クライアントの認証に Kerberos を選択し、ネットワーク コント ローラー ノードを登録または SPN を変更するためのアクセス許可を付与しない場合は、Windows Server 2019 展開、ネットワーク コント ローラーに対する REST 操作が失敗しました。SDN の管理を妨げています。

Windows Server 2016 と Windows Server の 2019 へのアップグレードは、REST クライアントの認証に Kerberos を選択の REST 操作はブロックされない、既存の運用環境のデプロイの透過性を確保します。 

SPN が登録されていない場合は、REST クライアントの認証は、これは安全性の低い NTLM を使用します。 取得することも重要なイベントの管理チャネルに**NetworkController Framework** SPN を登録する、ネットワーク コント ローラーのノードにアクセス許可を提供するよう求めるイベント チャネル。 アクセス許可を指定するとネットワーク コント ローラーが自動的には、SPN を登録し、Kerberos を使用して、すべてのクライアント操作します。


>[!TIP]
>通常、REST ベースの操作の DNS 名または IP アドレスを使用するネットワーク コント ローラーを構成できます。 ただし、Kerberos を構成するときに、ネットワーク コント ローラーに対する REST クエリの場合、IP アドレスを使用できません。 たとえば、使用することができます\< https://networkcontroller.consotso.com\>、使用することはできませんが、 \<https://192.34.21.3\>します。 IP アドレスを使用する場合、サービス プリンシパル名は機能できません。
>
>IP アドレスと共に Windows Server 2016 での Kerberos 認証の REST 操作を使用していた場合、実際の通信が NTLM 認証経由ででした。 このような展開では、Windows Server 2019 にアップグレードした後は、引き続き NTLM ベースの認証を使用します。 Kerberos ベースの認証に移動するには、REST 操作のネットワーク コント ローラーの DNS 名を使用して、、ネットワーク コント ローラー ノードの SPN を登録するためのアクセス許可を指定する必要があります。

---