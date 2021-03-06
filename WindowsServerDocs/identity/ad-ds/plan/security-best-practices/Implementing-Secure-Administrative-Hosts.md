---
ms.assetid: eafdddc3-40d7-4a75-8f4f-a45294aabfc8
title: セキュリティで保護された管理用のホストを実装する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ed2ff7bfa0cc3b27506b1ca324e819860eef314c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890423"
---
# <a name="implementing-secure-administrative-hosts"></a>セキュリティで保護された管理用のホストを実装する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

セキュリティで保護された管理ホストがワークステーションまたは専用の元となる特権アカウントできる管理タスクを実行またはドメイン コント ローラーで Active Directory でセキュリティで保護されたプラットフォームを作成する目的で構成されているサーバーにはドメインに参加しているシステム、およびドメインに参加しているシステムで実行されるアプリケーション。 この場合は、「特権のアカウント」は、Active Directory で、最も特権のグループのメンバーであるアカウントだけでなく、委任された権限があるアカウントと権限の管理タスクを実行できるようにするを参照します。  
  
これらのアカウントには、ヘルプ デスクのアカウントのほとんどの DNS レコードと、ゾーンの管理に使用されるアカウント、または構成管理のために使用されるアカウントのドメインでは、ユーザーのパスワードをリセットすることができる可能性があります。 セキュリティで保護された管理ホストは専用の管理機能、および Microsoft Office などの電子メール アプリケーション、web ブラウザーや生産性ソフトウェアなどのソフトウェアを実行しないでください。  
  
「最も特権」のアカウントとグループが最も厳密に保護されたそれに応じて必要がありますが、アカウントとグループ アカウントを付与されている以上の標準ユーザー特権を保護する必要があるこれはありません。  
  
セキュリティで保護された管理ホストが、リモート デスクトップ ゲートウェイ サーバーの役割を実行するメンバー サーバーの管理タスクにのみ使用される専用のワークステーションをして IT ユーザーには、宛先ホスト、またはを実行するサーバーの管理を実行する接続HYPER-V ロールし、管理タスクを使用するには、各 IT ユーザーの一意の仮想マシンを提供します。 多くの環境ですべての 3 つのアプローチの組み合わせを実装することがあります。  
  
セキュリティで保護された管理ホストを実装するには、計画と構成、組織のサイズ、管理作業、リスク選好度、および予算と整合性がある必要があります。 組織に適した管理戦略の開発で使用するための考慮事項とセキュリティで保護された管理ホストを実装するためのオプションがここで提供されます。  
  
## <a name="principles-for-creating-secure-administrative-hosts"></a>セキュリティで保護された管理ホストを作成するための原則  
攻撃からシステムを効果的に保護するには、いくつかの一般的な原則に収めることに注意してください。  
  
1.  信頼性の低いホスト (管理システムと同じレベルにセキュリティ保護されていないワークステーション) から信頼されたシステム (ドメイン コント ローラーなどセキュリティで保護されたサーバー) を管理する必要があることはありません。  
  
2.  依存しないようにして単一の認証要素に特権を持つアクティビティを実行するときにユーザー名とパスワードの組み合わせは見なされない認証 (ユーザーの知識) 単一要素のみが表されるためです。 資格情報を生成しキャッシュまたは管理シナリオに格納する場所を考慮する必要があります。  
  
3.  現在の脅威の状況でほとんどの攻撃は、マルウェアや悪意のあるハッキングを利用して、、物理的なセキュリティを設計してセキュリティで保護された管理ホストを実装する場合を省略することはできません。  
  
### <a name="account-configuration"></a>アカウントの構成  
組織が現在のスマート カードを使用しない場合でも、その権限のアカウントとセキュリティで保護された管理ホストの実装を検討してください。 管理ホストは、すべてのアカウント管理用のホストを含む Ou にリンクされている GPO の次の設定を変更することでスマート カード ログオンを必要とするように構成する必要があります。  
  
**コンピューターの構成 \ セキュリティ オプション \ 対話型ログオン:スマート カードが必要**  
  
この設定には、Active Directory 内の個々 のアカウントの構成に関係なく、スマート カードを使用するすべての対話型ログオンが必要です。  
  
のみで構成できますが、承認されたアカウントでログオンを許可するセキュリティで保護された管理用のホストを構成することも必要があります。  
  
**コンピューター \policies\windows settings \local セキュリティ settings \local policies \user Rights Assignment**  
  
これは、対話を許可 (および、適切で、リモート デスクトップ サービス)、セキュリティで保護された管理ホストの承認されたユーザーにのみログオン権限。  
  
### <a name="physical-security"></a>物理的なセキュリティ  
信頼できると見なされるホストの管理、それらを構成し、管理システムと同じレベルに保護されています。 提供される推奨事項のほとんど[攻撃からドメイン コント ローラーのセキュリティで保護する](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)はドメイン コント ローラーと AD DS データベースの管理に使用するホストにも適用されます。 セキュリティで保護された管理システムを実装するほとんどの環境での課題の 1 つは、物理的なセキュリティがこれらのコンピューターは、多くの場合、サーバーなどのデータ センターでホストされている場合ほど安全でない領域に存在するために実装することが難しくなること管理ユーザーのデスクトップにします。  
  
物理的なセキュリティには、管理ホストの物理アクセス制御が含まれています。 小規模な組織では、オフィスや使用中でないときに、机の引き出し内は保持されている専用管理ワークステーションでロックを保持することがあります。 または、Active Directory またはドメイン コント ローラーの管理を実行する必要がある場合にログオンするドメイン コント ローラー直接する可能性があります。  
  
中規模の組織では、セキュリティで保護された管理「ジャンプ サーバー」の実装を検討可能性がありますをオフィスにセキュリティで保護された場所にあるし、Active Directory またはドメイン コント ローラーの管理が必要なときに使用されます。 ジャンプ サーバーの有無は使用しないときは、安全な場所にロックされている管理ワークステーションを実装することも可能性があります。  
  
大規模な組織では、Active Directory は; を厳密に制御されたアクセスを提供するデータ センターに格納されているジャンプ サーバーを展開することができます。ドメイン コント ローラーファイル、印刷、またはアプリケーション サーバー。 ジャンプ サーバー アーキテクチャの実装は、最も可能性の高い大規模な環境でセキュリティで保護されたワークステーションとサーバーの組み合わせを含めるは。  
  
組織の規模や管理、ホストのデザインに関係なくに対する未承認のアクセスや盗難、物理コンピューターをセキュリティで保護する必要があり。 の暗号化し、保護の管理用のホスト上のドライブに BitLocker ドライブ暗号化を使用する必要があります. 管理ホスト上に BitLocker を実装する場合でも、ホストが盗まれたまたは、そのディスクが削除されると、により、ドライブ上のデータが未承認のユーザーにアクセスできないこと。  
  
### <a name="operating-system-versions-and-configuration"></a>オペレーティング システムのバージョンと構成  
すべての管理ホスト サーバーまたはワークステーションでは、実行かどうか、最新のオペレーティング システムでは、このドキュメントで既に説明した理由から、組織で使用します。 現在のオペレーティング システムを実行して、管理スタッフは新しいセキュリティ機能、完全なベンダーのサポート、およびオペレーティング システムで導入された追加の機能からメリットがあります。 さらに、管理する最初のホストを展開して、新しいオペレーティング システムを評価するときは必要がありますの新機能、設定、および計画で利用できる、その後、その管理メカニズムを理解するにはオペレーティング システムのより広範囲に展開します。 は、組織の最も高度なユーザーに新しいオペレーティング システムについてよく理解しサポートするように最適な位置指定であるユーザーがあります。  
  
### <a name="microsoft-security-configuration-wizard"></a>Microsoft セキュリティの構成ウィザード  
ホストの管理戦略の一環としてジャンプ サーバーを実装する場合は、サービス、レジストリ、監査、およびサーバーの攻撃対象領域を削減するファイアウォールの設定を構成する、組み込みのセキュリティ構成ウィザードを使用する必要があります。 セキュリティの構成ウィザードの構成設定を収集し、構成されているときに、設定がすべてジャンプ サーバー上で一定のベースライン構成を適用するために使用する GPO を変換できます。 ジャンプ サーバーに設定固有のセキュリティを実装するために GPO をさらに編集することができ、すべての Microsoft Security Compliance Manager から抽出された追加のベースライン設定と設定を組み合わせることができます。  
  
### <a name="microsoft-security-compliance-manager"></a>Microsoft Security Compliance Manager  
[Microsoft Security Compliance Manager](https://technet.microsoft.com/library/cc677002.aspx)でそれらを収集しますは、オペレーティング システムのバージョンとの役割の構成に基づき、マイクロソフトが推奨するセキュリティ構成を統合する自由に利用できるツールであり、1 つのツールと UI を作成し、ドメイン コント ローラーのベースライン セキュリティ設定を構成するために使用できます。 Microsoft セキュリティ コンプライアンス マネージャーのテンプレートは、ジャンプ サーバーがデプロイおよびどのジャンプ サーバーを Ou に配置された Gpo を適用するための包括的な構成基準を生成するためにセキュリティの構成ウィザードの設定と組み合わせることができます。Active Directory に存在します。  
  
> [!NOTE]  
> この執筆時点で、Microsoft セキュリティ コンプライアンス マネージャーにジャンプ サーバーまたはその他のセキュリティで保護された管理ホストに固有の設定は含まれませんが、セキュリティ コンプライアンス マネージャー (SCM) は、管理の初期の基準を作成するも使用できます。ホスト。 ただし、ホストを適切に保護するには、高いセキュリティで保護されたワークステーションとサーバーに適切な追加のセキュリティ設定を適用してください。  
  
### <a name="applocker"></a>AppLocker  
管理用のホストと仮想 machinesshould は、スクリプト、ツール、および AppLocker またはサードパーティ製のアプリケーションの制限のソフトウェアを使用してアプリケーションのホワイト リストを構成します。 すべての管理アプリケーションまたはユーティリティでのセキュリティ設定に準拠していないする必要がありますアップグレードまたはセキュリティで保護された開発と管理のプラクティスに準拠したツールに置き換えられます。 新しいまたは追加のツールが必要なく、管理ホストでアプリケーションおよびユーティリティが徹底的にテストする、およびツールが管理ホストに配置する適切な場合は、システムのホワイト リストに追加できます。  
  
### <a name="rdp-restrictions"></a>RDP の制限  
特定の構成は、管理システムのアーキテクチャによって異なりますが、制限をアカウントとコンピューターを管理対象のシステムへのリモート デスクトップ プロトコル (RDP) 接続を確立するために使用できるを含める必要があります。リモート デスクトップ ゲートウェイ (RD ゲートウェイ) を使用するなど、ドメイン コント ローラーへのアクセスと権限のあるユーザーやシステムからその他の管理対象システムを制御するサーバーを移動します。  
  
必要があります、許可されたユーザーの対話型ログオンを許可してする必要がありますを削除またはでもブロックしないサーバーへのアクセスのために必要なその他のログオンの種類。  
  
### <a name="patch-and-configuration-management"></a>修正プログラムと構成の管理  
小規模な組織が Windows Update などの製品に依存または[Windows Server Update Services](https://technet.microsoft.com/windowsserver/bb332157)大規模な組織がエンタープライズ修正プログラムを実装中に、Windows システムに更新プログラムの展開を管理するには、(WSUS) と管理ソフトウェアなど、System Center Configuration Manager を構成します。 一般的なサーバーやワークステーション ユーザーに更新プログラムの展開に使用するメカニズムに関係なく、個別のデプロイメントをドメイン コント ローラー、証明機関、および管理用のホストなどの高度なセキュリティ システムを検討してください。 全般的な管理インフラストラクチャからこれらのシステムを隔離することによって、管理ソフトウェアまたはサービス アカウントが侵害された場合、侵害簡単に拡張できません、インフラストラクチャ内の最も安全なシステムに。  
  
セキュリティで保護されたシステムの更新プログラムの手動プロセスを実装しないでください、セキュリティで保護されたシステムの更新に個別のインフラストラクチャを構成する必要があります。 非常に大規模な組織であってもにするこのインフラストラクチャのセキュリティで保護されたシステム専用の WSUS サーバーと Gpo を使用して、通常、実装できます。  
  
### <a name="blocking-internet-access"></a>インターネット アクセスをブロックします。  
管理用のホストをインターネットへのアクセスを許可しない必要がありますも、組織のイントラネットを参照できます。 Web ブラウザーと同様のアプリケーションを管理ホストで許可されませんする必要があります。 境界ファイアウォールの設定、WFAS 構成、およびセキュリティで保護されたホスト上の「ブラック_ホール」プロキシ構成の組み合わせを使用してセキュリティで保護されたホストのインターネットへのアクセスをブロックできます。 Web ブラウザーが管理ホストで使用されていることを防ぐために、アプリケーションのホワイト リストを使用することもできます。  
  
### <a name="virtualization"></a>仮想化  
可能であれば、仮想マシンを管理ホストとしての実装を検討してください。 仮想化を使用して、システムを作成できますユーザーごとの管理を簡単にシャット ダウンできる場合に、使用中でないと一元的には格納され管理されている資格情報が残っていないこと active 管理システムのことを確認します。 管理用の仮想ホスト リセットされる初期スナップショットを使用後に仮想マシンが初期状態であることを確認要求することもできます。 管理ホストの仮想化のためのオプションの詳細については、次のセクションで提供されます。  
  
## <a name="sample-approaches-to-implementing-secure-administrative-hosts"></a>実装する方法のサンプルには、管理ホストがセキュリティで保護します。  
設計方法と、ホストの管理インフラストラクチャを展開に関係なくおく必要がありますに注意してくださいこのトピックの「"の原則を作成するセキュリティで保護された管理ホストの"で説明するガイドライン。 各ここで説明したアプローチは、[管理] と、IT スタッフで使用される「生産性」システムを分離する方法に関する一般的な情報を提供します。 生産性のシステムは、電子メールを確認したり、インターネットを参照し、Microsoft Office などの一般的な生産性向上ソフトウェアを使用する IT 管理者が採用しているコンピューターです。 管理システムは、セキュリティを強化して、IT 環境の日々 の管理に使用する専用です。  
  
セキュリティで保護された管理ホストを実装する最も簡単な方法は、元の管理タスクを実行できるセキュリティで保護されたワークステーションを使用した、IT スタッフを提供することです。 ワークステーションのみの実装では、各管理ワークステーションが管理ツールと管理サーバーとその他のインフラストラクチャへの RDP 接続を起動するために使用します。 ワークステーションのみの実装は有効である小規模の組織が管理ホストを専用の管理サーバーとワークステーションを使用すると、分散設計から大規模でより複雑なインフラストラクチャが挙げられますとしてこのトピックの「「を実装するセキュリティで保護された管理ワークステーションとジャンプ サーバー」で説明します。  
  
### <a name="implementing-separate-physical-workstations"></a>別個の物理ワークステーションを実装します。  
管理用のホストを実装できることを 1 つの方法は、IT ユーザーごとに 2 台のワークステーションを発行するためです。 1 台のワークステーションは、2 つ目のワークステーションが管理機能を専用に、生産性アプリケーションを使用して電子メールのチェックなどのアクティビティを実行する「通常」のユーザー アカウントで使用されます。  
  
生産性ワークステーションのセキュリティ保護されていないコンピューターにログオンする権限を持つアカウントを使用するのではなく、通常のユーザー アカウント、IT スタッフを指定できます。 管理ワークステーションには厳密に制御された構成を構成して、IT スタッフは、別のアカウントを使用して管理ワークステーションにログオンする必要があります。  
  
スマート カードを実装している場合は、管理ワークステーションは、スマート カードによるログオンを必要とするように構成する必要があり、IT スタッフは、対話型ログオンにスマート カードを要求するように構成することも、管理の使用の個別のアカウント与える必要があります。 管理ホスト セキュリティを強化した前述のようにする管理ワークステーションにローカルでログオンする IT の指定されたユーザーのみを許可する必要があります。  
  
#### <a name="pros"></a>長所  
別の物理システムを実装すると、そのロールの各コンピューターが適切に構成して、IT ユーザーがリスクを管理システムに公開できません。 誤ってを保証できます。  
  
#### <a name="cons"></a>短所  
  
-   別々 の物理コンピューターを実装すると、ハードウェアのコストが増加します。  
  
-   リモート システムの管理に使用される資格情報を持つ物理コンピューターにログオンしているメモリ内の資格情報をキャッシュします。  
  
-   管理ワークステーションが安全に格納されていない場合、物理ハードウェア キー ロガーやその他の物理的な攻撃などのメカニズムを使用して侵害受ける可能性があります。  
  
### <a name="implementing-a-secure-physical-workstation-with-a-virtualized-productivity-workstation"></a>仮想化された生産性ワークステーションを使用してセキュリティで保護された物理ワークステーションを実装します。  
この方法で、IT ユーザーは、特定の責任には、そのスコープ内でリモート サーバー管理ツール (RSAT) またはサーバーへの RDP 接続を使用して、日常の管理機能を実行できるセキュリティで保護された管理ワークステーションが付与されます。 IT ユーザーは、生産性のタスクを実行する必要があります、仮想マシンとして実行されているリモート生産性ワークステーションに RDP 経由で接続できます。 ワークステーションごとに個別の資格情報を使用する必要があり、スマート カードなどのコントロールを実装する必要があります。  
  
#### <a name="pros"></a>長所  
  
-   管理ワークステーションと生産性ワークステーションは区切られます。  
  
-   生産性ワークステーションへの接続をセキュリティで保護されたワークステーションを使用して、IT スタッフは、個別の資格情報と、スマート カードを使用でき、特権的な資格情報は安全性の低いコンピューターでは格納されません。  
  
#### <a name="cons"></a>短所  
  
-   ソリューションを実装するには、設計と実装の作業、および信頼性の高い仮想化のオプションが必要です。  
  
-   物理ワークステーションが安全に格納されていない場合、ハードウェアまたはオペレーティング システムを侵害し、通信の傍受を受けやすくための物理的な攻撃に対する脆弱性があります。  
  
### <a name="implementing-a-single-secure-workstation-with-connections-to-separate-productivity-and-administrative-virtual-machines"></a>「生産性」と「管理」の仮想マシンを個別に接続している 1 つのセキュリティで保護されたワークステーションを実装します。  
この方法では、IT ユーザーに 1 台の物理ワークステーションをロックダウン前述したようとを IT ユーザーは特権アクセスを発行できます。 電子メールおよびその他の生産性アプリケーションを実行する 1 つの仮想マシンと、ユーザーのとして構成されている 2 番目の仮想マシンに IT スタッフを提供する、専用のサーバーでホストされているバーチャル マシンへのリモート デスクトップ サービス接続を提供できます。専用管理ホスト。  
  
必要がありますが必要なスマート カードまたはその他の多要素ログオン仮想マシンの場合、物理コンピューターにログオンに使用されるアカウント以外の別のアカウントを使用します。 ユーザーが IT が物理コンピューターにログオンした後、生産性をリモート コンピューターと別のアカウントと、リモート管理コンピューターに接続するためのスマート カードに接続するユーザーの生産性のスマート カードを使用できます。  
  
#### <a name="pros"></a>長所  
  
-   IT ユーザーには、1 台の物理ワークステーションを使用できます。  
  
-   仮想ホストと仮想マシンにリモート デスクトップ サービス接続を使用して個別のアカウントが必要なによって IT ユーザーの資格情報は、ローカル コンピューター上のメモリにキャッシュされません。  
  
-   ローカル コンピューターのセキュリティ侵害の可能性を減少させ、管理用のホストとして同じ程度には、物理ホストを保護できます。  
  
-   これで、IT ユーザーの生産性の仮想マシンまたは管理、仮想マシンが侵害された場合、仮想マシンを「正常」状態にリセット簡単にできます。  
  
-   物理コンピューターが侵害された場合、メモリ内での特権的な資格情報がキャッシュされず、スマート カードの使用は、キーストローク ロガーで資格情報の侵害を防止できます。  
  
#### <a name="cons"></a>短所  
  
-   ソリューションを実装するには、設計と実装の作業、および信頼性の高い仮想化のオプションが必要です。  
  
-   物理ワークステーションが安全に格納されていない場合、ハードウェアまたはオペレーティング システムを侵害し、通信の傍受を受けやすくための物理的な攻撃に対する脆弱性があります。  
  
### <a name="implementing-secure-administrative-workstations-and-jump-servers"></a>セキュリティで保護された管理ワークステーションとジャンプ サーバーを実装します。  
管理ワークステーションは、セキュリティで保護する代替手段として、またはそれらと組み合わせて、セキュリティで保護されたジャンプ サーバーを実装して、管理ユーザーが RDP とスマート カードを使用して、管理タスクを実行するジャンプ サーバーに接続できます。  
  
ジャンプ サーバーは、ジャンプ サーバーと移行先サーバーから管理される接続の制限を実装することを許可するリモート デスクトップ ゲートウェイのロールを実行するように構成する必要があります。 可能な場合も、HYPER-V の役割をインストールし、作成[個人用仮想デスクトップ](https://technet.microsoft.com/library/dd759174.aspx)またはジャンプ サーバー上のタスクを使用する管理ユーザーの他のユーザーごとの仮想マシン。  
  
ジャンプ サーバーで管理ユーザー、ユーザーごとの仮想マシンを指定して、管理用のワークステーションの物理的なセキュリティを指定して、管理ユーザーがリセットまたは使用しないときは、仮想マシンをシャット ダウンできます。 同じ管理ホストで HYPER-V の役割とリモート デスクトップ ゲートウェイの役割をインストールしない場合は、別のコンピューターにインストールできます。  
  
可能な場合は、サーバーを管理するリモート管理ツールを使用してください。 ユーザーがバーチャル マシン (またはジャンプ サーバー管理用のユーザーごとの仮想マシンを実装していない場合) にリモート サーバー管理ツール (RSAT) 機能をインストールする必要があり、管理スタッフに RDP 経由で接続する必要があります、管理タスクを実行する仮想マシン。  
  
場合を直接管理する移行先サーバーに管理ユーザーが RDP 経由で接続する必要がありますと RD ゲートウェイを構成する適切なユーザーとコンピューターが、変換先への接続を確立するために使用される場合にのみ行わへの接続を許可します。サーバー。 実行、管理システムが指定されていないシステムでツールを禁止するか RSAT の (または同等) など、一般に使用するワークステーションとメンバ サーバーであるジャンプ サーバーがありません。  
  
#### <a name="pros"></a>長所  
  
-   ジャンプ サーバーを作成すると、"zones"(同様の構成、接続、およびセキュリティ要件を持つシステムのコレクション)、ネットワーク内に特定のサーバーをマップして、管理スタッフによる各ゾーンの管理を実現することが必要です。指定された"zone"サーバーへのセキュリティで保護された管理ホストから接続します。  
  
-   ジャンプ サーバーをゾーンに対応付けると、接続プロパティおよび構成の要件の詳細なコントロールを実装することができ、承認されていないシステムからの接続試行を簡単に特定できます。  
  
-   管理者 1 人あたりの仮想マシンをジャンプ サーバーに実装すると、シャット ダウンし、管理タスクが完了したときに、既知のクリーンな状態に仮想マシンのリセットを強制します。 管理タスクが完了したときに、仮想マシンのシャット ダウン (または再起動) を適用することで、仮想マシンは、攻撃者の対象となることはできませんも、メモリにキャッシュされた資格情報は、再起動を超える無効になるために、資格情報盗難攻撃可能です。  
  
#### <a name="cons"></a>短所  
  
-   専用サーバーは、物理または仮想かどうかにジャンプ サーバー、必要があります。  
  
-   ジャンプ サーバーの指定を実装して、管理ワークステーションは、慎重な計画と構成環境で構成されている任意のセキュリティ ゾーンにマップする必要があります。  
  


