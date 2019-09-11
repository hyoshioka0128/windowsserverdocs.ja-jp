---
title: NTFS の概要
description: NTFS の概要について説明します。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 06/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: e43d0520f97f28af54f794daf7ad263bc9928fac
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867350"
---
# <a name="ntfs-overview"></a>NTFS の概要

>適用対象:Windows 10、windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

NTFS —最新バージョンの Windows および Windows Server 用のプライマリファイルシステム-セキュリティ記述子、暗号化、ディスククォータ、豊富なメタデータを含むすべての機能を提供し、クラスターの共有ボリューム (CSV) と共に使用して、継続的に提供することができます。フェールオーバークラスターの複数のノードから同時にアクセスできる使用可能なボリューム。

Windows Server 2012 R2 での NTFS の新機能と変更された機能の詳細については、「 [ntfs の新](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))機能」を参照してください。 その他の機能については、このトピックの「[追加情報](#additional-information)」セクションを参照してください。 新しい弾力性のあるファイルシステム (ReFS) の詳細については、「[弾力性ファイルシステム (refs) の概要](../refs/refs-overview.md)」を参照してください。

## <a name="practical-applications"></a>実際の適用例

### <a name="increased-reliability"></a>信頼性の向上

NTFS は、システム障害が発生した後にコンピューターが再起動されたときに、そのログファイルとチェックポイント情報を使用してファイルシステムの整合性を復元します。 不良セクターエラーが発生すると、その不良セクターを含むクラスターが NTFS によって動的に再マップされ、データに新しいクラスターが割り当てられ、元のクラスターが不良とマークされ、以前のクラスターが使用されなくなります。 たとえば、サーバーがクラッシュした後、NTFS はログファイルを再生してデータを回復できます。

NTFS は、ボリュームをオフラインにしなくても、バックグラウンドで一時的な破損の問題を継続的に監視および修正します (この機能は、Windows Server 2008 で導入された[自己復旧 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))と呼ばれています)。 破損の大きな問題については、Windows Server 2012 以降で Chkdsk ユーティリティを実行すると、ボリュームがオンラインの間、ドライブがスキャンおよび分析され、ボリューム上のデータの整合性を復元するために必要な時間まで、オフラインになる時間が制限されます。 NTFS がクラスターの共有ボリュームと共に使用される場合、ダウンタイムは必要ありません。 詳細については、「 [NTFS Health And Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))」を参照してください。

### <a name="increased-security"></a>セキュリティの強化

- **ファイルとフォルダーの Access Control 一覧 (ACL) ベースのセキュリティ**-NTFS では、ファイルまたはフォルダーに対するアクセス許可を設定し、アクセスを制限または許可するグループとユーザーを指定し、[アクセスの種類] を選択できます。

- **BitLocker ドライブ暗号化のサポート**: BitLocker ドライブ暗号化は、重要なシステム情報や、NTFS ボリュームに格納されているその他のデータに対して、セキュリティを強化します。 Windows Server 2012 R2 および Windows 8.1 以降では、BitLocker は、接続されたスタンドアロン (以前は Windows RT デバイスでのみ利用可能) をサポートするトラステッドプラットフォームモジュール (TPM) を搭載した x86 および x64 ベースのコンピューターでのデバイスの暗号化をサポートしています。 デバイスの暗号化は、Windows ベースのコンピューター上のデータを保護するのに役立ちます。悪意のあるユーザーが、ユーザーのパスワードを検出するために依存しているシステムファイルにアクセスしたり、PC から物理的に削除してドライブにアクセスしたりすることによって、異なるものがあります。 詳細については、「 [BitLocker の新機能](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11))」を参照してください。

- **大容量ボリュームのサポート**— NTFS では、256テラバイトのサイズのボリュームをサポートできます。 サポートされるボリュームのサイズは、クラスターのサイズとクラスターの数の影響を受けます。 (2<sup>32</sup> -1) クラスター (NTFS がサポートするクラスターの最大数) では、次のボリュームサイズとファイルサイズがサポートされています。

  |クラスターサイズ|最大ボリューム|最大ファイル|
  |---|---|---|
  |4 KB (既定のサイズ)|16 TB|16 TB|
  |8 KB|32 TB|32 TB|
  |16 KB|64 TB です。|64 TB です。|
  |32 KB|128 TB|128 TB|
  |64 KB (最大サイズ)|256 TB|256 TB|

>[!IMPORTANT]
>サービスとアプリでは、ファイルとボリュームのサイズに対して追加の制限が課される場合があります。 たとえば、以前のバージョンの機能を使用している場合、またはボリュームシャドウコピーサービス (VSS) のスナップショットを使用している (かつ、SAN または RAID エンクロージャを使用していない) バックアップアプリを使用している場合、ボリュームサイズの上限は 64 TB になります。 ただし、ワークロードとストレージのパフォーマンスによっては、より小さいボリュームサイズの使用が必要になる場合があります。

### <a name="formatting-requirements-for-large-files"></a>大きなファイルの書式設定の要件

大きな .vhdx ファイルを適切に拡張できるようにするには、ボリュームのフォーマットに関する新しい推奨事項があります。 データ重複除去で使用するボリュームをフォーマットするとき、または 1 TB を超える .vhdx ファイルなどの非常に大きなファイルをホストする場合は、Windows PowerShell で次のパラメーターを使用して、 **Format Volume**コマンドレットを使用します。

|パラメーター|説明|
|---|---|
|-AllocationUnitSize 64 KB|64 KB の NTFS アロケーションユニットサイズを設定します。|
|-UseLargeFRS|大きなファイルレコードセグメント (FRS) のサポートを有効にします。 これは、ボリューム上のファイルごとに許可されるエクステントの数を増やすために必要です。 大きな FRS レコードの場合、制限は約150万エクステントから約600万エクステントに増えます。|

たとえば、次のコマンドレットは、FRS が有効でアロケーションユニットサイズが 64 KB の NTFS ボリュームとしてドライブ D をフォーマットします。

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

**Format**コマンドを使用することもできます。 システムのコマンドプロンプトで、次のコマンドを入力します。 **/l**は、大きな FRS ボリュームをフォーマットし、 **/a: 64K**は 64 KB のアロケーションユニットサイズを設定します。

```PowerShell
format /L /A:64k
```

### <a name="maximum-file-name-and-path"></a>最大ファイル名とパス

NTFS では、長いファイル名と拡張パスがサポートされており、最大値は次のとおりです。

- **長いファイル名のサポート。旧バージョンとの互換性のために、** NTFS では長いファイル名が許可されており、ファイル名と拡張子に8.3 の制限が適用されるファイルシステムとの互換性を確保するために、8.3 エイリアス (Unicode) がディスクに格納されています。 必要に応じて (パフォーマンス上の理由から)、windows Server 2008 R2、Windows 8、および Windows オペレーティングシステムの最新バージョンで、個々の NTFS ボリュームで8.3 のエイリアスを選択的に無効にすることができます。
  Windows Server 2008 R2 以降のシステムでは、ボリュームがオペレーティングシステムを使用してフォーマットされている場合、短い名前は既定で無効になっています。 アプリケーションの互換性のために、システムボリュームで短い名前が引き続き有効になります。

- **拡張長パスのサポート**—多くの Windows API 関数には、最大\_パス設定で定義されている260文字のパス制限を超える、約32767文字の拡張長パスを許可する Unicode バージョンが用意されています。 ファイル名とパス形式の詳細な要件、および拡張パスを実装するためのガイダンスについては、「[ファイル、パス、および名前空間の名前付け](https://msdn.microsoft.com/library/windows/desktop/aa365247)」を参照してください。

- **クラスター化**された記憶域—フェールオーバークラスターで使用する場合、NTFS は、クラスターの共有ボリューム (CSV) ファイルシステムと組み合わせて使用するときに、複数のクラスターノードから同時にアクセスできる継続的に使用可能なボリュームをサポートします。 詳細については、「[フェールオーバークラスターでクラスターの共有ボリュームを使用する](../../failover-clustering/failover-cluster-csvs.md)」を参照してください。

### <a name="flexible-allocation-of-capacity"></a>容量の柔軟な割り当て

ボリューム上の領域が制限されている場合、NTFS はサーバーの記憶域容量を操作するための次の方法を提供します。

- ディスククォータを使用して、個々のユーザーの NTFS ボリュームでのディスク領域の使用状況を追跡および制御します。
- ファイルシステムの圧縮を使用して、格納できるデータの量を最大化します。
- 同じディスクまたは別のディスクから未割り当て領域を追加して、NTFS ボリュームのサイズを増やします。
- ドライブ文字が不足している場合、または既存のフォルダーからアクセスできる追加の領域を作成する必要がある場合は、ローカル NTFS ボリューム上の空のフォルダーにボリュームをマウントします。

## <a name="additional-information"></a>追加情報

- [ReFS および NTFS のクラスターサイズに関する推奨事項](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Cluster-size-recommendations-for-ReFS-and-NTFS/ba-p/425960)
- [弾力性ファイルシステム (ReFS) の概要](../refs/refs-overview.md)
- [NTFS の新機能](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))(Windows Server 2012 R2)
- [NTFS の新機能](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff383236(v=ws.10))(Windows Server 2008 R2、Windows 7)
- [NTFS の正常性と Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))
- [自己復旧型の NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))(Windows Server 2008 で導入)
- [トランザクション NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10))(Windows Server 2008 で導入)
- [Windows Server の記憶域](../storage.md)