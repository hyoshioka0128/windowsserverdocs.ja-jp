---
title: LDAP ADDS パフォーマンス チューニングに関する考慮事項
description: ワークロードに対応する Active Directory の LDAP の考慮事項
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 7ac9453159fe97dc15ecbb2ab858214664a2a197
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811527"
---
# <a name="ldap-considerations-in-adds-performance-tuning"></a>LDAP ADDS パフォーマンス チューニングに関する考慮事項

> [!IMPORTANT]
> サーバー ハードウェアでさらに詳しくは、「Active Directory ワークロードを最適化するためには、主な推奨事項と考慮事項概要次に、 [Active Directory Domain Services のキャパシティ プランニング](https://go.microsoft.com/fwlink/?LinkId=324566)記事。 リーダーは、確認を強くお勧め[Active Directory Domain Services のキャパシティ プランニング](https://go.microsoft.com/fwlink/?LinkId=324566)技術に関する理解を深めると、これらの推奨事項の影響。

## <a name="verify-ldap-queries"></a>LDAP クエリを確認します。

LDAP クエリを作成する効率的なクエリに関する推奨事項に準拠していることを確認します。

MSDN で正しく書き込み、構造、および Active Directory に対して使用するためのクエリを分析する方法についての広範なドキュメントがあります。 詳細については、次を参照してください。 [Creating More Efficient Microsoft Active Directory-Enabled アプリケーション](https://msdn.microsoft.com/library/ms808539.aspx)します。

## <a name="optimize-ldap-page-sizes"></a>LDAP ページ サイズを最適化します。

クライアントの要求に応答内の複数のオブジェクトで結果を返す、ドメイン コント ローラーはメモリ内の結果セットを一時的に保存するがします。 ページ サイズの増加により、多くのメモリ使用量と、キャッシュからアイテムを不必要に age ことができます。 この場合、既定の設定が最適です。 推奨事項がページ サイズの設定を増やすに行われたいくつかのシナリオがあります。 不適切なとして特定されていない限り、既定値を使用することをお勧めします。

クエリでは、多くの結果がある、同時に実行されると同様のクエリの制限が発生する可能性が。  これは、LDAP サーバーに cookie プールと呼ばれるグローバル メモリ領域が消費されますが、発生します。  説明したように、プールのサイズを大きく必要があります[LDAP サーバー Cookie の処理方法](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/manage/how-ldap-server-cookies-are-handled)します。

これらの設定を調整するには、次を参照してください。 [Windows Server 2008 以降のドメイン コント ローラーは、LDAP 応答でのみ 5000 の値を返します](https://support.microsoft.com/kb/2009267)します。

## <a name="determine-whether-to-add-indices"></a>インデックスを追加するかどうかを決定します。

インデックスの属性は、フィルターで属性名を持つオブジェクトを検索するときに役立ちます。 インデックス作成と、フィルターを評価するときにアクセスする必要がありますオブジェクトの数を減らすことができます。 ただし、このパフォーマンスを低下させる、書き込み操作の対応する属性を変更または追加時に、インデックスを更新する必要があります。 ただし、多くの場合、記憶域のコストを上回るメリットが、ディレクトリ データベースのサイズも増加します。 高価で非効率的なクエリを検索するのには、ログ記録を使用できます。 識別、対応するクエリで検索のパフォーマンスを向上させるために使用されるいくつかの属性のインデックス作成を検討してください。 Active Directory の検索の動作方法の詳細については、次を参照してください。 [Active Directory 検索のしくみ](https://technet.microsoft.com/library/cc755809.aspx)します。

### <a name="scenarios-that-benefit-in-adding-indices"></a>インデックスの追加の利点を得られるシナリオ

-   データを要求でクライアントの負荷が大幅な CPU 使用率を生成して、クライアント クエリの動作を変更または最適化できません。 負荷の高いでは、Server Performance Advisor または組み込み Active Directory データ コレクター セットの上位 10 悪影響を及ぼさないように一覧に示す自体は CPU の 1% 以上を使用してを検討してください。

-   クライアントの負荷がインデックスのない属性により、サーバーで大量のディスク I/O を生成して、クライアント クエリの動作を変更または最適化できません。

-   クエリでは、長い時間がかかると、カバーのインデックスの不足しているため、クライアントに、許容される時間が完了しません。

- 使用量と ATQ LDAP スレッドの枯渇、膨大な量の高い期間を持つクエリが原因となっています。 次のパフォーマンス カウンターを監視します。

    - **NTDS\\要求の待機時間**– 要求がプロセスにはどのくらいの期間の対象になります。 Active Directory が 120 秒 (既定) 後にタイムアウトになる要求、ただし、大部分がより速く実行する必要があり、全体的な数値に隠れてしまう極端に長いクエリを実行する必要があります。 絶対しきい値ではなくこの基準での変更を探します。

        > [!NOTE]
        > 値が大きい場合は、ここでは、その他のドメインと CRL チェックの「プロキシ」要求で遅延のインジケーターはこともできます。

    - **NTDS\\推定処理の遅延**– これが最適なパフォーマンスを 0 に近いする必要がありますが理想的です、これは、要求が提供されるを待機する時間をかけていないことを意味します。

これらのシナリオは、次の方法の 1 つ以上を使用して検出できます。

-   [統計情報のコントロールでのクエリのタイミングを決定します。](https://msdn.microsoft.com/library/ms808539.aspx)

-   [高価で非効率的な検索の追跡](https://msdn.microsoft.com/library/ms808539.aspx)

-   Active Directory の診断データ コレクター セットのパフォーマンス モニターで ([SPA の息子。AD データ コレクター設定 Win2008 以降](http://blogs.technet.com/b/askds/archive/2010/06/08/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond.aspx))

-   [Microsoft Server Performance Advisor](../../../server-performance-advisor/microsoft-server-performance-advisor.md) Active Directory Advisor パック

-   以外の任意のフィルターを使用して検索"(objectClass =\*)"の先祖のインデックスを使用します。

### <a name="other-index-considerations"></a>その他のインデックスに関する考慮事項

-   確保して、インデックスを作成する問題に最適なソリューション、クエリのチューニングがオプションとして使い果たされた後。 ハードウェアを正しくサイズ設定は、非常に重要です。 適切な修正プログラムは、ハードウェアの問題を難読化しようとしないと、属性のインデックスを作成するときにのみ、インデックスを追加する必要があります。

-   インデックスは、インデックスが作成される属性の合計サイズの最小値、データベースのサイズを大ききます。 データベース サイズの増加の推定値は、属性のデータの平均サイズを取得して設定属性を設定するオブジェクトの数を乗算してしたがって評価できます。 一般に、データベースのサイズで 1% の増加についてはします。 詳細については、次を参照してください。 [、データ ストアのしくみ](https://technet.microsoft.com/library/cc772829.aspx)します。

-   組織単位レベルでの検索動作が実行して主場合は、コンテナー化された検索のインデックス作成を検討してください。

-   タプル インデックスは通常のインデックスよりも大きくなりますが、サイズを推定するはかなり難しきます。 最大 20% の成長、床面として通常のインデックス サイズの推定を使用します。 詳細については、次を参照してください。 [、データ ストアのしくみ](https://technet.microsoft.com/library/cc772829.aspx)します。

-   組織単位レベルでの検索動作が実行して主場合は、コンテナー化された検索のインデックス作成を検討してください。

-   内の検索文字列と最終的な検索文字列をサポートするためにタプル インデックスが必要です。 最初の検索文字列のタプル インデックスが不要です。

    -   最初の検索文字列: (samAccountName = MYPC\*)

    -   検索文字列である中間 (samAccountName =\*MYPC\*)

    -   最終的な検索文字列: (samAccountName =\*MYPC$)

-   インデックスを作成する場合は、インデックスが構築されるときにディスク I/O が生成されます。 これは優先順位の低いバック グラウンド スレッドで行われ、受信要求は、インデックスの構築よりも優先されます。 環境の容量計画が正しく行われるされている場合は、透過的なこの必要があります。 ただし、書き込み負荷の高いシナリオまたはドメイン コント ローラーの記憶域の負荷が不明環境クライアント エクスペリエンスが低下しする必要があります勤務時間外に行われます。

-   インデックスの構築、ローカルで行われるために、レプリケーション トラフィックに影響は最小限です。

詳細については、次を参照してください。

-   [効率の高い Microsoft Active Directory 対応のアプリケーションを作成します。](https://msdn.microsoft.com/library/ms808539.aspx)

-   [Active Directory Domain Services での検索](https://msdn.microsoft.com/library/aa746427.aspx)

-   [インデックス付けされた属性](https://msdn.microsoft.com/library/windows/desktop/ms677112.aspx)

## <a name="see-also"></a>関連項目

- [Active Directory サーバーのチューニング パフォーマンス](index.md)
- [ハードウェアに関する考慮事項](hardware-considerations.md)
- [ドメイン コントローラーとサイトの適切な配置に関する考慮事項](site-definition-considerations.md)
- [ADDS パフォーマンスのトラブルシューティング](troubleshoot.md) 
- [Active Directory Domain Services のキャパシティ プランニング](https://go.microsoft.com/fwlink/?LinkId=324566)