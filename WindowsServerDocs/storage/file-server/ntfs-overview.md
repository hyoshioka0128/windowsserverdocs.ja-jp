---
title: NTFS の概要
description: どのような NTFS の説明は次のとおりです。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 556110fe7bed1aed002ef6d985324ff5171e770e
ms.sourcegitcommit: 5ed023a2ef3a9002daf41c7717feb1df186d2a14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2019
ms.locfileid: "9122105"
---
# NTFS の概要

>適用対象: Windows 10、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

NTFS、最近のバージョンの Windows および Windows Server のプライマリ ファイル システム、セキュリティ記述子、暗号化、ディスク クォータ、リッチ メタデータなどの機能の完全なセットを提供し、継続的に提供するクラスター共有ボリューム (CSV) とを使用することができますフェールオーバー クラスターの複数のノードから同時にアクセスできる利用可能なボリューム。

Windows Server 2012 R2 の NTFS で新しいや変更された機能について詳しくは、[新機能については NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))を参照してください。 追加の機能については、このトピックの[追加情報](#additional-information)] セクションを参照してください。 新しい Resilient File System (ReFS) について詳しくは、 [Resilient File System (ReFS) の概要](../refs/refs-overview.md)をご覧ください。

## 実際の適用例

### 信頼性の向上

NTFS では、そのログ ファイルとチェックポイント情報を使用して、システム障害の発生後、コンピューターが再起動されるときに、ファイル システムの整合性を復元します。 NTFS には、不良セクター エラーが発生した、クラスター不良セクターが含まれています、データの新しいクラスターを割り当てます、として無効な場合は、元のクラスターをマーク、古いクラスターで使用されなくなったを動的に再マップします。 たとえば、サーバーのクラッシュの後 NTFS を回復できますデータのログ ファイルを再生します。

NTFS は継続的に監視し、(この機能は[自己修復 NTFS の場合](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))、Windows Server 2008 で導入されたと呼ばれます)、ボリュームをオフラインにすることがなく、バック グラウンドでの一時的な破損の問題を修正します。 大規模な破損問題については、Chkdsk ユーティリティは、Windows Server 2012 以降はスキャンし、ボリュームはオンライン、オフライン時間、ボリューム上のデータの整合性を復元するために必要な時間を制限するときに、ドライブを分析します。 NTFS 使用すると、クラスターの共有ボリュームのダウンタイムを必要はありません。 詳細については、 [NTFS の正常性と Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))を参照してください。

### セキュリティの強化

- **ファイルとフォルダーのアクセス制御リスト ACL ベースのセキュリティ**NTFS ファイルまたはフォルダーのアクセス許可を設定することができますグループとユーザー アクセスを制限または許可するを指定し、アクセスの種類を選択します。

- **BitLocker ドライブ暗号化のサポート**: BitLocker ドライブ暗号化は重要なシステム情報と NTFS ボリュームに格納されているその他のデータの追加のセキュリティを提供します。 Windows Server 2012 R2 と Windows 8.1 以降では、BitLocker は、サポート x86 および x64 ベースのコンピューターで、トラステッド プラットフォーム モジュール (TPM) でデバイスの暗号化スタンド by (以前 Windows RT デバイスでのみ利用可能な) サポートが接続されています。 デバイスの暗号化では、Windows ベースのコンピューター上のデータを保護し、これにより、ユーザーのパスワードを検出するに依存しているシステム ファイルへのアクセスや物理的に PC から削除しにインストールすることによってドライブへのアクセスからの悪意のあるユーザーをブロックします。1 つの異なるします。 詳細については、 [BitLocker の新機能では、何](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11))を参照してください。

- **大量ボリュームのサポート**: NTFS は 256 テラバイトと同じサイズのボリュームをサポートできます。 クラスター サイズとクラスターの数によってサイズが影響を受けるボリュームがサポートされています。 (2<sup>32</sup> – 1) とクラスター (NTFS をサポートしているクラスターの最大数)、次のボリューム ファイル サイズがサポートされています。

  |クラスター サイズ|最大ボリューム|最大ファイル|
  |---|---|---|
  |4 KB (既定のサイズ)|16 TB|16 TB|
  |8 KB|32 TB|32 TB|
  |16 KB|64 TB|64 TB|
  |32 KB|128 TB|128 TB|
  |64 KB (最大サイズ)|256 TB|256 TB|

>[!IMPORTANT]
>サービスとアプリ追加を制限ファイルやボリュームのサイズ。 たとえば、ボリュームのサイズの制限はボリューム シャドウ コピー サービス (VSS) のスナップショットを使用して、以前のバージョンの機能やバックアップ アプリが使っている場合、64 TB (、SAN または RAID エンクロージャを使用していない)。 ただし、ワークロードと記憶域のパフォーマンスに応じてボリュームのサイズが小さいを使用する必要があります。

### 大きいファイルの要件を書式設定

大規模な .vhdx ファイルの適切な拡張機能を許可するのには、ボリュームを書式設定の新しい推奨事項があります。 データ重複除去で使用するか、1 TB を超える .vhdx ファイルなど、非常に大きなファイルをホストするボリュームを書式設定するときは、次のパラメーターで Windows PowerShell で**ボリュームのフォーマット**コマンドレットを使用します。

|パラメーター|説明|
|---|---|
|AllocationUnitSize 64 KB|64 KB NTFS のアロケーション ユニット サイズを設定します。|
|-UseLargeFRS|大きなファイル レコード セグメント (FRS) のサポートを有効にします。 これは、ボリューム上のファイルごとに許可される範囲の数を増やす必要です。 大量の FRS レコードの制限は約 1.5 人以上の範囲から約 600万範囲に増加します。|

たとえば、次のコマンドレットの形式ドライブ D NTFS ボリュームとして有効になっている FRS と 64 KB のアロケーション ユニット サイズ。

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

また、 **format**コマンドを使用することもできます。 システムのコマンド プロンプトで、 **/L** FRS 大量の形式し、 **/A:64 k** 64 KB のアロケーション ユニット サイズの設定、次のコマンドを入力します。

```PowerShell
format /L /A:64k
```

### 最大ファイルの名前とパス

NTFS には、長いファイル名と、次の最大値の長さが拡張パスがサポートしています。

- **下位互換性を長いファイル名のサポート**-NTFS では、長い名前のファイル (Unicode) でディスク上のファイル名と拡張子 8.3 制限ファイル システムとの互換性を提供する、8.3 をエイリアス保存します。 パフォーマンス上の理由により) が必要な場合、Windows Server 2008 R2、Windows 8、および最新のバージョンの Windows オペレーティング システム内の個々 の NTFS ボリューム上の 8.3 のエイリアスを選択的に無効にできます。
  ボリュームがオペレーティング システムでフォーマットされている場合は、Windows Server 2008 R2 およびそれ以降のシステムでは、既定では短い名前が無効です。 アプリケーションの互換性のための短い名前はに対して有効なままシステム ボリューム。

- **長拡張パスのサポート**-多くの Windows API 関数には、長拡張パスの約 32,767 文字を許可する Unicode バージョンがインストールされている-MAX\_PATH 設定によって定義された 260 文字パスの制限を超えています。 詳細なファイルの名前とパスの形式の要件と長拡張パスを実装するためのガイダンスは、[ファイルの名前付け、パス、および名前空間](https://msdn.microsoft.com/library/windows/desktop/aa365247)を参照してください。

- **クラスター化された記憶域**: NTFS、クラスター共有ボリューム (CSV) ファイル システムと組み合わせて使用すると同時に複数のクラスター ノードからアクセスできる継続的に利用可能なボリュームがサポートされるフェールオーバー クラスターで使用する場合。 詳細については、[フェールオーバー クラスターで使用してクラスター共有ボリューム](../../failover-clustering/failover-cluster-csvs.md)を参照してください。

### 容量の柔軟な割り当て

ボリューム上の領域が限られた場合は、NTFS は次のサーバーの記憶域の容量を操作する方法を提供します。

- ディスク クォータを使用して追跡し、個々 のユーザーの NTFS ボリューム上のディスク領域の使用量を制御します。
- 格納できるデータの量を最大化するのにには、ファイル システムの圧縮を使用します。
- NTFS ボリュームのサイズを大きくには、同じディスクとは異なるディスクから未割り当て領域を追加します。
- ローカルの NTFS ボリューム上の空のフォルダー ボリュームをマウントするドライブ文字が実行するか、既存のフォルダーからアクセス可能なその他の領域を作成する必要があります。

## 追加情報

|コンテンツの種類|参考資料|
|---|---|
|評価|- [NTFS の新機能では](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))(Windows Server 2012 R2)<br>- [NTFS の新機能では](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff383236(v=ws.10))(Windows Server 2008 R2、Windows 7)<br>- [NTFS の正常性と Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))<br>- [NTFS を自動修復](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))(Windows Server 2008 で導入)<br>- [トランザクション NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10))(Windows Server 2008 で導入)|
|コミュニティ リソース|- [Windows のストレージ チームのブログ](https://blogs.msdn.microsoft.com/san/)|
|関連テクノロジ|- [Windows Server の記憶域](../storage.md)<br>- [クラスター共有ボリューム フェールオーバー クラスターの使用](../../failover-clustering/failover-cluster-csvs.md)<br>-[クラスターの共有ボリューム](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)#cluster-shared-volumes>)と[記憶域設計](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)#storage-design>)セクションでは、[クラウド](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11))インフラストラクチャの設計 <br>- [記憶域スペース](../storage-spaces/overview.md)<br>- [Resilient File System (ReFS) の概要](../refs/refs-overview.md)
