---
title: NTFS の概要
description: NTFS の新機能の説明です。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 556110fe7bed1aed002ef6d985324ff5171e770e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885373"
---
# <a name="ntfs-overview"></a>NTFS の概要

>適用対象:Windows 10、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

NTFS-最近のバージョンの Windows および Windows Server のプライマリ ファイル システム、セキュリティ記述子、暗号化、ディスク クォータ、リッチ メタデータなどの機能の完全なセットし、継続的に提供するクラスター共有ボリューム (CSV) とを使用できますフェールオーバー クラスターの複数のノードから同時にアクセスできる使用可能なボリュームです。

Windows Server 2012 R2 の NTFS 機能と変更された機能の詳細については、次を参照してください。 [NTFS の新](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))します。 追加の機能については、次を参照してください。、[追加情報](#additional-information)このトピックの「します。 新しい Resilient File System (ReFS) の詳細については、次を参照してください。 [Resilient File System (ReFS) の概要](../refs/refs-overview.md)します。

## <a name="practical-applications"></a>実際の適用例

### <a name="increased-reliability"></a>信頼性の向上

NTFS では、そのログ ファイルとチェックポイント情報を使用して、システム障害の後、コンピューターを再起動すると、ファイル システムの整合性を復元します。 不良セクター エラーの発生後 NTFS では、不良セクターが含まれています、データの新しいクラスターに割り当てますは不良である、元のクラスターをマークおよび不要になった、以前のクラスターを使用するクラスターが動的に再マップします。 たとえば、サーバー クラッシュ後 NTFS データを回復できますのログ ファイルを再生します。

NTFS は継続的に監視し、ボリュームをオフラインにせず、バック グラウンドでの一時的な破損の問題を修正 (この機能と呼ばれる[NTFS の自己修復](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))、Windows Server 2008 で導入された)。 大規模な破損問題については、Chkdsk ユーティリティを Windows Server 2012 以降はスキャンし、ボリュームがオンラインで、ボリュームのデータの整合性の復元に必要な時間にオフライン時間を制限するときに、ドライブを分析します。 クラスターの共有ボリュームで NTFS を使用する場合のダウンタイムは必要ありません。 詳細については、次を参照してください。 [NTFS 正常性と Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))します。

### <a name="increased-security"></a>セキュリティの強化

- **アクセス制御リスト ACL ベースのセキュリティ ファイルとフォルダーの**-NTFS ファイルまたはフォルダーのアクセス許可を設定することができます、グループとユーザー アクセスを制限または許可するを指定し、アクセスの種類を選択します。

- **BitLocker ドライブ暗号化のサポート**— BitLocker ドライブ暗号化が重要なシステム情報および NTFS ボリュームに格納されているその他のデータの追加のセキュリティを提供します。 以降 Windows Server 2012 R2 および Windows 8.1 では、BitLocker 対応していますデバイス暗号化の x86 および x64 ベース コンピューターのトラステッド プラットフォーム モジュール (TPM) のサポートがスタンド by (以前 Windows RT デバイスでのみ使用可能な) に接続されています。 デバイスの暗号化は、Windows ベースのコンピューター上のデータを保護でき、悪意のあるユーザーをユーザーのパスワードの検出に依存しているシステム ファイルへのアクセスやから物理的に PC から削除しにインストールしたドライブへのアクセスをブロックします。別の 1 つ。 詳細については、次を参照してください。 [BitLocker の新](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11))します。

- **大量ボリュームのサポート**-NTFS ボリュームが 256 のテラバイトの大きさをサポートできます。 サイズは、クラスターのサイズのクラスターの数によって影響を受けるボリュームがサポートされています。 使用 (2<sup>32</sup> – 1) クラスター (NTFS がサポートしているクラスターの最大数)、次のボリュームとファイル サイズがサポートされています。

  |クラスター サイズ|最大サイズのボリューム|最大のファイル|
  |---|---|---|
  |4 KB (既定のサイズ)|16 TB|16 TB|
  |8 KB|32 TB|32 TB|
  |16 KB|64 TB です。|64 TB です。|
  |32 KB|128 TB|128 TB|
  |64 KB (最大サイズ)|256 TB|256 TB|

>[!IMPORTANT]
>サービスとアプリは、追加のファイルとボリュームのサイズ制限を課すことがあります。 たとえば、ボリュームのサイズ制限は 64 TB、以前のバージョンの機能や、バックアップ アプリを使用している場合は、ボリューム シャドウ コピー サービス (VSS) スナップショットの使用 (、SAN または RAID エンクロージャを使用していない)。 ただし、ワークロードと記憶域のパフォーマンスに応じて小さいボリューム サイズを使用する必要があります。

### <a name="formatting-requirements-for-large-files"></a>大きなファイルの形式の要件

大規模な .vhdx ファイルの適切な拡張機能を許可するのには、ボリュームを書式設定するための新しい推奨事項です。 データ重複除去で使用されるか、1 TB を超える .vhdx ファイルなどの非常に大きなファイルをホストするボリュームをフォーマットするときに使用して、**ボリュームのフォーマット**コマンドレットは、Windows PowerShell で次のパラメーターとします。

|パラメーター|説明|
|---|---|
|AllocationUnitSize 64 KB|64 KB NTFS アロケーション ユニットのサイズを設定します。|
|-UseLargeFRS|大きいファイル レコード セグメント (FRS) のサポートを有効にします。 これは、ボリューム上のファイルごとに許可されているエクステントの数を増やす必要です。 大規模な FRS レコードを制限は約 150万エクステントから約 600万エクステントに増加します。|

など、コマンドレットの次の形式は、FRS が有効になっていると、アロケーション ユニット サイズ 64 KB の NTFS ボリュームとして D をドライブします。

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

また、使用して、**形式**コマンド。 システムのコマンド プロンプトで、次のコマンドを入力します。 場所 **/L** 、大規模な FRS ボリュームをフォーマットおよび **/A:64 k** 、64 KB アロケーション ユニット サイズの設定。

```PowerShell
format /L /A:64k
```

### <a name="maximum-file-name-and-path"></a>最大のファイル名とパス

NTFS では、長いファイル名および以下の最大値の長拡張パスをサポートします。

- **旧バージョンとの互換性の長いファイル名のサポート**-NTFS では、長いファイル名、ファイル名と拡張子の 8.3 制限ファイル システムとの互換性を提供するエイリアス (Unicode) でディスク上にいる、8.3 を格納します。 (パフォーマンス上の理由) が必要な場合、Windows Server 2008 R2、Windows 8、および最新バージョンの Windows オペレーティング システムの個々 の NTFS ボリュームに 8.3 の別名を選択的に無効にできます。
  Windows Server 2008 R2 およびそれ以降のシステムでボリュームがオペレーティング システムでフォーマットされている場合、短い名前は既定で無効にします。 アプリケーションの互換性のための短い名前はに対して有効なままシステム ボリューム。

- **長拡張パスのサポート**— 多くの Windows API 関数が約 32,767 文字の長さが拡張パスを許可する Unicode バージョンがあるなど、最大で定義されているパスを 260 文字の制限を超える\_パスの設定。 詳細なファイル名とパスの形式の要件と長拡張パスの実装に関するガイダンスは、次を参照してください。[ファイルの名前付け、パス、および名前空間](https://msdn.microsoft.com/library/windows/desktop/aa365247)します。

- **記憶域をクラスター化された**— クラスター共有ボリューム (CSV) ファイル システムと組み合わせて使用すると同時に複数のクラスター ノードによってアクセスできる継続的に使用可能なボリュームを NTFS がサポートしているフェールオーバー クラスターで使用する場合。 詳細については、次を参照してください。 [Use Cluster Shared Volumes フェールオーバー クラスターで](../../failover-clustering/failover-cluster-csvs.md)します。

### <a name="flexible-allocation-of-capacity"></a>容量の柔軟な割り当て

ボリューム上の領域が制限されている場合、NTFS は、サーバーの記憶域容量を使用する次の方法を提供します。

- 追跡および個々 のユーザーの NTFS ボリュームでディスク使用量を制御するには、ディスク クォータを使用します。
- 格納できるデータの量を最大化するのにには、ファイル システム圧縮を使用します。
- 同じディスクまたは別のディスクからの未割り当て領域を追加することで、NTFS ボリュームのサイズを増やします。
- ローカル NTFS ボリューム上の空のフォルダー ボリュームをマウントするドライブ文字から実行するか、既存のフォルダーからアクセスできる追加の領域を作成する必要があります。

## <a name="additional-information"></a>追加情報

|コンテンツの種類|参考資料|
|---|---|
|評価|- [NTFS の新](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))(Windows Server 2012 R2)<br>- [NTFS の新](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff383236(v=ws.10))(Windows Server 2008 R2、Windows 7)<br>- [NTFS の正常性と Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))<br>- [NTFS の自己修復](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))(Windows Server 2008 で導入)<br>- [トランザクション NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10)) (Windows Server 2008 で導入)|
|コミュニティ リソース|- [Windows Storage チームのブログ](https://blogs.msdn.microsoft.com/san/)|
|関連テクノロジ|- [Windows Server でのストレージ](../storage.md)<br>- [クラスターは、フェールオーバー クラスターでボリュームを共有します。](../../failover-clustering/failover-cluster-csvs.md)<br>-[クラスターの共有ボリューム](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)#cluster-shared-volumes>)と[記憶域の設計](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)#storage-design>)のセクションでは[クラウド インフラストラクチャの設計](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)) <br>- [記憶域スペース](../storage-spaces/overview.md)<br>- [Resilient File System (ReFS) の概要](../refs/refs-overview.md)
