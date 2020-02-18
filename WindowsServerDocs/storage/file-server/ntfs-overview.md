---
title: NTFS の概要
description: NTFS の概要について説明します。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 06/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: b98877d0a94ff8033b65bf74d0118e2a5f1ea092
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402076"
---
# <a name="ntfs-overview"></a>NTFS の概要

>適用先:Windows 10、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

NTFS は最新バージョンの Windows と Windows Server のプライマリ ファイル システムであり、セキュリティ記述子、暗号化、ディスク クォータ、リッチ メタデータなど豊富な機能を備えています。また、クラスターの共有ボリューム (CSV) と併用することで、フェールオーバー クラスターの複数のノードから同時アクセス可能であり、継続的に使用可能なボリュームを実現できます。

Windows Server 2012 R2 の NTFS の新機能と変更された機能の詳細については、[NTFS の新機能](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))に関する記事を参照してください。 その他の機能については、このトピックの「[追加情報](#additional-information)」セクションを参照してください。 新しい Resilient File System (ReFS) の詳細については、「[Resilient File System (ReFS) の概要](../refs/refs-overview.md)」を参照してください。

## <a name="practical-applications"></a>実際の適用例

### <a name="increased-reliability"></a>信頼性の向上

システム障害が発生してコンピューターが再起動されると、NTFS では、そのログ ファイルとチェックポイント情報を使用してファイル システムの整合性が復元されます。 不良セクター エラーが発生すると、NTFS によってその不良セクターを含むクラスターが動的に再マッピングされ、データに新しいクラスターが割り当てられ、元のクラスターが不良とマークされ、以前のクラスターは使用されなくなります。 たとえば、サーバーがクラッシュした後、NTFS ではログ ファイルを再生してデータを回復できます。

NTFS を使うと、ボリュームをオフラインにしなくても、一時的な破損の問題をバックグラウンドで継続的に監視および修正できます (この機能は、Windows Server 2008 で導入され、[自己修復 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)) と呼ばれます)。 大規模な破損の問題の場合は、ボリュームがオンラインの間に Windows Server 2012 以降の Chkdsk ユーティリティを使ってドライブのスキャンと分析を行い、ボリューム上のデータの整合性を復元するために必要な時間まで、オフラインの時間を制限することができます。 NTFS がクラスター共有ボリュームと併用されている場合、ダウンタイムは必要ありません。 詳細については、[NTFS の正常性と Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11)) に関する記事を参照してください。

### <a name="increased-security"></a>セキュリティの向上

- **ファイルとフォルダーのアクセス制御リスト (ACL) ベースのセキュリティ**: NTFS を使って、ファイルまたはフォルダーに対するアクセス許可を設定し、アクセスを制限または許可するグループとユーザーを指定し、アクセスの種類を選択することができます。

- **BitLocker ドライブ暗号化のサポート**: BitLocker ドライブ暗号化によって、NTFS ボリュームに格納されている重要なシステム情報やその他のデータに対するセキュリティが強化されます。 Windows Server 2012 R2 および Windows 8.1 以降、BitLocker は、コネクト スタンバイをサポートするトラステッド プラットフォーム モジュール (TPM) を搭載した x86 および x64 ベースのコンピューターに対して、デバイス暗号化をサポートするようになりました (以前は Windows RT デバイスでのみ利用可能でした)。 デバイスの暗号化は、Windows ベースのコンピューター上のデータを保護するために役立ちます。また、悪意のあるユーザーがユーザーのパスワードを見つけるために利用するシステム ファイルにアクセスすることや、ドライブを PC から物理的に取り外して別のものに取り付けてアクセスすることをブロックするために役立ちます。 詳細については、「[BitLocker の新機能](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11))」を参照してください。

- **大容量ボリュームのサポート**: NTFS では、256 TB のサイズのボリュームをサポートできます。 サポートされるボリュームのサイズは、クラスターのサイズとクラスターの数の影響を受けます。 (2<sup>32</sup> - 1) クラスター (NTFS がサポートするクラスターの最大数) では、次のボリューム サイズとファイル サイズがサポートされます。

  |クラスター サイズ|最大ボリューム|最大ファイル|
  |---|---|---|
  |4 KB (既定のサイズ)|16 TB|16 TB|
  |8 KB|32 TB|32 TB|
  |16 KB|64 TB|64 TB|
  |32 KB|128 TB|128 TB|
  |64 KB (最大サイズ)|256 TB|256 TB|

>[!IMPORTANT]
>サービスとアプリによっては、ファイルとボリューム サイズに対して追加の制限が課される場合があります。 たとえば、以前のバージョンの機能、またはボリューム シャドウ コピー サービス (VSS) のスナップショットを利用するバックアップ アプリを使用している場合 (かつ、SAN または RAID エンクロージャを使用していない場合)、ボリューム サイズの上限は 64 TB になります。 ただし、ワークロードとストレージのパフォーマンスによっては、より小さいボリューム サイズの使用が必要になる場合があります。

### <a name="formatting-requirements-for-large-files"></a>大きなファイルのフォーマットの要件

大きな .vhdx ファイルを適切に拡張できるようにするには、ボリュームのフォーマットについて新しい推奨事項があります。 データ重複除去で使用するボリュームをフォーマットするとき、または 1 TB を超える .vhdx ファイルなどの非常に大きなファイルをホストする場合は、Windows PowerShell で次のパラメーターを指定して **Format-Volume** コマンドレットを使用します。

|パラメーター|説明|
|---|---|
|-AllocationUnitSize 64KB|64 KB の NTFS アロケーション ユニット サイズを設定します。|
|-UseLargeFRS|大きなファイル レコード セグメント (FRS) のサポートを有効にします。 これは、ボリューム上のファイルごとに許可されるエクステントの数を増やすために必要です。 大きな FRS レコードの場合、上限は約 150 万エクステントから約 600 万エクステントに増えます。|

たとえば、次のコマンドレットを実行すると、FRS が有効でアロケーション ユニット サイズが 64 KB の NTFS ボリュームとしてドライブ D がフォーマットされます。

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

また、**format** コマンドを使用することもできます。 システムのコマンド プロンプトで、次のコマンドを入力します。 **/L** を指定すると大きな FRS ボリュームがフォーマットされ、 **/A:64k** を指定すると 64 KB のアロケーション ユニット サイズが設定されます。

```PowerShell
format /L /A:64k
```

### <a name="maximum-file-name-and-path"></a>ファイル名とパスの最大値

NTFS では、長いファイル名と拡張パスがサポートされており、最大値は次のとおりです。

- **下位互換性のある長いファイル名のサポート**: NTFS では、長いファイル名を使用し、ディスク上に (Unicode で) 8.3 エイリアスを格納できるので、ファイル名と拡張子に 8.3 の制限を課すファイル システムとの互換性を確保することができます。 (パフォーマンス上の理由から) 必要に応じて、Windows Server 2008 R2、Windows 8、およびより新しいバージョンの Windows オペレーティング システムの個々の NTFS ボリューム上で 8.3 エイリアスを選択的に無効にすることができます。
  Windows Server 2008 R2 以降のシステムでは、オペレーティング システムを使用してボリュームをフォーマットすると、既定で短縮名は無効になります。 アプリケーションの互換性のために、短い名前はシステム ボリューム上で引き続き有効です。

- **拡張パスのサポート**: 多くの Windows API 関数には、MAX\_PATH 設定で定義された 260 文字のパスの上限を超える約 32,767 文字の拡張パスを許可する Unicode バージョンがあります。 ファイル名とパス形式の詳細な要件と、拡張パスを実装するためのガイダンスについては、「[ファイル、パス、および名前空間の名前付け](https://msdn.microsoft.com/library/windows/desktop/aa365247)」を参照してください。

- **クラスター化されたストレージ**: フェールオーバー クラスターで使用する場合、NTFS では、クラスター共有ボリューム (CSV) ファイル システムと組み合わせて使用すると、複数のクラスター ノードから同時にアクセスできる継続的に使用可能なボリュームがサポートされます。 詳細については、「[フェールオーバー クラスターでクラスターの共有ボリュームを使用する](../../failover-clustering/failover-cluster-csvs.md)」を参照してください。

### <a name="flexible-allocation-of-capacity"></a>容量の柔軟な割り当て

ボリュームの領域が限られている場合、NTFS にはサーバーのストレージ容量を操作できる次の方法が用意されています。

- ディスク クォータを使用して、個々のユーザーの NTFS ボリューム上のディスク領域の使用状況を追跡および制御します。
- ファイル システムの圧縮を使用して、格納できるデータの量を最大化します。
- 同じディスクまたは別のディスクから未割り当て領域を追加して、NTFS ボリュームのサイズを増やします。
- ドライブ文字が不足している場合、または既存のフォルダーからアクセスできる追加の領域を作成する必要がある場合は、ローカル NTFS ボリューム上の空のフォルダーにボリュームをマウントします。

## <a name="additional-information"></a>追加情報

- [ReFS および NTFS のクラスター サイズに関する推奨事項](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Cluster-size-recommendations-for-ReFS-and-NTFS/ba-p/425960)
- [Resilient File System (ReFS) の概要](../refs/refs-overview.md)
- [NTFS の新機能](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)) (Windows Server 2012 R2)
- [NTFS の新機能](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff383236(v=ws.10)) (Windows Server 2008 R2、Windows 7)
- [NTFS の正常性と Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))
- [自己復旧 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)) (Windows Server 2008 で導入)
- [トランザクション NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10)) (Windows Server 2008 で導入)
- [Windows Server の記憶域](../storage.md)