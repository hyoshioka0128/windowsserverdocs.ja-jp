---
title: Kerberos とサービス プリンシパル名 (SPN)
description: ネットワークコントローラーは、管理クライアントと通信するための複数の認証方法をサポートしています。 Kerberos ベースの認証 (X509 証明書ベースの認証) を使用できます。 テスト配置に認証を使用しないオプションもあります。
manager: grcusanz
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/23/2018
ms.openlocfilehash: ce85e93f229c62d836a00e7665e2a76bd08b44dd
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996545"
---
# <a name="kerberos-with-service-principal-name-spn"></a>Kerberos とサービス プリンシパル名 (SPN)

>適用対象:Windows Server 2019

ネットワークコントローラーは、管理クライアントと通信するための複数の認証方法をサポートしています。 Kerberos ベースの認証 (X509 証明書ベースの認証) を使用できます。 テスト配置に認証を使用しないオプションもあります。

System Center Virtual Machine Manager は、Kerberos ベースの認証を使用します。 Kerberos ベースの認証を使用している場合は、Active Directory でネットワークコントローラーのサービスプリンシパル名 (SPN) を構成する必要があります。 SPN は、ネットワークコントローラーサービスインスタンスの一意の識別子です。この識別子は、サービスインスタンスをサービスログインアカウントに関連付けるために Kerberos 認証によって使用されます。 詳細については、「[サービスプリンシパル名](/windows/desktop/ad/service-principal-names)」を参照してください。

## <a name="configure-service-principal-names-spn"></a>サービスプリンシパル名 (SPN) の構成

SPN は、ネットワークコントローラーによって自動的に構成されます。 必要なのは、SPN を登録および変更するためのアクセス許可をネットワークコントローラーコンピューターに付与することだけです。

1.  ドメインコントローラーコンピューターで、 **Active Directory ユーザーとコンピューター**] を起動します。

2.  [ ** \> 詳細表示**] を選択します。

3.  [**コンピューター**] で、いずれかのネットワークコントローラーのコンピューターアカウントを見つけて右クリックし、[**プロパティ**] を選択します。

4.  **[セキュリティ]** タブを選択してから **[詳細設定]** をクリックします。

5.  一覧で、すべてのネットワークコントローラーのコンピューターアカウントまたはすべてのネットワークコントローラーのコンピューターアカウントを持つセキュリティグループが一覧に表示されていない場合は、[**追加**] をクリックして追加します。

6.  各ネットワークコントローラーのコンピューターアカウント、またはネットワークコントローラーのコンピューターアカウントを含む1つのセキュリティグループについて、次のようにします。

    a.  アカウントまたはグループを選択し、[**編集**] をクリックします。

    b.  [アクセス許可] の [検証] [ **servicePrincipalName の検証**] を選択します。

    d.  下にスクロールし、[**プロパティ**] を選択します。

       -  **ServicePrincipalName の読み取り**

       -  **ServicePrincipalName の書き込み**

    e.  [**OK**] を 2 回クリックします。

7.  各ネットワークコントローラーマシンについて、手順 3-6 を繰り返します。

8.  **[Active Directory ユーザーとコンピューター]** を閉じます。

## <a name="failure-to-provide-permissions-for-spn-registrationmodification"></a>SPN の登録または変更に対するアクセス許可を提供できませんでした

**新しい**Windows Server 2019 の展開では、[rest クライアント認証に Kerberos を使用する] を選択し、SPN を登録または変更するためのアクセス許可をネットワークコントローラーノードに付与しないと、ネットワークコントローラーに対する rest 操作が失敗し、SDN を管理できなくなります。

Windows Server 2016 から Windows Server 2019 にアップグレードする場合、[REST クライアント認証に Kerberos を使用する] を選択した場合、REST 操作はブロックされず、既存の運用環境のデプロイの透明性が確保されます。

SPN が登録されていない場合、REST クライアント認証は NTLM を使用しますが、安全性は低くなります。 また、 **NetworkController**イベントチャネルの管理チャネルでも、SPN を登録するためのアクセス許可をネットワークコントローラーノードに提供するよう求めるメッセージが表示されます。 アクセス許可を指定すると、ネットワークコントローラーによって SPN が自動的に登録され、すべてのクライアント操作で Kerberos が使用されます。


>[!TIP]
>通常、REST ベースの操作には、IP アドレスまたは DNS 名を使用するようにネットワークコントローラーを構成できます。 ただし、Kerberos を構成するときに、ネットワークコントローラーに対する REST クエリに IP アドレスを使用することはできません。 たとえば、を使用することはでき \<https://networkcontroller.consotso.com\> ますが、を使用することはできません \<https://192.34.21.3\> 。 IP アドレスが使用されている場合、サービスプリンシパル名は機能しません。
>
>Windows Server 2016 で Kerberos 認証と共に REST 操作に IP アドレスを使用していた場合、実際の通信は NTLM 認証を介して行われていました。 このような展開では、Windows Server 2019 にアップグレードすると、引き続き NTLM ベースの認証を使用します。 Kerberos ベースの認証に移行するには、REST 操作にネットワークコントローラーの DNS 名を使用し、SPN を登録するためのアクセス許可をネットワークコントローラーノードに付与する必要があります。

---