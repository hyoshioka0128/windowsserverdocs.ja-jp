---
ms.assetid: d92731f1-e4d8-4223-9b07-ca1f40bb0e1f
title: "不整合のある Namespace"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ac231dbfbaaeafa39199e29a1744d84d5cec23e8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="disjoint-namespace"></a>不整合のある Namespace

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

不整合な名前空間は、1 つまたは複数のドメイン メンバー コンピューターのプライマリ ドメイン ネーム サービス (DNS) サフィックス、Active Directory が、コンピューターがドメインのメンバーの DNS 名と一致しない場合に発生します。 たとえば、na.corp.fabrikam.com という Active Directory ドメインに corp.fabrikam.com のプライマリ DNS サフィックスを使用するメンバー コンピューターでは、不整合な名前空間を使っています。  
  
不整合な名前空間は、管理、保守、およびより隣接する名前空間のトラブルシューティングを行うには複雑です。 連続する名前空間では、プライマリ DNS サフィックスは、Active Directory ドメイン名と一致します。 不整合な名前空間の Active Directory 名前空間がドメイン メンバー コンピューターのすべてのプライマリ DNS サフィックスと同じであると仮定する記述されているネットワーク アプリケーションが正しく機能しません。  
  
## <a name="support-for-disjoint-namespaces"></a>不整合な名前空間のサポート  
ドメイン コントローラーを含む、ドメイン メンバー コンピューターは、不整合な名前空間で動作できます。 ドメイン メンバー コンピューターが、ホストに登録できます (A) リソース レコードと IP version 6 (IPv6) のホスト (AAAA) リソース レコードを DNS 名前空間の不整合します。 ドメイン メンバー コンピューターでは、この方法で、リソース レコードを登録するときに、Active Directory ドメイン名に一致する DNS ゾーンのグローバルおよびサイト固有のサービス (SRV) リソース レコードを登録するドメイン コントローラーを続行します。  
  
たとえば、という名前の na.corp.fabrikam.com corp.fabrikam.com のプライマリ DNS サフィックスを使用する Active Directory ドメインのドメイン コントローラーで corp.fabrikam.com DNS ゾーンのホスト (A) と IPv6 ホスト (AAAA) リソース レコードを登録します。 ドメイン コントローラーは引き続き _msdcs。na.corp.fabrikam.com と na.corp.fabrikam.com DNS ゾーンに、グローバルおよびサイト固有のサービス (SRV) リソース レコードを登録するサービスの場所が可能になります。  
  
> [!IMPORTANT]  
> Windows オペレーティング システムは、不整合な名前空間をサポートすることが、プライマリ DNS サフィックスが Active Directory ドメインのサフィックスと同じであると仮定する記述されているアプリケーションがこのような環境で機能しない可能性が。 このため、十分にテストし、すべてのアプリケーションにそれぞれのオペレーティング システム、不整合な名前空間を展開する前にします。  
  
不整合な名前空間作業する必要があります (およびはサポートされている)、次の状況で。  
  
-   複数の Active Directory ドメインを持つフォレストが単一 DNS の名前空間、DNS ゾーンとも呼ばれるを使用する場合  
  
    この例は、na.corp.fabrikam.com、sa.corp.fabrikam.com、asia.corp.fabrikam.com などの名前を持つ地域ドメインを使用し、1 つ DNS 名前空間、corp.fabrikam.com などを使用している企業です。  
  
-   単一の Active Directory ドメインを別の DNS 名前空間に分割する場合  
  
    この例は、会社の corp.contoso.com hr.corp.contoso.com、production.corp.contoso.com、it.corp.contoso.com などの DNS ゾーンを使用する Active Directory ドメインにです。  
  
不整合な名前空間が正しく動作しない (およびサポートされていません) 次の状況で。  
  
-   ドメインのメンバーで使用される分離されたサフィックスは、同じまたは別のフォレスト内の Active Directory ドメイン名と一致します。 これは、Kerberos 名前サフィックスのルーティングを中断します。  
  
-   同じ分離されたサフィックスは、別のフォレストで使用されます。 これには、フォレスト間で一意にこれらのサフィックスのルーティングができないようにします。  
  
-   ドメイン メンバーの証明機関 (CA) した場合、サーバーの変更が完全には、CA サーバーがメンバーにするドメインのドメイン コントローラーによって使用される同じプライマリ DNS サフィックスを不要になった使用できるようにドメイン名 (FQDN) を限定します。 この場合、CRL 配布ポイントでどのような DNS 名を使用することによって、発行された CA サーバー証明書を検証する問題がある可能性があります。 安定して不整合な名前空間で CA サーバーを配置する場合が正常に動作がサポートされています。  
  
## <a name="considerations-for-disjoint-namespaces"></a>不整合な名前空間に関する考慮事項  
次の考慮事項は、するかどうかは、不整合な名前空間を使用する必要がありますを決定に役立つ場合があります。  
  
### <a name="application-compatibility"></a>アプリケーションの互換性  
前述のように、不整合な名前空間のアプリケーションとコンピューターのプライマリ DNS サフィックスが属するドメイン名の名前と同じであると仮定する記述されているサービスの問題が発生することができます。 不整合な名前空間を展開する前に、アプリケーションの互換性の問題を確認する必要があります。 また、必ず、分析を実行するときに使用するすべてのアプリケーションの互換性を確認します。 これには、Microsoft およびその他のソフトウェア開発者からのアプリケーションが含まれます。  
  
### <a name="advantages-of-disjoint-namespaces"></a>不整合な名前空間の利点  
不整合な名前空間を使用して、次の利点があります。  
  
-   コンピューターのプライマリ DNS サフィックスは、さまざまな情報を示すことができます、ため Active Directory ドメイン名からとは別に、DNS 名前空間を管理できます。  
  
-   ビジネスの構造体または地理的な場所に基づいて、DNS 名前空間を分離することができます。 たとえば、ビジネス ユニットの名前または大陸、国/地域建物などの物理的な場所に基づいて、名前空間を分離することができます。  
  
### <a name="disadvantages-of-disjoint-namespaces"></a>不整合な名前空間の短所  
不整合な名前空間を使用して、次の欠点があります。  
  
-   作成し、各 Active Directory ドメイン メンバー コンピューターが不整合な名前空間を使用するフォレスト内の別の DNS ゾーンを管理する必要があります。 (つまり、その構成が必要です、追加しより複雑です。)  
  
-   変更およびドメイン メンバーに指定すると、プライマリ DNS サフィックスを使用できるようにする Active Directory 属性を管理する手動の手順を実行する必要があります。  
  
-   名前解決を最適化するには、変更および代替のプライマリ DNS サフィックスを持つメンバー コンピューターを構成するグループ ポリシーの保守の手動の手順を実行する必要があります。  
  
    > [!NOTE]  
    > 単一ラベル名を解決することによってこの欠点のペースには、Windows インターネット ネーム サービス (WINS) を使用できます。 WINS の詳細については、WINS のテクニカル リファレンスを参照してください ([https://go.microsoft.com/fwlink/?LinkId=102303](https://go.microsoft.com/fwlink/?LinkId=102303))。  
  
-   環境内には、複数のプライマリ DNS サフィックスが必要とする場合、フォレスト内のすべての Active Directory ドメインの DNS サフィックスの検索順序を適切に構成する必要があります。  
  
    DNS サフィックスの検索順序を設定するには、グループ ポリシー オブジェクトまたは動的ホスト構成プロトコル (DHCP) サーバー サービスのパラメーターを使用できます。 レジストリを変更することもできます。  
  
-   互換性の問題のすべてのアプリケーションを慎重にテストする必要があります。  
  
実行できる手順の詳細についてはこれらの欠点に対処するための作成を参照不整合のある Namespace ([https://go.microsoft.com/fwlink/?LinkId=106638](https://go.microsoft.com/fwlink/?LinkId=106638))。  
  
### <a name="planning-a-namespace-transition"></a>名前空間の移行の計画  
名前空間を変更する前に、連続する名前空間の不整合の名前空間 (またはその逆) からの状態遷移に適用する次の考慮事項を確認します。  
  
-   手動で構成されているサービス プリンシパル名 (SPN) 可能性がありますと一致しなく DNS 名の名前空間の変更後。 これにより、認証エラーが発生することができます。  
  
    詳細については、サービスのログオンが原因で SPN を正しく設定を参照してください ([https://go.microsoft.com/fwlink/?LinkId=102304](https://go.microsoft.com/fwlink/?LinkId=102304))。  
  
    -   制約付き委任を Windows Server 2003 ベースのコンピューターを使用する場合、これらのコンピューターは、SPN を変更する追加の構成を必要があります。 詳細については、936628、Microsoft サポート技術情報の記事を参照してください ([https://go.microsoft.com/fwlink/?LinkId=102306](https://go.microsoft.com/fwlink/?LinkId=102306))。  
  
    -   管理者の下位に SPN を変更するアクセス許可を委任する場合は、SPN を変更する権限を委任するを参照してください ([https://go.microsoft.com/fwlink/?LinkId=106639](https://go.microsoft.com/fwlink/?LinkId=106639))。  
  
-   経由で Secure Sockets Layer (SSL) (LDAPS と呼ばれます) 不整合な名前空間で構成されているドメイン コントローラーのある展開の CA とライトウェイト ディレクトリ アクセス プロトコル (LDAP) を使用する場合、LDAPS 証明書を構成するときに、適切な Active Directory ドメイン名とプライマリ DNS サフィックスを使用する必要があります。  
  
    ドメイン コントローラーの証明書要件の詳細については、321051、Microsoft サポート技術情報の記事を参照してください ([https://go.microsoft.com/fwlink/?LinkId=102307](https://go.microsoft.com/fwlink/?LinkId=102307))。  
  
    > [!NOTE]  
    > LDAPS の証明書を使用するドメイン コントローラーは、その証明書を再展開する必要があります。 これを行うときにドメイン コントローラーを選択できません適切な証明書再起動されるまで。 Windows Server 2003 の LDAPS 認証、および関連する更新プログラムの詳細については、932834、Microsoft サポート技術情報の記事を参照してください ([https://go.microsoft.com/fwlink/?LinkId=102308](https://go.microsoft.com/fwlink/?LinkId=102308))。  
  
### <a name="planning-for-disjoint-namespace-deployments"></a>不整合な名前空間の展開の計画  
不整合な名前空間が存在する環境でコンピューターを展開する場合は、次の予防措置を実行します。  
  
1.  すべてのソフトウェア ベンダーがビジネスことのテストし、不整合な名前空間をサポートする必要がありますを行う相手に通知します。 不整合な名前空間を使用している環境で各自のアプリケーションをサポートすることを確認するを尋ねます。  
  
2.  不整合な名前空間のラボ環境ですべてのバージョンのオペレーティング システムとアプリケーションをテストします。 実行すると、これらの推奨事項に従います。  
  
    1.  お客様の環境にソフトウェアを展開する前に、すべてのソフトウェアの問題を解決します。  
  
    2.  可能であればへの参加のオペレーティング システムとアプリケーションを不整合な名前空間を展開する予定のベータ テストします。  
  
3.  管理者およびヘルプ デスクのスタッフが不整合な名前空間とその影響理解していることを確認します。  
  
4.  できるようになりますを移行する、隣接する名前空間を不整合な名前空間から必要に応じて計画を作成します。  
  
5.  オペレーティング システムとアプリケーション プロバイダーのサポートを不整合な名前空間の重要度を宣伝します。  
  


