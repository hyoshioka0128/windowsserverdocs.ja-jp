---
ms.assetid: 864ad4bc-8428-4a8b-8671-cb93b68b0c03
title: "Active Directory の攻撃対象領域を減らす"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b2de254076b10a1a75d658f006c2245d523de6b7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="reducing-the-active-directory-attack-surface"></a>Active Directory の攻撃対象領域を減らす

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このセクションでは、Active Directory のインストールの攻撃を軽減するために実装の技術的コントロールについて説明します。 セクションには、次の情報が含まれています。  
  
-   [最低限の特権の管理モデルを実装する](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)特権アカウントが存在するリスクを軽減するために実装するための推奨事項を提供するだけでなく、日常的な管理の高い権限を持つアカウントの使用を表示するリスクの識別に焦点を当てています。  
  
-   [セキュリティで保護された管理ホストを実装する](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)をセキュリティで保護された管理ホストの展開のいくつかのサンプルだけでなく、セキュリティで保護された、専用の管理システムの展開のアプローチの原則をについて説明します。  
  
-   [攻撃からドメイン コントローラーをセキュリティで保護する](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)ポリシーとセキュリティで保護された管理ホストの実装に関する推奨事項に似ていますが、ドメイン コントローラーとそれらを管理するために使用するシステムが適切にセキュリティで保護されたことを確認するドメイン コントローラーに固有の推奨事項が含まれている設定について説明します。  
  
## <a name="privileged-accounts-and-groups-in-active-directory"></a>Active Directory の特権を持つアカウントとグループ  
このセクションでは、特権アカウントに関する背景情報を提供し、Active Directory のグループが Active Directory の権限を持つアカウントとグループの違い、共通点を説明するものです。 これらの違いを理解すると、かどうかを実装するの推奨事項[最低限の特権の管理モデルを実装する](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)逐語的または、組織用にカスタマイズするには、各グループをセキュリティで保護し、適切なアカウントに必要なツールです。  
  
### <a name="built-in-privileged-accounts-and-groups"></a>組み込みの特権アカウントとグループ  
Active Directory は、管理の委任を容易にし、権限とアクセス許可を割り当てることで最低限の特権の原則をサポートします。 ドメインにアカウントを持つユーザーは、「通常」は、既定で、ディレクトリに保存される情報の多くを読み取ることができませんが、ディレクトリ内のデータのセットがごく一部のみを変更することは。 追加の特権を必要とするユーザーには、その役割に関連する特定のタスクを実行することがありますが各自の作業に関連性の低いタスクを実行できないように、そのディレクトリに組み込まれているさまざまな「の特権」グループのメンバーシップを付与できます。 組織では、特定の職務に合わせて調整されますおよび細分化された権限と IT スタッフの権限とそれらの関数に必要なは不可能なアクセス許可を付与せず日常的な管理機能は実行を許可するアクセス許可が付与されているグループも作成できます。  
  
Active Directory は、次の 3 つのビルトイン グループがディレクトリ内の最上位の特権グループ: Enterprise Admins、Domain Admins、および管理者。 既定の構成とこれらのグループのそれぞれの機能は、次のセクションについて説明します。  
  
#### <a name="highest-privilege-groups-in-active-directory"></a>Active Directory 内の最上位の特権グループ  
  
##### <a name="enterprise-admins"></a>Enterprise Admins  
Enterprise Admins (EA) は、フォレスト ルート ドメイン内にのみ存在するグループであり、既定では、フォレスト内のすべてのドメイン内の Administrators グループのメンバーであります。 フォレスト ルート ドメインのビルトイン Administrator アカウントは、EA グループの唯一の既定のメンバーです。 EAs はなどの追加や削除、ドメイン、フォレストの信頼を確立するフォレスト機能レベルを上げる権限とそれらのフォレスト全体の変更 (つまり、変更、フォレスト内のすべてのドメインに影響を与える) の実装を許可するアクセス許可が付与されます。 適切に設計され、実装された委任モデルでは、まずフォレストを作成する場合にのみ、または送信フォレスト信頼を確立するなどの特定のフォレスト全体にわたる変更を行うときにで EA メンバーシップが必要です。 EA グループに付与されたアクセス許可と権利のほとんどは、権限の低いユーザーとグループに委任できます。  
  
##### <a name="domain-admins"></a>Domain Admins  

フォレスト内の各ドメインが、そのドメインの管理者グループのメンバーと、ドメインに参加しているすべてのコンピューターでローカルの Administrators グループのメンバーは、独自のドメイン管理者 (DA) グループです。 DA、ドメインのグループの唯一の既定のメンバーは、そのドメインのビルトイン Administrator アカウントです。 Da は、EAs がフォレスト全体の権限を持っているときに、ドメイン内で「強力な」です。 適切に設計され、実装された委任モデルで (ドメイン内のすべてのコンピューター上には、高いレベルの特権を持つアカウントが必要がある場合) など、"break glass"シナリオでのみ Domain Admins のメンバーシップを必要する必要があります。 ネイティブの Active Directory 委任メカニズムには、委任緊急の場合にのみ DA アカウントを使用することはするが、効果的な委任モデルを構築することが時間がかかり、でき、多くの組織が迅速に処理するサード パーティ製ツールを活用します。  
  
##### <a name="administrators"></a>管理者  
3 番目のグループは、ビルトイン ドメイン ローカル管理者 (BA) グループを DAs および EAs が入れ子にです。 このグループは、直接的な権限とアクセス許可およびドメイン コントローラー、ディレクトリ内の多くが付与されます。 ただし、ドメインの管理者グループを持たない特権メンバー サーバーまたはワークステーションにします。 ローカルの権限が付与されているコンピューターのローカルの Administrators グループのメンバーシップ経由でです。  
  
> [!NOTE]  
> これらは、これらの特権グループの既定の構成が、3 つのグループのいずれかのメンバーは、その他のグループのいずれかでメンバーシップを取得するディレクトリを操作できます。 場合によってを簡単にその他のグループのメンバーシップを取得中にはより困難ですが、他のユーザーも、実質的に同等見なす必要が 3 つのグループをすべての潜在的な特権の観点からです。  
  
##### <a name="schema-admins"></a>Schema Admins  

4 つ目の特権グループ、スキーマ管理者 (SA) が、フォレスト ルート ドメインにしか存在しないし、Enterprise Admins グループのような既定のメンバーとしてのみそのドメインのビルトイン Administrator アカウントには。 Schema Admins グループのことがあります (AD DS スキーマの変更が必要な場合) と一時的に格納する目的です。  
  
SA グループ (の [ディレクトリの基になるデータ構造オブジェクトと属性など)、Active Directory スキーマを変更することのできるだけのグループでは、SA グループの権利とアクセス許可の範囲は、既に説明したグループよりも制限されます。 通常、グループのメンバーシップが必要頻度が低いため、短時間にのみ、組織に SA グループのメンバーシップを管理するための適切なプラクティスを開発したを検索する一般的なもあります。 これは、EA、DA、および BA 内のグループの Active Directory は、同様に、技術的には true がはるかに低くなりますに共通の組織が SA グループとこれらのグループのようなプラクティスを実装していることを確認します。  
  
#### <a name="protected-accounts-and-groups-in-active-directory"></a>Active Directory の保護されたアカウントとグループ  
Active Directory 内で特権アカウントとグループの既定のセットが「保護された」アカウントと呼ばれ、グループがディレクトリ内の他のオブジェクトとは異なるセキュリティで保護します。 (かどうか、メンバーシップはセキュリティまたは配布グループから派生) に関係なく、保護グループの直接または推移的なメンバーシップを持つ任意のアカウントは、この制限付きのセキュリティを継承します。  

  
たとえば、ユーザーがいる場合、配布グループのメンバーは、さらに、Active Directory、その user オブジェクト内の保護グループのメンバーは保護されているアカウントとしてフラグが設定します。 保護されたアカウントとしてアカウントを設定すると、オブジェクトの adminCount 属性の値は 1 に設定されます。  
  
> [!NOTE]
> 推移的な保護グループのメンバーシップには、入れ子になった配布と入れ子になったセキュリティ グループが含まれますが、入れ子になった配布グループのメンバーであるアカウントでは、アクセス トークンは、保護グループの SID は受け取りません。 ただし、配布グループは、その保護グループ メンバーの列挙型で配布グループが含まれているため、Active directory セキュリティ グループに変換できます。 保護された入れ子になった配布グループこれまでに変換するセキュリティ グループ、前者の配布グループのメンバーは、親を受信して後であるアカウントには、次回ログオン時のアクセス トークンでグループの SID が保護されています。  
  
次の表は、保護されている既定のアカウントとオペレーティング システムのバージョンおよびサービス パック レベルでの Active Directory のグループを示します。  
  
**既定では、オペレーティング システムと Service Pack (SP) のバージョンの Active Directory のアカウントとグループの保護**  
  
|||||  
|-|-|-|-|  
|**Windows 2000 < SP4**|**Windows 2000 SP4、Windows Server 2003**|**Windows Server 2003 SP1 +**|**Windows Server 2008、Windows Server 2012**|  
|管理者|アカウント オペレーター|アカウント オペレーター|アカウント オペレーター|  
||管理者|管理者|管理者|  
||管理者|管理者|管理者|  
|Domain Admins|バックアップ オペレーター|バックアップ オペレーター|バックアップ オペレーター|  
||Cert Publishers|||  
||Domain Admins|Domain Admins|Domain Admins|  
|Enterprise Admins|ドメイン コント ローラー|ドメイン コント ローラー|ドメイン コント ローラー|  
||Enterprise Admins|Enterprise Admins|Enterprise Admins|  
||Krbtgt|Krbtgt|Krbtgt|  
||演算子を印刷します|演算子を印刷します|演算子を印刷します|  
||||読み取り専用ドメイン コント ローラー|  
||レプリケーター|レプリケーター|レプリケーター|  
|Schema Admins|Schema Admins||Schema Admins|  
  
##### <a name="adminsdholder-and-sdprop"></a>AdminSDHolder と SDProp  
すべての Active Directory ドメインのシステム コンテナーでという AdminSDHolder オブジェクトが自動的に作成します。 AdminSDHolder オブジェクトでは、保護グループとアカウントがドメインにある場所に関係なく、保護されたアカウントとグループのアクセス許可を一貫して適用されることを確認します。  

(既定) では 60 分ごとのセキュリティ記述子伝達子 (SDProp) と呼ばれるプロセスは、ドメインの PDC エミュレーターの役割を持つドメイン コントローラーで実行されます。 SDProp は、保護されたアカウントと、ドメイン内のグループのアクセス許可を持つ、ドメインの AdminSDHolder オブジェクトに対するアクセス許可を比較します。 保護されたアカウントとグループのいずれかのアクセス許可で AdminSDHolder オブジェクトに対するアクセス許可が一致しない場合、ドメインの AdminSDHolder オブジェクトのものと一致する保護されたアカウントとグループのアクセス許可がリセットされます。  
  
アクセス許可の継承が無効になって保護グループとアカウント、ことでもアカウントまたはグループに移動した場合、ディレクトリ内の別の場所を権限を継承しない、新しい親オブジェクトからを意味します。 AdminSDHolder オブジェクトでは、継承が、親オブジェクトへのアクセス許可の変更は AdminSDHolder のアクセス許可を変更しないようにも無効になります。  
  
> [!NOTE]
> 保護グループからアカウントが削除されると、不要になったと見なされます、保護されたアカウントがその adminCount 属性は手動で変更されていない場合は、1 に設定します。 この構成の結果が SDProp で、オブジェクトの Acl が不要になった更新されるオブジェクトはしないアクセス許可を継承その親オブジェクト。 そのため、オブジェクトは、組織単位 (OU) するアクセス許可が委任されている、以前に保護されたオブジェクトはこれらの委任されたアクセス許可を継承しませんに置か可能性があります。 検索し、ドメインで以前に保護されたオブジェクトをリセットするスクリプトは記載されて、[Microsoft サポートの記事 817433](https://support.microsoft.com/?id=817433)します。  
  
###### <a name="adminsdholder-ownership"></a>AdminSDHolder 所有権  
Active Directory 内のほとんどのオブジェクトは、ドメインの BA グループによって所有されます。 ただし、AdminSDHolder オブジェクトは、既定が所有するドメインの DA グループ。 (これは、DAs はその権限と、ドメインの管理者グループのメンバーシップ経由でアクセス許可しない派生状況です)。  
  
Windows Server 2008 より前のバージョンの Windows では、オブジェクトの所有者はもともと含まれていないアクセス許可の付与自体を含むオブジェクトのアクセス許可を変更できます。 そのため、ドメインの AdminSDHolder オブジェクトの既定のアクセス許可は、ドメインの AdminSDHolder オブジェクトに対するアクセス許可を変更できない BA または EA のグループのメンバーであるユーザーを防止します。 ただし、ドメインの管理者グループのメンバーは、オブジェクトの所有権を取得し、自分に与えます追加のアクセス許可、つまり、この保護は不十分であり、ドメイン内の DA グループのメンバーではないユーザーが誤って変更に対してオブジェクトを保護しかできます。 さらに、BA と EA (該当する箇所で) グループは、ローカル ドメイン (EA のルート ドメイン) 内の AdminSDHolder オブジェクトの属性を変更するアクセス許可を持っています。  
  
> [!NOTE]  
> AdminSDHolder オブジェクト、dSHeuristics の属性ではグループの保護グループと見なされ、AdminSDHolder と SDProp の影響を受けることの制限のカスタマイズ (削除)。 このカスタマイズ見なす必要が慎重に実装されている場合は dSHeuristics AdminSDHolder での変更が便利で有効な状況です。 AdminSDHolder オブジェクトで dSHeuristics 属性の変更の詳細については記載されて、Microsoft サポート記事[817433](https://support.microsoft.com/?id=817433)と[973840](https://support.microsoft.com/kb/973840)、し、[[付録 c: 保護されたアカウントと Active Directory のグループ](Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)します。  
  
Active Directory で最も特権グループがここで説明されているがその他の多くが付与されているグループ レベルの特権の昇格します。 詳細については、既定で組み込みのグループそれぞれに割り当てられたユーザー権限と Active Directory 内のすべて、次を参照してください。[付録 b: 特権のアカウントと Active Directory のグループ](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)します。  
  


