---
title: での LDAP に関する考慮事項によるパフォーマンスチューニングの追加
description: Active Directory ワークロードでの LDAP に関する考慮事項
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: timwi; chrisrob; herbertm; kenbrumf;  mleary; shawnrab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 2ef32b379dcc5d1c2d8217564b639f44d024e5ee
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471548"
---
# <a name="ldap-considerations-in-adds-performance-tuning"></a>での LDAP に関する考慮事項によるパフォーマンスチューニングの追加

> [!IMPORTANT]
> 以下は、 [Active Directory Domain Services の容量計画](https://go.microsoft.com/fwlink/?LinkId=324566)に関する記事で詳しく説明されている Active Directory ワークロードのために、サーバーハードウェアを最適化するための主な推奨事項と考慮事項の概要を示しています。 リーダーは、 [Active Directory Domain Services のキャパシティプランニング](https://go.microsoft.com/fwlink/?LinkId=324566)を検討して、これらの推奨事項に関する技術的な理解と影響を高めます。

## <a name="verify-ldap-queries"></a>LDAP クエリの検証

LDAP クエリが効率的なクエリの作成に関する推奨事項に準拠していることを確認します。

Active Directory に対して使用するクエリを適切に記述、構築、および分析する方法については、MSDN の幅広いドキュメントを参照してください。 詳細については、「[より効率的な Microsoft Active Directory 対応アプリケーションの作成](https://msdn.microsoft.com/library/ms808539.aspx)」を参照してください。

## <a name="optimize-ldap-page-sizes"></a>LDAP ページサイズの最適化

クライアント要求への応答として複数のオブジェクトを使用して結果を返す場合、ドメインコントローラーは一時的に結果セットをメモリに格納する必要があります。 ページサイズを大きくすると、メモリ使用量が増加し、不必要にキャッシュから除外される可能性があります。 この場合、既定の設定は最適です。 ページサイズの設定を増やすための推奨事項がいくつかあります。 特に不適切と特定されない限り、既定値を使用することをお勧めします。

クエリに多くの結果が含まれている場合は、同時に実行される同様のクエリの制限が発生する可能性があります。  これは、LDAP サーバーが cookie プールと呼ばれるグローバルメモリ領域を消費する可能性があるためです。  「 [LDAP サーバーの cookie の処理方法](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/manage/how-ldap-server-cookies-are-handled)」で説明されているように、プールのサイズを増やす必要がある場合があります。

これらの設定を調整するには、「 [Windows Server 2008 以降のドメインコントローラーは LDAP 応答に5000値のみを返し](https://support.microsoft.com/kb/2009267)ます」を参照してください。

## <a name="determine-whether-to-add-indices"></a>インデックスを追加するかどうかを判断する

属性のインデックス作成は、フィルターで属性名を持つオブジェクトを検索する場合に便利です。 インデックスを作成すると、フィルターを評価するときにアクセスする必要があるオブジェクトの数を減らすことができます。 ただし、これにより書き込み操作のパフォーマンスが低下します。これは、対応する属性が変更または追加されたときにインデックスを更新する必要があるためです。 また、ディレクトリデータベースのサイズも大きくなりますが、多くの場合、ストレージのコストを上回るメリットがあります。 ログ記録を使用して、高価で非効率なクエリを見つけることができます。 特定した後は、検索のパフォーマンスを向上させるために、対応するクエリで使用されるいくつかの属性のインデックスを作成することを検討してください。 Active Directory 検索の動作の詳細については、「 [Active Directory の検索のしくみ](https://technet.microsoft.com/library/cc755809.aspx)」を参照してください。

### <a name="scenarios-that-benefit-in-adding-indices"></a>インデックスを追加する場合の利点

-   データの要求におけるクライアントの負荷が大量の CPU 使用率を生成しているため、クライアントのクエリ動作を変更または最適化できません。 大幅に負荷がかかる場合は、サーバーパフォーマンスアドバイザーまたは組み込みの Active Directory データコレクターセットの上位10の攻撃者一覧に表示されており、CPU の使用率が1% を超えていることを考慮してください。

-   インデックスなしの属性が原因で、クライアントの負荷によってサーバー上で大量のディスク i/o が生成されていますが、クライアントのクエリ動作を変更または最適化することはできません。

-   インデックスがカバーされていないため、クエリの実行に時間がかかり、クライアントに許容できる時間内に完了していません。

- 長い期間の大量のクエリでは、ATQ LDAP スレッドの消費と枯渇が発生しています。 次のパフォーマンスカウンターを監視します。

    - **NTDS \\要求の待機時間**–これは、要求の処理にかかる時間の影響を受けます。 ただし、120秒 (既定値) の後に要求がタイムアウトになるようにすると、ほとんどの場合、実行時間が大幅に短縮され、極端に長時間に実行されるクエリは、全体の数値で非表示になります。 Active Directory 絶対しきい値ではなく、この基準の変更を検索します。

        > [!NOTE]
        > この値が高い場合は、他のドメインに対する "プロキシ処理" 要求の遅延を示すインジケーターや、CRL チェックを行うこともできます。

    - **NTDS \\推定キュー遅延**–最適なパフォーマンスを得るためには、最適なパフォーマンスを得るためには0に近い必要があります。これは、要求がサービスの待機に時間を費やすことがないためです。

これらのシナリオは、次の1つまたは複数の方法を使用して検出できます。

-   [統計コントロールを使用したクエリタイミングの決定](https://msdn.microsoft.com/library/ms808539.aspx)

-   [高コストで非効率的な検索の追跡](https://msdn.microsoft.com/library/ms808539.aspx)

-   パフォーマンスモニターの Active Directory 診断データコレクターセット ([SPA の Son: Win2008 以降の AD データコレクターセット](https://blogs.technet.com/b/askds/archive/2010/06/08/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond.aspx))

-   [Microsoft Server Performance Advisor](../../../server-performance-advisor/microsoft-server-performance-advisor.md)Active Directory Advisor パック

-   先祖インデックスを使用する "(objectClass =)" 以外の任意のフィルターを使用して検索し \* ます。

### <a name="other-index-considerations"></a>その他のインデックスに関する考慮事項

-   クエリがオプションとして使い果たされた後に、インデックスを作成して問題に対する適切な解決策があることを確認してください。 ハードウェアのサイズを正しく設定することは非常に重要です。 インデックスは、ハードウェアの問題を難読化しようとするのではなく、属性にインデックスを設定する必要がある場合にのみ追加してください。

-   インデックスを作成すると、インデックスを作成する属性の合計サイズの最小値によって、データベースのサイズが大きくなります。 このため、データベースの増加量の見積もりは、属性内のデータの平均サイズを取得し、属性が設定されるオブジェクトの数を乗算することで評価できます。 一般に、これはデータベースサイズの1% 増加に関するものです。 詳細については、「[データストアのしくみ](https://technet.microsoft.com/library/cc772829.aspx)」を参照してください。

-   検索動作が組織単位レベルで行われる場合は、コンテナー化検索のインデックス作成を検討してください。

-   タプルインデックスは通常のインデックスよりも大きくなりますが、サイズを推定するのは非常に困難です。 通常のインデックスサイズの推定値は、増加に対するフロアとして使用します。最大値は20% です。 詳細については、「[データストアのしくみ](https://technet.microsoft.com/library/cc772829.aspx)」を参照してください。

-   検索動作が組織単位レベルで行われる場合は、コンテナー化検索のインデックス作成を検討してください。

-   インデックスは、medial 検索文字列と最終的な検索文字列をサポートするために必要です。 最初の検索文字列にタプルインデックスは必要ありません。

    -   最初の検索文字列– (samAccountName = MYPC \* )

    -   Medial 検索文字列-(samAccountName = \* mypc \* )

    -   最終的な検索文字列– (samAccountName = \* mypc $)

-   インデックスを作成すると、インデックスの作成中にディスク i/o が生成されます。 これは、優先順位の低いバックグラウンドスレッドで実行され、受信要求はインデックス構築より優先されます。 環境の容量計画が正常に完了している場合は、このことを意識する必要はありません。 ただし、書き込みが多いシナリオや、ドメインコントローラー記憶域の負荷が不明な環境では、クライアントエクスペリエンスが低下する可能性があるため、時間外に行う必要があります。

-   インデックスの構築はローカルで行われるため、レプリケーショントラフィックへの影響は最小限に抑えられます。

詳細については、次の情報を参照してください。

-   [より効率的な Microsoft Active Directory 対応アプリケーションの作成](https://msdn.microsoft.com/library/ms808539.aspx)

-   [Active Directory Domain Services の検索](https://msdn.microsoft.com/library/aa746427.aspx)

-   [インデックス付き属性](https://msdn.microsoft.com/library/windows/desktop/ms677112.aspx)

## <a name="additional-references"></a>その他のリファレンス

- [Active Directory サーバーのパフォーマンス チューニング](index.md)
- [ハードウェアに関する考慮事項](hardware-considerations.md)
- [ドメイン コントローラーとサイトの適切な配置に関する考慮事項](site-definition-considerations.md)
- [ADDS パフォーマンスのトラブルシューティング](troubleshoot.md)
- [Active Directory Domain Services のキャパシティ プランニング](https://go.microsoft.com/fwlink/?LinkId=324566)