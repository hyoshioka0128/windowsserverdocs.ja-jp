---
title: クラスターとプールのクォーラムを理解します。
description: 複雑な作業を経由する具体的な例では、クラスターとプールのクォーラムを理解すること。
keywords: 記憶域スペース ダイレクト、クォーラム、ミラーリング監視サーバー、S2D では、クラスター クォーラム、プールのクォーラム、クラスターでは、プール
ms.prod: windows-server-threshold
ms.author: adagashe
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 30958b8b1e8b0009626509409d1f031611c76a20
ms.sourcegitcommit: fe621b72d45d0259bac1d5b9031deed3dcbed29d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2019
ms.locfileid: "66455432"
---
# <a name="understanding-cluster-and-pool-quorum"></a>クラスターとプールのクォーラムを理解します。

>適用対象:Windows Server 2019、Windows Server 2016

[Windows Server フェールオーバー クラスタ リング](../../failover-clustering/failover-clustering-overview.md)ワークロードの高可用性を提供します。 これらのリソースはリソースをホストするノードが稼働; 場合は、高可用性と見なされますただし、クラスター一般には、半分以上のノードが実行されているとも呼ばれ*クォーラム*します。

クォーラムを防ぐために設計されています。*スプリット ブレイン*シナリオは、ネットワークのパーティションとノードのサブセットが互いと通信できないときに発生することができます。 ワークロードを所有し、多くの問題につながる可能性の同じディスクに書き込むしようとするノードの両方のサブセットがある可能性があります。 ただし、これらのグループのため、これらのグループの 1 つだけがオンラインのまま実行を続行するノードの 1 つだけを強制クォーラムのフェールオーバー クラスタ リングの概念では禁止します。

クォーラムは、クラスターが残っているオンライン中に維持できるエラーの数を決定します。 クォーラムは、複数のサーバーを同時に、リソース グループをホストし、同時に同じディスクに書き込むくださいようにサブセットのクラスター ノードの間の通信に問題がある場合に、シナリオを処理するために設計されています。 このクォーラムの概念をさせて、クラスターはクラスター サービスが特定のリソース グループの 1 つだけの場合は true。 所有者があることを確認するノードのサブセットのいずれかで停止するを強制します。 停止しているノードは、ノードのメインのグループと通信できるもう一度とクラスターに再度参加し、クラスター サービスを開始しますが、自動的に。

Windows Server 2019 および Windows Server 2016 では、独自のメカニズムのクォーラムがあるシステムの 2 つのコンポーネントがあります。

- **クラスターのクォーラム**:クラスター レベルで動作し (つまりノードが失われるしてクラスターを入手できます)
- **プールのクォーラム**:記憶域スペース ダイレクトが有効な場合に、プール レベルで動作し (つまりノードおよびドライブが失われるしてプールを入手できます)。 記憶域プールがクラスター化および非クラスター化の両方のシナリオで使用するために設計されてさまざまなクォーラムがあるためにです。

## <a name="cluster-quorum-overview"></a>クラスター クォーラムの概要

次の表では、シナリオごとのクラスター クォーラムの結果の概要します。

| サーバー ノード | 1 つのサーバー ノードの障害を切り抜ける | 1 つのサーバー ノードの障害、その後別にあっても存続できます。 | 2 つの同時サーバー ノードの障害を切り抜ける |
|--------------|-------------------------------------|---------------------------------------------------|----------------------------------------------------|
| 2            | 50/50                               | X                                                | X                                                 |
| 2 + ミラーリング監視サーバー  | 〇                                 | X                                                | X                                                 |
| 3            | 〇                                 | 50/50                                             | X                                                 |
| 3 + ミラーリング監視サーバー  | 〇                                 | 〇                                               | X                                                 |
| 4            | 〇                                 | 〇                                               | 50/50                                              |
| 4 + ミラーリング監視サーバー  | 〇                                 | 〇                                               | 〇                                                |
| 5 以降  | 〇                                 | 〇                                               | 〇                                                |

### <a name="cluster-quorum-recommendations"></a>クラスター クォーラムの推奨事項

- ミラーリング監視サーバーは、2 つのノードがあれば、**必要**します。
- ミラーリング監視サーバーは、次の 3 つまたは 4 つのノードがあれば、**強くお勧めします**します。
- 使用して、インターネットにアクセスした場合、 **[クラウド ミラーリング監視サーバー](../../failover-clustering/deploy-cloud-witness.md)**
- 他のマシンのファイル共有と IT 環境の場合は、ファイル共有監視を使用して、

## <a name="how-cluster-quorum-works"></a>クラスター クォーラムのしくみ

稼働しているノードが該当することを確認する必要がありますノードが失敗したときに、またはノードのサブセットが別のサブセットとの接続を失ったとき、*マジョリティ*オンラインのままに、クラスターの。 確認することはできませんと、それらがオフラインにします。

概念が、*マジョリティ*のみは正常にクラスター内のノードの合計数が奇数 (たとえば、5 つのノード クラスター内の 3 つのノード)。 そのため、クラスター ノード (たとえば、4 ノード クラスター) の数が偶数の詳細について何か。

クラスターを作成できる 2 つの方法がある、*合計投票数*奇数。

1. まず、できます*を*を追加して 1 つ、*ミラーリング監視サーバー*余分な投票で。 これには、ユーザー設定が必要です。
2.  または、移動、*ダウン*(必要に応じて自動的に行われます)、1 つの復旧を開始ノードの投票をゼロが 1 つ。

残っているノードが正常にされるたびにいることを確認、*マジョリティ*の定義*マジョリティ*残存オブジェクトだけに存在するように更新します。 これにより、1 つのノード、失われるなど、クラスターができます。 この概念の*合計投票数*と呼ばれる、連続する障害の後に適合させる***動的なクォーラム***します。  

### <a name="dynamic-witness"></a>動的なミラーリング監視サーバー

動的なミラーリング監視サーバーは、ことを確認する、ミラーリング監視の投票を切り替えます、*合計投票数*が奇数です。 投票の数が奇数の場合は、ミラーリング監視サーバーに、投票はありません。 投票数が偶数の場合、ミラーリング監視サーバーも票を持ちます。 動的なミラーリング監視サーバーは、ミラーリング監視サーバーの障害が原因でクラスターをダウンするリスクを大幅に短縮します。 クラスターは、クラスターで使用可能な投票ノード数に基づいて監視の投票を使用するかどうかを決定します。

動的なクォーラムは、以下に示すように動的にミラーリング監視サーバーで動作します。

### <a name="dynamic-quorum-behavior"></a>動的なクォーラムの動作

- ある場合、**でも**ノードと、ミラーリング監視サーバーなしの数値*1 つのノードの投票をゼロに設定を取得する*します。 たとえば、4 つのノードのうち 3 が投票数を取得ため、*合計投票数*は、3 と投票の 2 つの残存オブジェクトの大部分と見なされます。
- ある場合、**奇数**ノードと、ミラーリング監視サーバーなしの数値*投票を取得*します。
- ある場合、**でも**個のノードとミラーリング監視サーバーの *、ミラーリング監視の投票の*で合計が奇数であるため、します。
- ある場合、**奇数**個のノードとミラーリング監視サーバーの*ミラーリング監視サーバーは投票*します。

動的なクォーラム ノード クラスターを 1 つのノード (最後 man 継続と呼ばれます) で実行を許可して、過半数の投票が失われないようにするには、動的に投票を割り当てる機能を使用できます。 例として、4 ノード クラスターを見てみましょう。 クォーラムの 3 つの投票を必要とします。 

この場合、クラスターがダウンした 2 つのノードが失われた場合。

![ダイアグラムが表示された 4 つのクラスター ノードの投票を取得します](media/understand-quorum/dynamic-quorum-base.png)

ただし、動的なクォーラムによりこれが発生します。 *合計投票数*必要なクォーラムが使用可能なノードの数に基づいて決定されますようになりました。 そのため、動的クォーラムは、3 つのノードが失われる場合でも、クラスターをとどまります。

![失敗して、各エラーの後に調整する必要の投票の数は、一度に 1 つのノードで、次の 4 つのクラスター ノードを示す図。](media/understand-quorum/dynamic-quorum-step-through.png)

上記のシナリオは、記憶域スペース ダイレクトを有効にしないが一般的なクラスターに適用されます。 ただし、記憶域スペース ダイレクトが有効な場合、クラスターのみをサポートできます 2 つのノードの障害。 より詳細については、[プールのクォーラム セクション](#pool-quorum-overview)します。

### <a name="examples"></a>例

#### <a name="two-nodes-without-a-witness"></a>ミラーリング監視サーバーなしの 2 つのノード。 
1 つのノードの投票を 0 にため、*マジョリティ*投票がの全体の中から決定**1 投票**。 非投票ノードが予期せずがダウンした場合、保持するが 1/1 とクラスターは存続します。 投票ノードが予期せずがダウンした場合、保持する、0/1 と、クラスターがダウンしました。 投票ノードの電源が適切に、投票は、その他のノードに転送し、クラスターは存続します。 ***これは、ため、ミラーリング監視サーバーを構成することが重要です。***

![クォーラムの場合は、ミラーリング監視サーバーなしの 2 つのノードの説明](media/understand-quorum/2-node-no-witness.png)

- 1 つのサーバー エラーがあっても存続できます。**50% の確率**します。
- 1 つのサーバーが故障し、別に存続できます。**No**:
- 2 つのサーバーの障害を一度に存続することができます。**No**: 

#### <a name="two-nodes-with-a-witness"></a>ミラーリング監視サーバーと 2 つのノード。 
両方のノードが投票し、投票のミラーリング監視サーバーであり、*マジョリティ*の全体の中から決定されます**3 票**します。 いずれかのノードがダウンした場合、保持するが 2/3 とクラスターは存続します。

![ミラーリング監視サーバーと 2 つのノードのケースで説明されているクォーラム](media/understand-quorum/2-node-witness.png)

- 1 つのサーバー エラーがあっても存続できます。**Yes**。
- 1 つのサーバーが故障し、別に存続できます。**No**:
- 2 つのサーバーの障害を一度に存続することができます。**No**: 

#### <a name="three-nodes-without-a-witness"></a>ミラーリング監視サーバーなしの 3 つのノード。
すべてのノードの投票はそのため、*マジョリティ*の全体の中から決定されます**3 票**します。 任意のノードがダウンした場合は、残存オブジェクトは 2/3 あり、クラスターが存続します。 クラスターが、ミラーリング監視サーバーなしの 2 つのノードになります-シナリオ 1 の中の時点では、します。

![クォーラムの場合は、ミラーリング監視サーバーなしの 3 つのノードの説明](media/understand-quorum/3-node-no-witness.png)

- 1 つのサーバー エラーがあっても存続できます。**Yes**。
- 1 つのサーバーが故障し、別に存続できます。**50% の確率**します。
- 2 つのサーバーの障害を一度に存続することができます。**No**: 

#### <a name="three-nodes-with-a-witness"></a>ミラーリング監視サーバーの 3 つのノード。
ミラーリング監視サーバーは投票が最初に、すべてのノードが投票します。 *マジョリティ*の全体の中から決定**3 票**します。 1 つの障害の後は、ミラーリング監視サーバー-シナリオ 2 には 2 つのノードがクラスターには、します。 そのため、ここで 2 つのノードとミラーリング監視サーバー票を投じます。

![ミラーリング監視サーバーの 3 つのノードのケースで説明されているクォーラム](media/understand-quorum/3-node-witness.png)

- 1 つのサーバー エラーがあっても存続できます。**Yes**。
- 1 つのサーバーが故障し、別に存続できます。**Yes**。
- 2 つのサーバーの障害を一度に存続することができます。**No**: 

#### <a name="four-nodes-without-a-witness"></a>ミラーリング監視サーバーなしの 4 つのノード
1 つのノードの投票を 0 に設定されるため、*マジョリティ*の全体の中から決定されます**3 票**します。 1 つの障害の後、クラスターが 3 つのノードになり、シナリオ 3 にしています。

![クォーラムの場合は、ミラーリング監視サーバーなしの 4 つのノードの説明](media/understand-quorum/4-node-no-witness.png)

- 1 つのサーバー エラーがあっても存続できます。**Yes**。
- 1 つのサーバーが故障し、別に存続できます。**Yes**。
- 2 つのサーバーの障害を一度に存続することができます。**50% の確率**します。 

#### <a name="four-nodes-with-a-witness"></a>ミラーリング監視サーバーで 4 つのノード。
すべてのノードの投票と、ミラーリング監視の投票数ため、*マジョリティ*の全体の中から決定**5 票**します。 1 つの障害が発生したシナリオ 4 でできました。 2 つの同時障害の後に、シナリオ 2 までスキップします。

![ミラーリング監視サーバーで 4 つのノードのケースで説明されているクォーラム](media/understand-quorum/4-node-witness.png)

- 1 つのサーバー エラーがあっても存続できます。**Yes**。
- 1 つのサーバーが故障し、別に存続できます。**Yes**。
- 2 つのサーバーの障害を一度に存続することができます。**Yes**。 

#### <a name="five-nodes-and-beyond"></a>5 つのノードおよびそれ以降。
すべてのノードが投票、または、すべてが 1 つの投票、どのようなが奇数の合計を作成します。 記憶域スペース ダイレクトを処理できません以上の 2 つのノードをこの時点では、ミラーリング監視サーバーがないため必要または有効。

![以降では、5 つのノードのケースで説明されているクォーラム](media/understand-quorum/5-nodes.png)

- 1 つのサーバー エラーがあっても存続できます。**Yes**。
- 1 つのサーバーが故障し、別に存続できます。**Yes**。
- 2 つのサーバーの障害を一度に存続することができます。**Yes**。 

クォーラムのしくみを理解したら、次のミラーリング監視サーバーはクォーラムの種類を見てみましょう。

### <a name="quorum-witness-types"></a>クォーラム監視の種類

フェールオーバー クラスタ リングには、ミラーリング監視サーバーはクォーラムの 3 つの種類がサポートされます。

- **[クラウド監視](../../failover-clustering/deploy-cloud-witness.md)** -クラスターのすべてのノードがアクセスできる Azure のストレージの Blob。 クラスタ リングに関する情報を witness.log ファイルで管理しているが、クラスター データベースのコピーを格納しません。
- **ファイル共有監視の**– Windows Server を実行するファイル サーバーで構成されている、SMB ファイル共有。 クラスタ リングに関する情報を witness.log ファイルで管理しているが、クラスター データベースのコピーを格納しません。
- **ディスク監視**-クラスターの使用可能なストレージ グループ内にある少数のクラスター化されたディスク。 このディスクでは、高可用性と、ノード間のフェールオーバーを実行できます。 クラスター データベースのコピーが含まれています。  ***記憶域スペース ダイレクトのディスク監視はサポートされていません***します。

## <a name="pool-quorum-overview"></a>プールのクォーラムの概要

クラスター クォーラムは、クラスター レベルでの動作について説明しました。 ここで、プールのクォーラムは、プール レベル (つまり、ノードが失われる可能性がドライブし、が稼働してプール) の動作について詳しく見ていきます。 記憶域プールがクラスター化および非クラスター化の両方のシナリオで使用するために設計されてさまざまなクォーラムがあるためにです。

次の表では、シナリオごとのプールのクォーラムの結果の概要します。

| サーバー ノード | 1 つのサーバー ノードの障害を切り抜ける | 1 つのサーバー ノードの障害、その後別にあっても存続できます。 | 2 つの同時サーバー ノードの障害を切り抜ける |
|--------------|-------------------------------------|---------------------------------------------------|----------------------------------------------------|
| 2            | X                                  | いいえ                                                | X                                                 |
| 2 + ミラーリング監視サーバー  | 〇                                 | X                                                | X                                                 |
| 3            | 〇                                 | X                                                | X                                                 |
| 3 + ミラーリング監視サーバー  | 〇                                 | X                                                | X                                                 |
| 4            | 〇                                 | X                                                | X                                                 |
| 4 + ミラーリング監視サーバー  | 〇                                 | 〇                                               | 〇                                                |
| 5 以降  | 〇                                 | 〇                                               | 〇                                                |

## <a name="how-pool-quorum-works"></a>プールのクォーラムのしくみ

残りのドライブが該当することを確認する必要がありますドライブが失敗したときに、またはドライブのサブセットが別のサブセットとの接続を失ったとき、*マジョリティ*のオンラインのままにプールします。 確認することはできませんと、それらがオフラインにします。 プールがオフラインまたはオンライン状態に維持クォーラムには、十分なディスクがあるかどうかに基づいているエンティティ (50% + 1)。 プール リソース所有者 (アクティブなクラスター ノード) は +1 にできます。

プールのクォーラムが、次の方法でクラスターのクォーラムからと異なる方法で動作します。

- プールを使用して 1 つのノード クラスターのタイ ブレーカーとしてミラーリング監視サーバーとしても半分になったドライブ (プール リソース所有者になっているこのノード) の処理を
- プールには、動的なクォーラムはありません。
- プールは、投票を削除する独自のバージョンを実装していません

### <a name="examples"></a>例

#### <a name="four-nodes-with-a-symmetrical-layout"></a>対称的なレイアウトを持つ 4 つのノード。 
16 台のドライブの 1 つの投票、2 つのノードも 1 票 (プール リソース所有者のため)。 *マジョリティ*の全体の中から決定**16 投票**します。 3 と 4 つのノードがダウンした場合残りのサブセットでドライブが 8 と 9/16 の投票は、プールのリソースの所有者は、します。 そのため、プールは存続します。

![プールのクォーラム 1](media/understand-quorum/pool-1.png)

- 1 つのサーバー エラーがあっても存続できます。**Yes**。
- 1 つのサーバーが故障し、別に存続できます。**Yes**。
- 2 つのサーバーの障害を一度に存続することができます。**Yes**。 

#### <a name="four-nodes-with-a-symmetrical-layout-and-drive-failure"></a>対称的なレイアウトとドライブ エラーのため、4 つのノード。 
16 台のドライブの 1 つの投票、ノード 2 も 1 票 (プール リソース所有者のため)。 *マジョリティ*の全体の中から決定**16 投票**します。 最初に、ドライブ 7 がダウンをしました。 3 と 4 つのノードがダウンした場合 7 ドライブと 8/16 の投票は、プールのリソースの所有者、残っているサブセットでは、します。 そのため、プールは大部分がないし、がダウンしました。

![プールのクォーラム 2](media/understand-quorum/pool-2.png)

- 1 つのサーバー エラーがあっても存続できます。**Yes**。
- 1 つのサーバーが故障し、別に存続できます。**No**:
- 2 つのサーバーの障害を一度に存続することができます。**No**: 

#### <a name="four-nodes-with-a-non-symmetrical-layout"></a>非対称レイアウトを持つ 4 つのノード。 
24 台のドライブの 1 つの投票、2 つのノードも 1 票 (プール リソース所有者のため)。 *マジョリティ*の全体の中から決定**24 投票**します。 3 と 4 つのノードがダウンした場合残りのサブセットでドライブが 8 と 9 月 24 日の投票は、プールのリソースの所有者は、します。 そのため、プールは大部分がないし、がダウンしました。

![プールのクォーラム 3](media/understand-quorum/pool-3.png)

- 1 つのサーバー エラーがあっても存続できます。**Yes**。
- 1 つのサーバーが故障し、別にあっても存続できます。 * * 依存先 * * (3 および 4 の両方のノードがダウンが他のすべてのシナリオを切り抜けるで生き残ることはできません。
- 一度に 2 つのサーバーの障害を存続することができます。 * * 依存先 * * (3 および 4 の両方のノードがダウンが他のすべてのシナリオを切り抜けるで生き残ることはできません。

### <a name="pool-quorum-recommendations"></a>プールのクォーラムの推奨事項

- クラスター内の各ノードが対称的なことを確認します (各ノードには、同じ数のドライブ)
- ノードの障害に対応して、仮想ディスクをオンラインを維持できるように、3 方向ミラーまたはデュアル パリティを有効にします。 参照してください、[ボリューム ガイダンス ページ](plan-volumes.md)の詳細。
- 超える、下の 2 つのノードが 2 つのノードと別のノード上のディスクが下にある場合は、ボリューム、データの 3 つすべてのコピーへのアクセスがない可能性がありますしたがってとオフラインになり使用できません。 返されることは、サーバーまたはボリューム内のすべてのデータのほとんどの回復性を確認します。 すぐにディスクを置換することをお勧めします。

## <a name="more-information"></a>詳細情報

- [クォーラムを構成および管理する](../../failover-clustering/manage-cluster-quorum.md)
- [クラウド監視を展開します。](../../failover-clustering/deploy-cloud-witness.md)
