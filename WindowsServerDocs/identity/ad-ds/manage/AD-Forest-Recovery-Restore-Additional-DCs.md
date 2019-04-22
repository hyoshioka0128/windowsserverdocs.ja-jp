---
title: AD フォレストの回復の残りの Dc を再デプロイ
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: af9ec02a480b35e573edebcdd5928451174b6c1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812003"
---
# <a name="ad-forest-recovery---redeploy-remaining-dcs"></a>AD フォレストの回復の残りの Dc を再デプロイ

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

この時点までの手順のすべてのフォレストに適用されます。 ドメインごとに有効なバックアップを検索、分離ドメインの回復、再接続、グローバル カタログをリセットおよびクリーンアップします。 この次の手順では、フォレスト再デプロイします。 これを行う方法は、フォレストの設計、サービス レベル契約、サイト構造、使用可能な帯域幅、およびその他の多数の要因に大幅に異なります。 基本原則と、ビジネス要件に最適な方法で、このセクションの推奨事項に基づく独自の再展開計画を設計する必要があります。  
  
次の手順では、フォレストの回復を実施する前に存在していたすべての Dc 上で AD DS をインストールします。 Dc がまだ存在しない場合は、AD DS サービスは、強制的に削除する必要があります。 または Dc を再インストールすることができます。 フォレストの回復中に対応するメタデータが削除されているため、これらの Dc の既存のバックアップを再利用できません。 単純な環境でこの再デプロイ プロセスは、運用ネットワークに復旧された Dc を再接続して、必要に応じて新しい Dc を昇格する同じくらい簡単にできます。  
  
ある大企業は、世界中のインフラストラクチャに直面して、高度な計画が必要です。 最初のフェーズは; サービスとして AD を復元するには、通常戦略的にインストールすることを意味では、すべての重要なビジネス部門とアプリケーションのもう一度操作を開始するように Dc が配置されます。 これによってパフォーマンスが一時的に低下するブランチ オフィスの許容される場合があります。 2 つ目として、残りのすべてのフェーズと重要度の低い Dc を再デプロイします。  
  
 どちらも自動化すること、その他の Dc をインストールする 2 つの方法はあります。  
  
- 複製  
   - Windows Server 2012 を実行する仮想化環境で多数の Dc を回復する最も高速かつ最も簡単な方法は、複製。 バックアップから 1 つの仮想化 DC を復元した後は、ドメイン内のすべての仮想化 Dc の復旧を自動化できます。  
   - 複製と前提条件の詳細については、次を参照してください。 [Active Directory Domain Services (AD DS) Virtualization (Level 100) の概要](https://technet.microsoft.com/library/hh831734.aspx)します。  
- Windows Server 2012 (または Windows Server の以前のバージョンを実行するサーバーで Dcpromo.exe) を実行するサーバーで Windows PowerShell を使用して、またはユーザー インターフェイスを使用して、AD DS を再インストールします。  
   - AD DS を再インストールする時間を短縮するには、インストール中にレプリケーション トラフィックを減らすため、メディア (IFM) オプションからインストールを使用できます。 使用しての詳細については、 **ntdsutil ifm**インストール メディアを作成するコマンド[メディアから AD DS のインストール](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx)します。  

仮想化 DC の複製またはバックアップから復元する) ではなく AD DS をインストールすることによって、フォレストの回復は各レプリカ DC の次の点を検討してください。  
  
- DC の複製のソースとして使用されるすべてのソフトウェアを複製することがあります。 複製が開始される前に、アプリケーションとサービスを複製することはできませんを削除する必要があります。 方法が使用できない場合は、別の仮想化 DC をソースとして選択する必要があります。  
- 復元する最初の仮想化 DC の追加の仮想化 Dc を複製する場合、ソース DC は、VHDX ファイルのコピー中にシャット ダウンする必要があります。 複製仮想ドメイン コント ローラーが実行され、使用可能なをオンラインでする必要がありますし、最初に起動します。 シャット ダウンによってダウンタイムが最初の DC を回復したとして受け入れ可能でない場合は、複製のソースとして機能する AD DS をインストールすることによって追加の仮想化 DC をデプロイします。  
- 複製された仮想化ドメイン コント ローラーまたは AD DS をインストールするサーバーのホスト名の制限はありません。 新しいホスト名または使用されていたホスト名を使用することができます。 DNS ホスト名の構文の詳細については、次を参照してください。 [DNS コンピューター名の作成](https://technet.microsoft.com/library/cc785282.aspx)([https://go.microsoft.com/fwlink/?LinkId=74564](https://go.microsoft.com/fwlink/?LinkId=74564))。  
- ネットワーク アダプターの TCP/IP のプロパティに優先 DNS サーバーとして (最初のルート ドメインで復元された DC) のフォレスト内の最初の DNS サーバーでは、各サーバーを構成します。 詳細については、次を参照してください。 [DNS を使用するには、TCP/IP の構成](https://technet.microsoft.com/library/cc779282.aspx)します。  
- いくつかの Rodc が中央の場所にデプロイされている場合、仮想化の DC に複製することにより、または削除および分離配置されている場所で個別にデプロイされる場合は、AD DS を再インストールしてそれらを再構築、従来の方法で、ドメイン内のすべての Rodc を再デプロイします。ブランチ オフィスなど。  
   - Rodc を再構築により、残留オブジェクトが含まれていない、され、後で発生してから、レプリケーションの競合を防ぐのに役立ちます。 RODC から AD DS を削除すると*DC のメタデータを保持するオプションを選択して*します。 このオプションを使用して、RODC の krbtgt アカウントを保持および委任された RODC 管理者アカウントとパスワード レプリケーション ポリシー (PRP) のアクセス許可を保持し、Domain Admin 資格情報を使用して、削除してに AD DS を再インストールする必要があります。RODC します。 そこには、DNS サーバーとグローバル カタログの役割最初、RODC にインストールされている場合。  
   - ある可能性があります (Rodc または書き込み可能 Dc) の Dc を再構築する場合、再インストール時にレプリケーション トラフィックの増加します。 その影響を低減するには、RODC のインストールのスケジュールを調整することができ、インストールからメディア (IFM) オプションを使用することができます。 IFM オプションを使用する場合は、実行、 **ntdsutil ifm**コマンドの無料データが破損している、信頼されている書き込み可能 DC をします。 これは、AD DS の再インストールが完了した後に、RODC 上に表示されるから破損している可能性を回避できます。 IFM の詳細については、次を参照してください。[メディアから AD DS のインストール](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx)します。  
   - Rodc を再構築の詳細については、次を参照してください。 [RODC の削除と再インストール](https://technet.microsoft.com/library/cc835490\(WS.10\).aspx)します。  
- DC はフォレストの機能不全の前に、DNS サーバー サービスを実行していた場合は、インストールし、AD DS のインストール中に DNS サーバー サービスを構成します。 それ以外の場合、その他の DNS サーバーで、元の DNS クライアントを構成します。  
- 認証またはユーザーやアプリケーションのクエリ負荷を共有する他のグローバル カタログを必要とする場合は、仮想化 DC を複製する前に、ソースにグローバル カタログまたは、AD DS のインストール中に、DC をグローバル カタログ サーバーを行うことができますか、追加できます。  
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復 - 前提条件](AD-Forest-Recovery-Prerequisties.md)  
- [AD フォレストの回復 - カスタム フォレスト回復の計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD フォレストの回復の問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD フォレストの回復に回復する方法を決定](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD フォレストの回復 - 最初の回復を実行します。](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
- [AD フォレストの回復 - よく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
- [AD フォレストの回復 - Multidomain フォレスト内の 1 つのドメインを回復します。](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD フォレストの回復 - Windows Server 2003 ドメイン コント ローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md)
