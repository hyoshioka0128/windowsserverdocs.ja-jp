---
ms.assetid: 864ad4bc-8428-4a8b-8671-cb93b68b0c03
title: Active Directory の攻撃を削減する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d692641d316b5fe7206cc3f413bdcfc9b74675b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874153"
---
# <a name="reducing-the-active-directory-attack-surface"></a>Active Directory の攻撃を削減する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このセクションでは、Active Directory のインストールの攻撃を軽減するために実装の技術的コントロールについて説明します。 セクションには、次の情報が含まれています。  
  
-   [最低限の特権の管理モデルを実装する](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)の使用が高度な権限をリスクの特定に重点を置くのアカウントに関する推奨事項、リスクを軽減するために実装を提供するだけでなく、日常的な管理を表示しますそのアカウントに存在します。  
  
-   [セキュリティで保護された管理ホストを実装する](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)いくつかのサンプルだけでなく、セキュリティで保護された、専用の管理システムの展開にセキュリティで保護された管理ホストの展開に近づく原則について説明します。  
  
-   [攻撃からのドメイン コント ローラーをセキュリティで保護する](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)ポリシーとセキュリティで保護された管理用のホストの実装のための推奨事項に似ていますに役立ついくつかのドメイン コント ローラーに固有の推奨事項が含まれている設定について説明しますドメイン コント ローラーとそれらを管理するために使用するシステムが適切にセキュリティで保護されたことを確認します。  
  
## <a name="privileged-accounts-and-groups-in-active-directory"></a>Active Directory の特権アカウントとグループ  
このセクションでは、特権アカウントに関する背景情報を提供し、Active Directory でグループの共通点と Active Directory での特権アカウントとグループの違いについて説明するためのものです。 このような違いを理解すると、かどうかを実装する推奨事項[最低限の特権の管理モデルを実装する](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)逐語的または組織用にカスタマイズするに必要なツールがあります。各グループおよびアカウントを適切にセキュリティで保護します。  
  
### <a name="built-in-privileged-accounts-and-groups"></a>組み込み特権アカウントとグループ  
Active Directory では、管理の委任を容易にし、権限とアクセス許可を割り当てるときに最小特権の原則をサポートします。 ドメインにアカウントを持っている"regular"のユーザーがディレクトリに格納される内容の多くを読めるように、既定しますが、ディレクトリ内のデータは非常に限定されたセットの変更できます。 追加の特権を必要とするユーザーには、各自の役割に関連する特定のタスクを実行できますが、各自の作業に関係のないタスクを実行することはできません、ようにディレクトリに組み込まれているさまざまな「管理者」グループのメンバーシップを付与できます。 組織は、特定の職務に合わせてカスタマイズし、詳細な権限と、it スタッフは、権限とアクセス許可を超えるものを付与しなくても日常的な管理機能を実行できるようにするアクセス許可が付与されますグループを作成もできます。これらの関数に必要です。  
  
Active Directory は、次の 3 つのビルトイン グループがディレクトリ内の最上位の特権グループです。Enterprise Admins、Domain Admins、および管理者。 既定の構成とこれらの各グループの機能は、次のセクションについて説明します。  
  
#### <a name="highest-privilege-groups-in-active-directory"></a>Active Directory 内の最上位の特権グループ  
  
##### <a name="enterprise-admins"></a>Enterprise Admins  
Enterprise Admins (EA) は、フォレスト ルート ドメインにのみ存在するグループであり、既定では、フォレスト内のすべてのドメインで、Administrators グループのメンバーであります。 フォレスト ルート ドメインのビルトイン Administrator アカウントは、EA のグループの唯一の既定のメンバーです。 EAs には、追加や削除などドメイン、フォレストの信頼を確立するフォレスト機能レベルを上げる権利とフォレスト全体の変更 (つまり、変更、フォレスト内のすべてのドメインに影響を与える) を実装するために行えるようにするアクセス許可が付与されます。 正しく設計と実装の委任モデルでは、まずフォレストを構築するときにのみ、または送信フォレスト信頼を確立するなど特定のフォレスト全体の変更を行うときにで EA のメンバーシップが必要です。 ほとんどの権限と、EA のグループに付与されるアクセス許可は、低い特権のあるユーザーとグループに委任できます。  
  
##### <a name="domain-admins"></a>Domain Admins  

フォレスト内の各ドメインでは、そのドメインの管理者グループのメンバーと、ドメインに参加しているすべてのコンピューターでローカルの Administrators グループのメンバーは、独自のドメイン管理者 (DA) グループがあります。 DA、ドメイン グループの唯一の既定のメンバーは、そのドメインの組み込み管理者アカウントです。 DAs は、EAs がフォレスト全体の特権のドメイン内で「強力な」です。 正しく設計と実装の委任モデルでは、Domain Admins のメンバーシップを (ドメイン内のすべてのコンピューターに対する高いレベルの特権を持つアカウントが必要な場合) などの「非常時」のシナリオでのみ必要にする必要があります。 ネイティブ Active Directory 委任メカニズムは委任を許可できる程度に緊急の場合にのみ DA アカウントを使用することは、時間がかかり、することができます、効果的な委任モデルを構築して多くの組織を活用処理時間を短縮するサード パーティ製のツールです。  
  
##### <a name="administrators"></a>管理者  
3 番目のグループは、先 DAs および EAs が入れ子に組み込みのドメイン ローカル管理者 (BA) グループです。 このグループには、直接権限とアクセス許可とドメイン コント ローラーのディレクトリ内の多くが許可されます。 ただし、サーバーまたはワークステーションのメンバーでは、ドメインの管理者グループが特権ありません。 ローカルの特権が付与されているコンピューターのローカルの Administrators グループのメンバーシップを通じてが。  
  
> [!NOTE]  
> これらの権限を持つグループの既定の構成は、次の 3 つのグループのいずれかのメンバーは任意の他のグループのメンバーシップを取得するディレクトリを操作できます。 場合によってを簡単に他のグループのメンバーシップを取得中には困難ですが、他のユーザーもと事実上同じ見なす必要がありますすべての 3 つのグループの潜在的な特権の観点からなります。  
  
##### <a name="schema-admins"></a>Schema Admins  

4 つ目の特権グループ、スキーマ管理者 (SA) が、フォレスト ルート ドメインのみに存在して、Enterprise Admins グループと同様に、既定のメンバーとしてそのドメインの組み込み管理者アカウントだけを持ちます。 Schema Admins グループの目的は、場合によっては (AD DS スキーマの変更が必要な場合) と一時的にのみ設定します。  
  
SA グループの権限とアクセス許可のスコープは、既に説明したよりも制限 SA グループ (よし、オブジェクトや属性などのディレクトリの基になるデータ構造) は、Active Directory スキーマを変更できる唯一のグループですが、グループ。 通常、グループのメンバーシップが必要頻度が低いため、短時間に対してのみ、組織に SA グループのメンバーシップの管理のための適切なプラクティスを開発したを検索する一般的です。 これは、EA、DA、および BA 内のグループの Active Directory は、同様に、技術的には true が、組織には、SA グループとこれらのグループのようなプラクティスが実装されてを検索するはるかに少ないが一般的です。  
  
#### <a name="protected-accounts-and-groups-in-active-directory"></a>保護されたアカウントと Active Directory のグループ  
Active Directory 内で特権アカウントとグループの既定のセットには、"protected"アカウントと呼ばれ、グループがディレクトリ内の他のオブジェクトとは異なるセキュリティで保護します。 (かどうか、メンバーシップがセキュリティまたは配布グループから派生) に関係なくその保護グループの直接または推移的メンバーシップを持つ任意のアカウントは、この制限付きのセキュリティを継承します。  

  
たとえば、ユーザーが配布グループのメンバーは、さらに場合、Active Directory、そのユーザー オブジェクトでの保護グループのメンバーは保護されているアカウントとしてフラグが設定します。 アカウントは、保護されているアカウントとしてフラグが設定された、ときに、オブジェクトの adminCount 属性の値が 1 に設定されます。  
  
> [!NOTE]
> 保護グループ内の推移的メンバーシップには、入れ子になった配布とネストされたセキュリティ グループが含まれますが、入れ子になった配布グループのメンバーであるアカウントでは、アクセス トークンは、保護グループの SID は受け取りません。 ただし、配布グループは、Active Directory は、保護グループ メンバーの列挙体に配布グループを含めるためのセキュリティ グループに変換できます。 保護された入れ子になった配布グループをこれまでに変換するか、セキュリティ グループ、アカウントは、前者の配布グループのメンバーは親受信後に、次回のログオン時に、そのアクセス トークンでのグループの SID が保護されています。  
  
次の表には、既定の保護アカウントとオペレーティング システムのバージョンおよびサービス パック レベルでの Active Directory のグループが一覧表示します。  
  
**既定のオペレーティング システムとバージョンの Service Pack (SP) で Active Directory で保護されたアカウントおよびグループ**  
  
|||||  
|-|-|-|-|  
|**Windows 2000 <SP4**|**Windows 2000 SP4 -Windows Server 2003**|**Windows Server 2003 SP1 以降**|**Windows Server 2008、Windows Server 2012**|  
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
  
##### <a name="adminsdholder-and-sdprop"></a>AdminSDHolder および SDProp  
すべての Active Directory ドメインのシステム コンテナー、AdminSDHolder をという名前のオブジェクトが自動的に作成します。 AdminSDHolder オブジェクトでは、保護グループとアカウントがドメインにある場所に関係なく、保護されたアカウントとグループのアクセス許可を一貫して適用されることを確認します。  

60 分 (既定) では、ドメインの PDC エミュレーターの役割を保持するドメイン コント ローラーで、セキュリティ記述子の伝達子 (SDProp) と呼ばれるプロセスが実行されます。 SDProp は、保護されたアカウントとドメイン内のグループ、アクセス許可を持つ、ドメインの AdminSDHolder オブジェクトに対する権限を比較します。 保護されたアカウントとグループのいずれかのアクセス許可では、AdminSDHolder オブジェクトのアクセス許可は一致しない場合、ドメインの AdminSDHolder オブジェクトと一致するように、保護されたアカウントとグループのアクセス許可がリセットされます。  
  
アクセス許可の継承は無効で保護されたグループとアカウントをする場合でも、アカウントまたはグループは、ディレクトリ内の別の場所に移動が権限を継承しない、新しい親オブジェクトからです。 AdminSDHolder オブジェクトでは、継承が、親オブジェクトへのアクセス許可の変更が AdminSDHolder のアクセス許可を変更しないようにも無効になります。  
  
> [!NOTE]
> 保護グループからアカウントを削除するときに、保護されたアカウントが手動で変更されていない場合は、1 に設定されたその adminCount 属性ままと見なされません。 この構成の結果がオブジェクトの Acl が SDProp、によって更新されないオブジェクトも継承しないアクセス許可、親オブジェクト。 そのため、オブジェクトは、組織単位 (OU) にアクセス許可を委任されている、以前保護されているオブジェクトはこれらの委任されたアクセス許可を継承しませんに置か可能性があります。 検索して、ドメインで以前に保護されているオブジェクトをリセットするスクリプトが記載されて、 [Microsoft サポート記事 817433](https://support.microsoft.com/?id=817433)します。  
  
###### <a name="adminsdholder-ownership"></a>AdminSDHolder 所有権  
Active Directory 内のほとんどのオブジェクトは、ドメインの BA グループによって所有されます。 ただし、AdminSDHolder オブジェクトが、既定では、所有ドメインの DA グループ。 (これは、DAs は、権限と、ドメインの管理者グループのメンバーシップを介したアクセス許可しない派生状況です)。  
  
Windows Server 2008 より前のバージョンの Windows では、オブジェクトの所有者はもともと含まれていないアクセス許可の付与自体など、オブジェクトのアクセス許可を変更できます。 そのため、ドメインの AdminSDHolder オブジェクトの既定のアクセス許可は、ドメインの AdminSDHolder オブジェクトのアクセス許可の変更から BA または EA のグループのメンバーであるユーザーを防止します。 ただし、ドメインの管理者グループのメンバーがオブジェクトの所有権を取得し、自分に与えます追加のアクセス許可、つまり、この保護が不十分であり、のみであるユーザーが誤って変更対象のオブジェクトを保護します。DA、ドメイン グループのメンバー以外。 さらに、BA および EA (必要に応じて) グループはローカル ドメイン (EA のルート ドメイン) 内の AdminSDHolder オブジェクトの属性を変更する権限します。  
  
> [!NOTE]  
> DSHeuristics の AdminSDHolder オブジェクトの属性は、保護グループと見なされ、AdminSDHolder および SDProp によって影響を受けるグループの限定的なカスタマイズ (削除) できます。 このカスタマイズ考慮する必要が慎重に実装すると、有効な状況で dSHeuristics AdminSDHolder での変更が便利ですが。 AdminSDHolder オブジェクトで dSHeuristics 属性の変更の詳細については、Microsoft サポート記事では[817433](https://support.microsoft.com/?id=817433)と[973840](https://support.microsoft.com/kb/973840)、および[付録 c:Active Directory のアカウントとグループの保護](Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)します。  
  
その他の数がある Active Directory で最も特権を持つグループがここで説明されているが付与されたグループ レベルの特権を昇格します。 すべての既定値と組み込みのグループには、Active Directory とそれぞれに割り当てられたユーザー権限の詳細については、次を参照してください[付録 b:。特権アカウントと Active Directory でグループ](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)します。  
  


