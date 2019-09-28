---
ms.assetid: 864ad4bc-8428-4a8b-8671-cb93b68b0c03
title: Active Directory の攻撃を削減する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 94bc65d42fa90dd7c93ba759a41d34edec10de09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367648"
---
# <a name="reducing-the-active-directory-attack-surface"></a>Active Directory の攻撃を削減する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このセクションでは、Active Directory のインストールの攻撃対象領域を減らすために実装する技術コントロールについて説明します。 このセクションには、次の情報が含まれています。  
  
-   [最小限の特権を持つ管理モデルを実装](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)することは、日常の管理に高い特権を持つアカウントを使用するというリスクを特定することに重点を置いています。また、を実装して、特権アカウントが存在します。  
  
-   セキュリティで保護された管理ホストの[実装](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)は、セキュリティで保護された管理ホストの展開に対するいくつかのサンプルアプローチに加えて、セキュリティで保護された専用管理システムを展開するための原則について  
  
-   [攻撃からドメインコントローラーを保護](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)するポリシーと設定について説明しますが、セキュリティで保護された管理ホストの実装に関する推奨事項に似ていますが、ドメインコントローラーに固有の推奨事項がいくつか含まれています。ドメインコントローラとそれらを管理するために使用されるシステムが適切にセキュリティで保護されていることを確認します。  
  
## <a name="privileged-accounts-and-groups-in-active-directory"></a>Active Directory の特権付きアカウントとグループ  
このセクションでは、Active Directory の特権アカウントとグループの共通点と相違点を説明するための Active Directory の特権アカウントとグループに関する背景情報について説明します。 これらの違いを理解することで、[最小特権の管理モデルの実装](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)に関する推奨事項をそのまま使用するか、組織に合わせてカスタマイズするかにかかわらず、各グループをセキュリティで保護するために必要なツールが用意されています。適切なアカウント。  
  
### <a name="built-in-privileged-accounts-and-groups"></a>組み込みの特権アカウントとグループ  
Active Directory により、管理の委任が容易になり、権限とアクセス許可を割り当てる際の最小限の特権の原則がサポートされます。 ドメイン内にアカウントを持つ "通常の" ユーザーは、既定では、ディレクトリに格納されているものの多くを読み取ることができますが、ディレクトリ内のデータのごく一部のみを変更することができます。 追加の特権を必要とするユーザーは、ディレクトリに組み込まれているさまざまな "特権のある" グループのメンバーシップを付与することができます。これにより、ロールに関連する特定のタスクを実行できますが、職務に関係のないタスクを実行することはできません。 組織は、特定のジョブの役割に合わせて調整されたグループを作成することもできます。また、IT スタッフが日常的な管理機能を実行するための権限とアクセス許可が付与されます。これらの関数にはが必要です。  
  
Active Directory 内では、次の3つの組み込みグループが、ディレクトリ内の最上位の特権グループになります。Enterprise Admins、Domain Admins、および Administrators。 これらの各グループの既定の構成と機能については、次のセクションで説明します。  
  
#### <a name="highest-privilege-groups-in-active-directory"></a>Active Directory の最上位の特権グループ  
  
##### <a name="enterprise-admins"></a>Enterprise Admins  
Enterprise Admins (EA) は、フォレストのルートドメインにのみ存在するグループで、既定では、フォレスト内のすべてのドメインの Administrators グループのメンバーです。 フォレストルートドメインの組み込みの Administrator アカウントは、EA グループの唯一の既定のメンバーです。 EAs には、ドメインの追加または削除、フォレストの信頼の確立、フォレストの機能レベルの設定など、フォレスト全体の変更 (フォレスト内のすべてのドメインに影響を与える変更) の実装を可能にする権限とアクセス許可が付与されます。 適切に設計および実装された委任モデルでは、最初にフォレストを構築するとき、または、送信フォレストの信頼を確立するなどの特定のフォレスト全体の変更を行うときにのみ、EA のメンバーシップが必要になります。 EA グループに付与されている権限とアクセス許可のほとんどは、より低い特権のユーザーおよびグループに委任できます。  
  
##### <a name="domain-admins"></a>Domain Admins  

フォレスト内の各ドメインには、独自のドメイン管理者 (DA) グループがあります。このグループは、そのドメインの Administrators グループのメンバーであり、ドメインに参加しているすべてのコンピューターのローカルの Administrators グループのメンバーです。 ドメインの DA グループの既定のメンバーは、そのドメインの組み込みの Administrator アカウントのみです。 DAs はドメイン内では "すべて強力" であり、EAs にはフォレスト全体の特権があります。 適切に設計および実装された委任モデルでは、ドメイン管理者のメンバーシップが必要になるのは、"中断" のシナリオ (ドメイン内のすべてのコンピューターに対して高いレベルの特権を持つアカウントが必要な場合など) のみです。 ネイティブ Active Directory の委任メカニズムでは、緊急のシナリオでのみ DA アカウントを使用できるという程度の委任が可能ですが、効果的な委任モデルの構築には時間がかかることがあり、多くの組織ではを活用できます。プロセスを迅速に実行するサードパーティ製のツール。  
  
##### <a name="administrators"></a>管理者  
3番目のグループは、DAs と EAs が入れ子になっている組み込みのドメインローカル管理者 (BA) グループです。 このグループには、ディレクトリおよびドメインコントローラーの直接の権限とアクセス許可の多くが付与されます。 ただし、ドメインの Administrators グループには、メンバーサーバーまたはワークステーションに対する権限がありません。 ローカルの特権が付与されているコンピューターのローカル管理者グループのメンバーシップを介して行われます。  
  
> [!NOTE]  
> これらはこれらの特権グループの既定の構成ですが、3つのグループのいずれかのメンバーは、そのディレクトリを操作して他のすべてのグループのメンバーシップを取得することができます。 場合によっては、他のグループのメンバーシップを取得するのは簡単ですが、それ以外の場合はより困難ですが、潜在的な特権の観点からは、3つのグループすべてが実質的に同等であると見なされる必要があります。  
  
##### <a name="schema-admins"></a>Schema Admins  

4番目の特権グループである Schema Admins (SA) は、フォレストのルートドメインにのみ存在し、Enterprise Admins グループと同様に、そのドメインの組み込みの Administrator アカウントのみが既定のメンバーになります。 Schema Admins グループは、一時的かつときどき (AD DS スキーマの変更が必要な場合) に設定することを目的としています。  
  
SA グループは Active Directory スキーマ (つまり、オブジェクトや属性などのディレクトリの基になるデータ構造) を変更できる唯一のグループですが、SA グループの権限とアクセス許可のスコープは前に説明したものよりも制限されています。グループ. また、グループのメンバーシップは通常はあまり必要ではなく、短時間にしか使用されないため、SA グループのメンバーシップを管理するための適切な方法が組織によって開発されていることがわかります。 これは、Active Directory の EA、DA、および BA グループについても技術的には当てはまりますが、組織が SA グループに対して同様のプラクティスを実装していることを確認するのは、あまり一般的ではありません。  
  
#### <a name="protected-accounts-and-groups-in-active-directory"></a>Active Directory の保護されたアカウントとグループ  
Active Directory 内では、特権アカウントとグループの既定のセットである "protected" アカウントとグループは、ディレクトリ内の他のオブジェクトとは異なる方法で保護されます。 保護されたグループの直接または推移的なメンバーシップを持つアカウント (メンバーシップがセキュリティグループと配布グループのどちらから派生しているかに関係なく) は、この制限付きセキュリティを継承します。  

  
たとえば、ユーザーが Active Directory の保護されたグループのメンバーである配布グループのメンバーである場合、そのユーザーオブジェクトには保護されたアカウントのフラグが設定されます。 アカウントに保護されたアカウントのフラグが設定されている場合は、オブジェクトの adminCount 属性の値が1に設定されます。  
  
> [!NOTE]
> 保護されたグループの推移的なメンバーシップには、入れ子になったディストリビューションと入れ子になったセキュリティグループが含まれますが、入れ子になった配布グループのメンバーであるアカウントは、そのアクセストークンで保護されたグループの SID を受け取りません。 ただし、配布グループを Active Directory のセキュリティグループに変換することができます。そのため、配布グループは、保護されたグループメンバーの列挙に含まれています。 保護された入れ子になった配布グループをセキュリティグループに変換したことがある場合、その配布グループのメンバーであるアカウントは、その後次回ログオン時に、親の保護されたグループの SID をアクセストークンで受信します。  
  
次の表は、Active Directory の既定の保護されたアカウントとグループをオペレーティングシステムのバージョンおよび Service Pack レベル別に示しています。  
  
**オペレーティングシステムおよび Service Pack (SP) のバージョンによって Active Directory の既定の保護されたアカウントとグループ**  
  
|||||  
|-|-|-|-|  
|**Windows 2000 < SP4**|**Windows 2000 SP4-Windows Server 2003**|**Windows Server 2003 SP1 +**|**Windows Server 2008-Windows Server 2012**|  
|管理者|Account Operators|Account Operators|Account Operators|  
||管理者|管理者|管理者|  
||管理者|管理者|管理者|  
|Domain Admins|Backup Operators|Backup Operators|Backup Operators|  
||Cert Publishers|||  
||Domain Admins|Domain Admins|Domain Admins|  
|Enterprise Admins|ドメイン コントローラー|ドメイン コントローラー|ドメイン コントローラー|  
||Enterprise Admins|Enterprise Admins|Enterprise Admins|  
||Krbtgt|Krbtgt|Krbtgt|  
||Print Operators|Print Operators|Print Operators|  
||||Read-Only Domain Controllers|  
||Replicator|Replicator|Replicator|  
|Schema Admins|Schema Admins||Schema Admins|  
  
##### <a name="adminsdholder-and-sdprop"></a>AdminSDHolder と SDProp  
すべての Active Directory ドメインのシステムコンテナーで、AdminSDHolder という名前のオブジェクトが自動的に作成されます。 AdminSDHolder オブジェクトの目的は、保護されたグループとアカウントがドメイン内に配置されている場所に関係なく、保護されたアカウントとグループに対するアクセス許可が確実に適用されるようにすることです。  

60分ごと (既定)、セキュリティ記述子伝達子 (SDProp) と呼ばれるプロセスが、ドメインの PDC エミュレーターの役割を持つドメインコントローラー上で実行されます。 SDProp は、ドメインの AdminSDHolder オブジェクトのアクセス許可と、ドメイン内の保護されたアカウントおよびグループのアクセス許可を比較します。 保護されているアカウントとグループのアクセス許可が、AdminSDHolder オブジェクトのアクセス許可と一致しない場合、保護されたアカウントとグループのアクセス許可は、ドメインの AdminSDHolder オブジェクトのアクセス許可と一致するようにリセットされます。  
  
権限の継承は、保護されたグループおよびアカウントでは無効になっています。つまり、アカウントまたはグループがディレクトリ内の別の場所に移動された場合でも、新しい親オブジェクトからアクセス許可を継承しません。 親オブジェクトに対するアクセス許可の変更によって、AdminSDHolder のアクセス許可が変更されないように、AdminSDHolder オブジェクトでも継承が無効になっています。  
  
> [!NOTE]
> 保護されたグループからアカウントを削除すると、保護されたアカウントとは見なされなくなりますが、手動で変更しない場合は、adminCount 属性が1に設定されたままになります。 この構成の結果として、オブジェクトの Acl は SDProp によって更新されなくなりますが、オブジェクトは親オブジェクトからアクセス許可を継承しません。 このため、オブジェクトは、権限が委任されている組織単位 (OU) に存在する場合がありますが、以前に保護されていたオブジェクトは、これらの委任されたアクセス許可を継承しません。 ドメイン内の以前に保護されたオブジェクトを検索してリセットするスクリプトは、 [Microsoft サポートの記事 817433](https://support.microsoft.com/?id=817433)に記載されています。  
  
###### <a name="adminsdholder-ownership"></a>AdminSDHolder の所有権  
Active Directory 内のほとんどのオブジェクトは、ドメインの BA グループによって所有されています。 ただし、既定では、AdminSDHolder オブジェクトはドメインの DA グループによって所有されています。 (これは、DAs がドメインの Administrators グループのメンバーシップを使用して権限とアクセス許可を派生させない状況です)。  
  
Windows Server 2008 より前のバージョンの Windows では、オブジェクトの所有者は、オブジェクトのアクセス許可を変更することができます。これには、元になっていなかったアクセス許可の付与などが含まれます。 そのため、ドメインの AdminSDHolder オブジェクトに対する既定のアクセス許可により、BA グループまたは EA グループのメンバーであるユーザーは、ドメインの AdminSDHolder オブジェクトのアクセス許可を変更できません。 ただし、ドメインの Administrators グループのメンバーは、オブジェクトの所有権を取得し、追加のアクセス許可を与えることができます。つまり、この保護は基本的で、ドメイン内の DA グループのメンバーではありません。 また、BA および EA (該当する場合) グループには、ローカルドメイン (EA のルートドメイン) の AdminSDHolder オブジェクトの属性を変更するアクセス許可があります。  
  
> [!NOTE]  
> AdminSDHolder オブジェクト dSHeuristics の属性では、保護されたグループと見なされ、AdminSDHolder と SDProp によって影響を受けるグループの限定されたカスタマイズ (削除) が可能です。 このカスタマイズは、実装されている場合は慎重に検討する必要がありますが、AdminSDHolder で dSHeuristics を変更すると便利な場合があります。 AdminSDHolder オブジェクトでの dSHeuristics 属性の変更の詳細については、Microsoft サポートの記事[817433](https://support.microsoft.com/?id=817433)と[973840](https://support.microsoft.com/kb/973840)、および @no__t 付録 C:Active Directory @ no__t の保護されたアカウントとグループ。  
  
ここでは、Active Directory の最も特権の高いグループについて説明しますが、管理者特権のレベルが付与されているグループが他にも多数あります。 Active Directory のすべての既定および組み込みグループと、それぞれに割り当てられているユーザー権利の詳細については、「[Appendix B:Active Directory @ no__t の特権のあるアカウントおよびグループ。  
  


