---
title: サーバー パフォーマンス アドバイザー パック開発ガイド
description: サーバー パフォーマンス アドバイザー パック開発ガイド
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cdf812f862534ba8cd07d4558e424faf3c56c699
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75947144"
---
# <a name="server-performance-advisor-pack-development-guide"></a>サーバー パフォーマンス アドバイザー パック開発ガイド

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 8、Windows 10

この開発ガイド Microsoft Server Performance Advisor (SPA) には、サーバーのパフォーマンスを分析するには、開発者やシステム管理者が advisor パックを開発するためのガイドラインを提供します。

これは、パフォーマンス ログと警告 (PLA)、パフォーマンス カウンター、レジストリ設定、Windows Management Instrumentation (WMI)、Event Tracing for Windows (ETW)、および TRANSACT-SQL (T-SQL) に慣れていると仮定します。

詳細については、SPA を使用して、次を参照してください。 [サーバー パフォーマンス アドバイザー ユーザー ガイド](server-performance-advisor-users-guide.md)します。

## <a name="spa-advisor-pack-overview"></a>SPA Advisor パックの概要


Advisor パックは、通常、特定のサーバーの役割を設計し、次を定義します。

* Windows Management Instrumentation (WMI)、パフォーマンス カウンター、レジストリ設定、ファイル、および Event Tracing for Windows (ETW) を含む PLA から収集されるデータ

* ルールで、アラートと推奨事項を示しています。

* (収集された生データ、集計データ、またはトップ 10 リスト) に表示されるデータ

* 時間の経過と共に変化する値を表示する統計情報

* 傾向できる統計値

Advisor パックには、次の要素が含まれています。

* **XML メタデータ** (ProvisionMetadata.xml)

    * [パフォーマンス ログと警告 (PLA)](https://msdn.microsoft.com/library/windows/desktop/aa372635.aspx) データ コレクター セット

    * レポートのレイアウト

* **SQL スクリプト**

    * 主なストアド プロシージャ

    * ストアド プロシージャおよびユーザー定義関数などの SQL オブジェクト

* **ETW スキーマファイル**(schema. man) これは省略可能です。

### <a name="advisor-pack-workflow"></a>Advisor パックのワークフロー

![advisor パックのワークフロー](../media/server-performance-advisor/spa-dev-guide-workflow.png)

このフローチャートでは、緑色の円は、advisor パックを表します。 その他のすべてのマークは、SPA フレームワーク プロセスで実行している段階を表します。 SPA では、advisor パックを使用して、データを収集、データベースにデータをインポート、実行環境の初期化、および SQL スクリプトを実行します。

### <a name="collect-data"></a>データを収集します。

Advisor パックは、SPA を使用して、特定のサーバーのキューに置かれた、データ収集モジュールは Advisor パックからのデータ コレクター セット XML クエリを実行し、ターゲット サーバーからデータを収集します。 生データは、ユーザー指定のファイル共有に保管されます。 SPA の実行ユーザーが指定されている時間が経過するまで、データの収集は停止されません。

### <a name="import-data-into-the-database"></a>データをデータベースにインポートする

データの収集が完了した後、各種類のデータは、SQL Server データベースに対応するテーブルにインポートされます。 たとえば、レジストリ設定は \#registryKeys という名前のテーブルにインポートされます。

ETW ファイルをインポートするには、.etl ファイルをデコードするための ETW スキーマファイルが必要です。 ETW のスキーマ ファイルは、XML ファイルです。 それは、Windows に含まれている、tracerpt.exe を使用して生成できます。 ETW のスキーマ ファイルはのみ advisor パックは、ETW データをインポートする必要がある場合は必須です。

### <a name="switch-to-low-user-rights"></a>権限の低いユーザーに切り替える

SPA フレームワークは、自動的に必要なセキュリティ アクセス レベルを最小化するには特権を調整します。 Advisor パックを開発したり、すべてのユーザーによって変更できる、ので、改ざんされた SQL スクリプトを格納する、advisor パック可能性があります。 セキュリティ上のリスクを軽減するためには、低い特権で advisor パック用のすべての SQL スクリプトを実行してください。 一時テーブルおよびストアド プロシージャとして公開されている SPA Api などの限られたデータベース オブジェクトにのみアクセスできます。 Advisor パック内の SQL スクリプトは、これらを呼び出すことができます、SPA フレームワークと対話するプロシージャを保存します。

### <a name="initialize-execution-environment"></a>実行環境を初期化します。

Advisor パックには、さまざまな種類の通知、推奨事項、ファクト テーブル、統計、および統計をグラフなどの出力を生成できます。 SQL スクリプトは、収集されたデータに対して特定の計算を実行します。 返された結果は、SPA のパブリック Api を使用して一時テーブルに格納されます。 初期化段階では、これらの一時テーブルおよびその他のシステムリソースをプロビジョニングする必要があります。

### <a name="run-sql-scripts"></a>SQL スクリプトを実行します。

Advisor パックの開発者によって命名される主なストアド プロシージャがあります。 SPA フレームワークでは、計算を開始するこのストアド プロシージャを呼び出します。 ストアド プロシージャは、収集したデータを処理し、SPA フレームワークに、最終的な結果を通信します。

### <a name="switch-to-administrative-rights"></a>管理権限を切り替える

レポートを生成するには、管理者権限が必要です。 レポートの生成は、SPA によって完全に制御されます。 改ざんしにくくなります。

### <a name="generate-a-report"></a>レポートを生成します

主なストアド プロシージャは、advisor パックを完了すると、前にすべての計算結果、通知などの統計は保持されません。 このフェーズでは、SPA フレームワークは、一時テーブルから、最終的な結果を特定の形式でテーブルに転送します。 このフェーズが完了した後は、SPA コンソールを使用してレポートを表示することができます。

## <a name="authoring-an-advisor-pack"></a>Advisor パックの作成


### <a name="quick-guidelines"></a>クイック ガイドライン

次のフローチャートは、完全に機能の advisor パックを開発するための手順を説明します。 このセクションでは、良い各手順を説明する手順を追って例も含まれます。

![advisor パック開発プロセス](../media/server-performance-advisor/spa-dev-guide-dev-flowchart.png)

Advisor パックは、通常次のように構成されています。

Advisor パック

ProvisionMetadata.xml

スクリプト

main.sql

func.sql

Schema.man

すべての advisor パック ProvisionMetadata.xml という名前のファイルが必要です。 基本的な advisor パックについては、データを収集、通知、ルール、およびレポートがどのように格納され、表示する必要がありますを定義します。 SPA フレームワークでは、この情報を使用して、一時テーブルを生成し、ユーザーがアクセスできるテーブルに、一時テーブルに結果を転送します。

すべてのレポートの SQL スクリプトは、という名前のサブフォルダーに保存する必要があります **スクリプト**します。 メンテナンスの目的で、別のデータベース オブジェクトは、SQL Server の異なるファイルに保存することをお勧めします。 メイン エントリ ポイントとして、少なくとも 1 つのストアド プロシージャが必要があります。

> [!NOTE]
> Advisor パックは、ETW トレースを収集しない限り、schema.man ファイルは必要ありません。 このスキーマ ファイルを使用するは、ETW イベントのスキーマを記述して、ETW イベントをデコードします。

### <a name="defining-basic-information"></a>基本的な情報を定義します。

このセクションでは、いくつかの ProvisionMetadata.xml や属性など、advisor パックを構成する基本的な要素について説明します。

ProvisionMetadata.xml ファイルのヘッダーの例を次に示します。

``` syntax
<advisorPack
xmlns="https://microsoft.com/schemas/ServerPerformanceAdvisor/ap/2010"
name="Microsoft.ServerPerformanceAdvisor.CoreOS.V2"
displayName="Microsoft CoreOS Advisor Pack V2"
description="Microsoft CoreOS Advisor Pack"
author="Microsoft"
version="1.0"
frameworkversion="3.0"
minOSversion="6.0"
reportScript="ReportScript">
</advisorPack>
```

### <a name="advisor-pack-version"></a>Advisor パックのバージョン

属性名:**バージョン**

Advisor パック開発者は、advisor パックのメジャーおよびマイナーのバージョンを定義できます。

* 通常、メジャー バージョンには、大幅に改善が含まれます。 古いバージョンで生成される結果は、新しい互換性がない可能性があります。 Advisor パックの名前のメジャー バージョンを含むを強くお勧めします。

* SPA によりデータの非互換性の問題はなくマイナー変更のみがある場合に、マイナー バージョン アップグレードできます。

バージョン管理の詳細については、「[高度なトピック](#bkmk-advancedtopics)」を参照してください。

### <a name="script-entry-point"></a>スクリプトのエントリ ポイント

属性名: **Reportscript**

SPA フレームワークでは、スクリプトのエントリ ポイントから主なストアド プロシージャ名を検索して、セキュリティで保護された方法で実行します。

### <a name="other-attributes"></a>その他の属性

Advisor パックを識別するために使用できるその他のいくつかの属性を次に示します。

* 表示名: **displayName**

* 説明: **の説明**

* 執筆者: **作成者**

* Framework のバージョン: **frameworkversion** (既定値は 3.0)

* オペレーティングシステムの最小バージョン: **Minosversion** (これは将来の拡張のために予約されています)

* イベント通知を紛失: **showEventLostWarning**

### <a href="" id="bkmk-definedatacollector"></a>データコレクターセットの定義

データ コレクター セットでは、SPA フレームワークがターゲット サーバーから収集するパフォーマンス データを定義します。 レジストリ設定、WMI、パフォーマンス カウンターをサポートしている、ETW、ターゲット サーバーからファイルをします。

``` syntax
<advisorPack>
<dataSourceDefinition xmlns="https://microsoft.com/schemas/ServerPerformanceAdvisor/dc/2010">
 <dataCollectorSet duration="10">
<registryKeys>
 ?<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\\</registryKey>
</registryKeys>
<managementpaths>
 ?<path>Root\Cimv2:select * FROM Win32_DiskDrive</path>
</managementpaths>
<performanceCounters interval="2">
 ?<performanceCounter>\PhysicalDisk(*)\Avg. Disk sec/Transfer</performanceCounter>
</performanceCounters>
<files>
 ?<path>%windir%\System32\inetsrv\config\applicationHost.config</path>
</files>
<providers>
 ?<provider session="NT Kernel Logger" guid="{9E814AAD-3204-11D2-9A82-006008A86939}" keywordsany="06010201" keywordsAll="00000000" level="00000000" />
</providers>
 </dataCollectorSet>
</dataSourceDefinition>
</advisorPack>
```

**期間** の属性 **&lt;dataCollectorSet/&gt;** 前の例では、(時間の単位は秒) データ コレクションの継続時間を定義します。 **期間** は必須の属性です。 この設定は、パフォーマンス カウンター、および ETW によって使用されるコレクション期間を制御します。

### <a name="collect-registry-data"></a>レジストリ データを収集します。

次のレジストリ ハイブからレジストリ データを収集できます。

* HKEY\_クラス\_ルート

* HKEY\_現在の\_構成

* HKEY\_現在の\_ユーザー

* HKEY\_ローカル\_マシン

* HKEY\_ユーザー

レジストリ設定を収集するには、値の名前を完全なパスを指定します HKEY\_ローカル\_マシン\\MyKey\\プロパティ。

レジストリキーの下にあるすべての設定を収集するには、レジストリキーの完全なパスを指定します。 HKEY\_LOCAL\_MACHINE\\MyKey\\

レジストリキーとそのサブキーの下にあるすべての値 (PLA によってレジストリデータを収集する) を収集するには、最後のパス区切り記号として2つの円記号を使用します。 HKEY\_LOCAL\_MACHINE\\MyKey\\\\

をリモート コンピューターからのレジストリ情報を収集するには、レジストリ パスの先頭にあるコンピューター名を含める: HKEY\_ローカル\_マシン\\MyKey\\プロパティ

たとえば、次のように表示されるレジストリ キーがあります。

``` syntax
Windows registry editor version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes]
"activePowerScheme"="db310065-829b-4671-9647-2261c00e86ef"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\db310065-829b-4671-9647-2261c00e86ef]
"Description"=
 FriendlyName = Power Source Optimized 

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\db310065-829b-4671-9647-2261c00e86ef \0012ee47-9041-4b5d-9b77-535fba8b1442\6738e2c4-e8a5-4a42-b16a-e040e769756e
"ACSettingIndex"=dword:000000b4
"DCSettingIndex"=dword:0000001e
```

例 1:、アクティブな PowerSchemes のみとその値が返されます。

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes</registryKey>
```

例 2:、このパスのすべてのキー値のペアが返されます。

> [!NOTE]
> PLA は、ユーザーの資格情報で実行されます。 一部のレジストリ キーでは、管理者の資格情報が必要です。 列挙体は、下位のキーのいずれかのアクセスに失敗した場合は停止します。

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\\</registryKey>
```

収集したすべてのデータは、SQL レポートスクリプトを実行する前に、 **\#registryKeys**という一時テーブルにインポートされます。 次の表は、たとえば 2 の結果を示しています。

キー名 | KeytypeId | Value
------ | ----- | -------
HKEY_LOCAL_MACHINE。 ..\PowerSchemes | 1 で保護されたプロセスとして起動されました | db310065-829b-4671-9647-2261c00e86ef
\db310065-829b-4671-9647-2261c00e86ef\Description | 2 で保護されたプロセスとして起動されました | |
\db310065-829b-4671-9647-2261c00e86ef\FriendlyName | 2 で保護されたプロセスとして起動されました | 最適化の電源
...\6738e2c4-e8a5-4a42-b16a-e040e769756e\ACSettingIndex | ホーム フォルダーが置かれているコンピューターにアクセスできない | 180
...\6738e2c4-e8a5-4a42-b16a-e040e769756e\DCSettingIndex | ホーム フォルダーが置かれているコンピューターにアクセスできない | 30

**#RegistryKeys**テーブルのスキーマは、次のようになります。

列名 | SQL データ型 | 説明
-------- | -------- | --------
キー名 | NULL でない Nvarchar(300) | レジストリ キーの完全なパス名
KeytypeId | NULL でない Smallint | 内部型 Id
Value | Nvarchar (4000) NULL でないです。 | すべての値

**Keytypeid**列には、次のいずれかの型を使用できます。

ID | タスクバーの検索ボックスに
--- | ---
1 で保護されたプロセスとして起動されました | String
2 で保護されたプロセスとして起動されました | expandString
3 で保護されたプロセスとして起動されました | バイナリ
ホーム フォルダーが置かれているコンピューターにアクセスできない | DWord
5 | DWordBigEndian
6 | [リンク]
7 | MultipleString
8 | Resourcelist
9 | FullResourceDescriptor
10 | ResourceRequirementslist
11 | Qword

### <a name="collect-wmi"></a>WMI を収集します。

任意の WMI クエリを追加することができます。 WMI クエリの作成方法の詳細については、次を参照してください。 [WQL (WMI 用の SQL)](https://msdn.microsoft.com/library/windows/desktop/aa394606.aspx)します。次の例では、ページのファイルの場所を照会します。

``` syntax
<path>Root\Cimv2:select * FROM Win32_PageFileUsage</path>
```

上記の例では、クエリには、1 つのレコードが返されます。

キャプション | 名前 | PeakUsage
----- | ----- | -----
C:\pagefile.sys | C:\pagefile.sys | 215

WMI で収集したデータがデータベースにインポートすると、別の列を持つテーブルを返すため、SPA はデータの正規化を実行し、次の表を追加します。

**\#の Wmi オブジェクトテーブル**

SequenceID | 名前空間 | クラス名 | Relativepath | WmiqueryID
----- | ----- | ----- | ----- | -----
10 | Root \cimv2 | Win32_PageFileUsage | Win32_PageFileUsage.Name=<br>C:\\pagefile.sys | 1 で保護されたプロセスとして起動されました

**\#の Wmi プロパティの一覧表**

ID | クエリ
--- | ---
1 で保護されたプロセスとして起動されました | Root\Cimv2: select * FROM Win32_PageFileUsage

**\#の Wmi クエリテーブル**

ID | クエリ
--- | ---
1 で保護されたプロセスとして起動されました | Root\Cimv2: select * FROM Win32_PageFileUsage

**\#の Wmi オブジェクトテーブルスキーマ**

列名 | SQL データ型 | 説明
--- | --- | ---
SequenceId | Int 型の NULL でないです。 | 行とそのプロパティを関連付ける
名前空間 | NULL でない nvarchar (200) | WMI 名前空間
クラス名 | NULL でない nvarchar (200) | WMI クラスの名前
Relativepath | NULL でない nvarchar (500) | WMI の相対パス
WmiqueryId | Int 型の NULL でないです。 | #WmiQueries のキーを関連付ける

**\#の Wmi Objectproperties テーブルスキーマ**

列名 | SQL データ型 | 説明
--- | --- | ---
SequenceId | Int 型の NULL でないです。 | 行とそのプロパティを関連付ける
名前 | NULL でない nvarchar (1000) | プロパティ名
Value | Nvarchar (4000) NULL | 現在のプロパティの値

**\#の Wmi クエリテーブルスキーマ**

列名 | SQL データ型 | 説明
--- | --- | ---
ID | Int 型の NULL でないです。 | > 一意のクエリ ID
クエリ | Nvarchar (4000) NULL でないです。 | プロビジョニングのメタデータ内の元のクエリ文字列

### <a name="collect-performance-counters"></a>パフォーマンス カウンターを収集します。

パフォーマンスカウンターを収集する方法の例を次に示します。

``` syntax
<performanceCounters interval="1">
  <performanceCounter>\PhysicalDisk(*)\Avg. Disk sec/Transfer</performanceCounter>
</performanceCounters>
```

**間隔** 属性は、すべてのパフォーマンス カウンターの場合は、必要なグローバル設定です。 パフォーマンス データを収集間隔 (時間の単位は秒) を定義します。

前の例では、counter \\PhysicalDisk (\*)\\Avg. Disk sec/Transfer に対して1秒ごとにクエリが実行されます。

2 つのインスタンスが存在する可能性があります: **\_合計** と **0 の c: d:** , 、出力は次のようとします。

timestamp | [区分名] | CounterName | _Total のインスタンスの値 | インスタンスの値の 0 の c: d:
---- | ---- | ---- | ---- | ----
13:45: 52.630 | PhysicalDisk | 1 秒間のディスク転送の平均 | 0.00100008362473995 |0.00100008362473995
13:45: 53.629 | PhysicalDisk | 1 秒間のディスク転送の平均 | 0.00280023414927187 | 0.00280023414927187
13:45: 54.627 | PhysicalDisk | 1 秒間のディスク転送の平均 | 0.00385999853230048 | 0.00385999853230048
13:45: 55.626 | PhysicalDisk | 1 秒間のディスク転送の平均 | 0.000933297607934224 | 0.000933297607934224

という名前のテーブルにデータをデータベースにインポートするデータを正規化する **\#PerformanceCounters**します。

CategoryDisplayName | インスタンス名 | CounterdisplayName | Value
---- | ---- | ---- | ----
PhysicalDisk | _Total | 1 秒間のディスク転送の平均 | 0.00100008362473995
PhysicalDisk | 0 の C: D: | 1 秒間のディスク転送の平均 | 0.00100008362473995
PhysicalDisk | _Total | 1 秒間のディスク転送の平均 | 0.00280023414927187
PhysicalDisk | 0 の C: D: | 1 秒間のディスク転送の平均 | 0.00280023414927187
PhysicalDisk | _Total | 1 秒間のディスク転送の平均 | 0.00385999853230048
PhysicalDisk | 0 の C: D: | 1 秒間のディスク転送の平均 | 0.00385999853230048
PhysicalDisk | _Total | 1 秒間のディスク転送の平均 | 0.000933297607934224
PhysicalDisk | 0 の C: D: | 1 秒間のディスク転送の平均 | 0.000933297607934224

**メモ** **カテゴリ displayname**や**counterdisplayname**などのローカライズされた名前は、対象サーバーで使用されている表示言語によって異なります。 言語に依存しない advisor パックを作成する場合は、これらのフィールドを使用しないでください。

**\#PerformanceCounters** テーブル スキーマ

列名 | SQL データ型 | 説明
---- | ---- | ---- | ----
timestamp | datetime2 (3) NOT NULL | UNC で収集された日付時刻
[区分名] | NULL でない nvarchar (200) | ［カテゴリ名］
CategoryDisplayName | NULL でない nvarchar (200) | ローカライズされたカテゴリ名
インスタンス名 | NULL nvarchar (200) | ［インスタンス名］
CounterName | NULL でない nvarchar (200) | カウンター名
CounterdisplayName | NULL でない nvarchar (200) | ローカライズされたカウンター名
Value | NULL でない浮動小数点数 | 収集された値

### <a name="collect-files"></a>[ファイルの収集]

パスには、絶対または相対パスを指定できます。 ファイル名がワイルドカード文字を含めることができます (\*)、疑問符 (?)。 たとえば、一時フォルダー内のすべてのファイルを収集するには、c:\\temp\\\*を指定します。 ワイルドカード文字は、指定したフォルダー内のファイルに適用されます。

指定したフォルダーのサブフォルダーからもファイルを収集する場合は、最後のフォルダーの区切り記号に2つの円記号を使用します。たとえば、「c:\\temp\\\\\*」と入力します。

**Applicationhost.config**ファイルに対してクエリを実行する例を次に示します。

``` syntax
<path>%windir%\System32\inetsrv\config\applicationHost.config</path>
```

という名前のテーブルに結果が見つかりません **\#ファイル**, など。

querypath | Fullpath | Parentpath | FileName | コンテンツ
----- | ----- | ----- | ----- | -----
%windir%\..\applicationHost.config |C:\Windows<br>\...\applicationHost.config | C:\Windows<br>\...\config | 構成する | 0x3C3F78

**\#Files テーブルスキーマ**

列名 | SQL データ型 | 説明
---- | ---- | ----
querypath | NULL でない Nvarchar(300) | 元のクエリ ステートメント
Fullpath | NULL でない Nvarchar(300) | 絶対ファイル パスとファイル名
Parentpath | NULL でない Nvarchar(300) | ファイルのパス
FileName | NULL でない Nvarchar(300) | ［ファイル名］
コンテンツ | Varbinary (max) NULL | バイナリ ファイルの内容

### <a name="defining-rules"></a>ルールを定義します。

十分なデータは、ターゲット サーバーからプラットフォームを使用して、収集される、Advisor パックは検証の場合、このデータを使用し、システム管理者に、簡単な概要を表示します。

ルールを使うと、サーバーのパフォーマンスに関する概要を簡単に知ることができます。 これらは、問題を選択し、推奨事項を提供します。 Advisor パックを検証するすべてのルールを一覧表示できます。 たとえば、コア オペレーティング システムの advisor パックを開発する場合は、可能なルールが考えられます。

* CPU の電源モードかどうかは、省電力

* 仮想化環境でサーバーが

* ディスク I/O の負荷があるかどうか

ルールは、次の要素を含めます。

* 依存するしきい値 (構成可能なルールの一部)

* ルールの定義 (通知と推奨事項)

単純なルールの例を次に示します。

``` syntax
<advisorPack>

  <reportDefinition>
    <thresholds>
      <threshold  />
    </thresholds>
    <rules>
      <rule  />
      </rule>
    </rules>
  </reportDefinition>
</advisorPack>
```

### <a name="threshold"></a>しきい値

しきい値は、システム管理者が適切では、または状態が無効で、ルールを表示すると判断できるようにする構成可能な要素です。 次の例は、空き領域が 10 GB 未満の場合は、システム ドライブと、警告の空き領域を検出する規則を示しています。

``` syntax
<threshold name="freediskSize" caption="Free Disk Size (GB)" description="Free Disk Size  value="10" />
```

ただし、この場合、システム管理者がより小さなハード ドライブです。 彼は、5 GB の空き領域がまだ、良好な状態になって、彼は避けたい警告が表示されると認識します。 Advisor パックを開発する方法を理解しなくても彼は、SPA コンソールを 5 に 10 から既定値を更新できます。

しきい値の概要には、advisor パックを変更する必要なく、値を簡単に変更するシステム管理者が利用できます。

例では、すべての属性を除く **説明** が必要です。 任意の数を使用する **値**です。

しきい値は、ルール間で共有できます。

### <a name="alerts-and-recommendations"></a>アラートと推奨事項

ルールの定義では、任意のロジックの計算は発生しません。 UI が検索する方法を定義し、UI に結果を通信する SQL Server がスクリプトを報告する方法です。

ルールには、3 つの部分があります。

* アラート (ルール キャプション)

* 推奨事項 (通知)

* 関連するしきい値 (省略可能な依存関係の情報)

ルールの例を次に示します。

``` syntax
<rule name="freediskSize" caption="Free Disk Size on System Drive" description="This rule checks free disk size on system drive ">
<advice name="SuccessAdvice" level="Success" message="No issue found.">No Recommendation.</advice>
<advice name="WarningAdvice" level="Warning" message="Not enough free space on system drive.">
Install OS on larger disk.</advice>
<dependencies>
 <threshold ref="freediskSize"/>
</dependencies>
</rule>
```

多くのアドバイスをするし、通常の推奨事項を定義しますを定義できます。 **レベル** アドバイスのできるは **成功** または **警告**します。

必要な数のしきい値にリンクすることができます。 現在のルールに関連するしきい値をリンクすることもできます。 リンクのしきい値を簡単に管理する SPA コンソールに役立ちます。

ルールの名前と推奨事項は、キーとが自分のスコープで一意です。 2 つの規則ではありませんが、同じ名前を持つし、1 つのルールに含まれる 2 つの推奨事項はありませんが同じ名前を付けることができます。 これらの名前は、SQL スクリプトレポートを作成するときに非常に重要になります。 呼び出すことができます、 \[dbo\].\[SetNotification\] ルールの状態を設定する API。

### <a name="defining-ui-display-elements"></a>UI の表示要素を定義します。

規則を定義したら、システム管理者は、レポートの概要を表示できます。 ただし、集計データに関心のある多くの場合、システム管理者を対象とするパフォーマンス ルールで使用されていたデータ ソースを確認します。

先ほどの前の例と、ユーザーは、システム ドライブに十分な空きディスク領域があるかどうかを認識します。 ユーザーは、空き領域の実際のサイズにも利用可能性があります。 1 つの値グループを使用して、保存してそのような結果を表示します。 複数の単一の値をグループ化され SPA コンソールでの表に示すことができます。 テーブルでは、次のように名前と値を 2 つの列があります。

名前 | Value
---- | ----
システム ドライブ (GB) の空きディスク サイズ | 100
インストールされているディスクの合計サイズ (GB) | 500 

サーバーにインストールされているすべてのハードドライブとそのディスクサイズの一覧を表示するには、次に示すように、3つの列と複数の行を含むリスト値を呼び出すことができます。

Disk | 空きディスク サイズ (GB) | 合計サイズ (GB)
---- | ---- | ----
0 | 100 | 500
1 で保護されたプロセスとして起動されました | 20 | 320

Advisor パックでは、多数のテーブル (単一の値のグループと値のテーブルを一覧表示) が存在することもできます。 整理およびこれらのテーブルを分類するセクションを使用できます。

要約すると、3 種類の UI 要素があります。

* [セクション](#bkmk-ui-section)

* [単一の値のグループ](#bkmk-ui-svg)

* [値テーブルの一覧表示](#bkmk-ui-lvt)

UI 要素を示す例を次に示します。

``` syntax
<advisorPack>
<dataSourceDefinition/>
<reportDefinition>
 <datatypes>
<datatype .../>
 </datatypes>
 <thresholds/>
 <rule/>
 <sections>
<section .../>
 </sections>
 <singleValues>
<singleValue .../>
 </singleValues>
 <listValues>
<listValue .../>
 </listValues>
</reportDefinition>
</advisorPack>
```

### <a href="" id="bkmk-ui-section"></a>各項

セクションでは、UI レイアウトの純粋にします。 論理計算では参加しません。 各 1 つのレポートには、一連親セクションがない最上位レベルのセクションにはが含まれています。 最上位レベルのセクションでは、レポート内のタブとして表示されます。 セクションには、サブセクションでは、最大 10 レベルまでのことができます。 拡張可能な領域では、最上位レベルのセクションでは、すべてのサブセクションが表示されます。 セクションには、複数のサブセクションで、1 つの値のグループ、および値のテーブルの一覧を含めることができます。 テーブルとしては、1 つの値のグループと値のテーブルの一覧が表示されます。

最上位のセクションの例を次に示します。

``` syntax
<section name="CPU" caption="CPU"/>
```

セクション名は一意である必要があります。 その他のセクションでは、単一の値のグループ値のテーブルを一覧表示してリンクできるキーとして使用されます。

次の例は、属性を持つ **親**, 、CPU のセクションを指しているとします。 CPUFacts は、CPU を名前付きセクションの子です。 **親** 前のセクションの名前を参照する必要がありますそれ以外の場合、このループ内で結果ことができます。

``` syntax
<section name="CPUFacts" caption="Facts" parent="CPU"/>
```

次の単一値グループには、属性、 **セクション**, 、および UI 設計が基に、任意のセクションを指すことができます。

``` syntax
<singleValue name="CPUInformation" section="CPUFacts" caption="Physical CPU Information"> </singleValue>
```

### <a name="data-types"></a>データ型

1 つの値のグループとリストの値のテーブルは、異なる種類の文字列、int、float などのデータを含めます。 SQL Server データベースには、これらの値が格納されている、ためデータ プロパティごとに SQL データ型を定義できます。 ただし、SQL データ型を定義することはかなり複雑です。 長さまたは有効桁数を変更しやすい可能性のあるを指定する必要があります。

最初の子を使用する論理データの種類を定義する **&lt;reportDefinition/&gt;** , 、これは、SQL データ型と、論理型のマッピングを定義することができます。

次の例では、2 つのデータ型を定義します。 1 つは、 **文字列** し、もう一方の **companyCode**します。

``` syntax
<datatype name="string" = sqltype="nvarchar(4000)" />
<datatype name="companyCode" sqltype="nvarchar(100)" />
```

データ型の名前には、任意の有効な文字列を指定できます。 許可される SQL データ型の一覧を次に示します。

* bigint 型

* バイナリ

* ビット

* char 型

* 日付

* datetime

* datetime2

* datetimeoffset

* 10 進数

* 浮動小数点数

* 整数

* 収益

* nchar

* 数値

* nvarchar

* real

* smalldatetime

* smallint

* smallmoney

* 時間

* tinyint

* 一意識別子

* varbinary

* varchar

これらの SQL データ型の詳細については、「[データ型 (transact-sql)](https://msdn.microsoft.com/library/ms187752.aspx)」を参照してください。

### <a href="" id="bkmk-ui-svg"></a>単一の値のグループ

1 つの値のグループには、次のように、テーブル内に存在する複数の単一の値がグループ化します。

``` syntax
<singleValue name="Systemoverview" section="SystemoverviewSection" caption="Facts">
<value name="OsName" type="string" caption="Operating system" description="WMI: Win32_OperatingSystem/Caption"/>
<value name="Osversion" type="string" caption="OS version" description="WMI: Win32_OperatingSystem/version"/>
<value name="OsLocation" type="string" caption="OS location" description="WMI: Win32_OperatingSystem/SystemDrive"/>
</singleValue>
```

前の例では、1 つの値のグループを定義しました。 これは、セクション**System概要セクション**の子ノードです。 このグループには、1つの値 ( **OsName**、 **Osversion**、および**oslocation**) があります。

1 つの値は、グローバル一意の名前属性が必要です。 この例では、グローバルな一意の名前属性は**Systemoverview**です。 一意の名前はカスタム レポートの対応するビューの生成に適用されます。 各ビューには、vwSystemoverview などのプレフィックス**vw**が含まれています。

複数の単一の値のグループを定義できますが、別のグループにある場合でも、しない 2 つの単一の値名前が同じを指定できます。 SQL スクリプトのレポートは、単一の値の名前を使用して、値を適宜設定します。

1 つの各値のデータ型を定義できます。 **型**の許可された入力は **&lt;datatype/&gt;** で定義されています。 最終的なレポートは、次のようになります。

**ファクト**

名前 | Value
--- | ---
オペレーティング システム | &lt;_値は、レポートスクリプトによって設定され_&gt;
OS のバージョン | &lt;_値は、レポートスクリプトによって設定され_&gt;
OS の場所 | &lt;_値は、レポートスクリプトによって設定され_&gt;

**キャプション** の属性 **&lt;値/&gt;** は最初の列に表示されます。 [値] 列の値は将来的にによるスクリプト レポートによって設定 \[dbo\].\[SetSingleValue\]します。 **説明** の属性 **&lt;値/&gt;** ツールヒントに表示されます。 通常、ツールヒントは、データのソースのユーザー表示されます。 ツール ヒントの詳細については、次を参照してください。 [ツールヒント](#bkmk-tooltips)します。

### <a href="" id="bkmk-ui-lvt"></a>値テーブルの一覧表示

リストの値を定義すると、テーブルを定義すると同じです。

``` syntax
<listValue name="NetworkAdapterInformation" section="NetworkIOFacts" caption="Physical network adapter information">
<column name="NetworkAdapterId" type="string" caption="ID" description="WMI: Win32_NetworkAdapter/DeviceID"/>
<column name="NetworkAdapterName" type="string" caption="Name" description="WMI: Win32_NetworkAdapter/Name"/>
<column name="type" type="string" caption="type" description="WMI: Win32_NetworkAdapter/Adaptertype"/>
<column name="Speed" type="decimal" caption="Speed (Mbps)" description="WMI: Win32_NetworkAdapter/Speed"/>
<column name="MACaddress" type="string" caption="MAC address" description="WMI: Win32_NetworkAdapter/MACaddress"/>
</listValue>
```

一覧の値の名前をグローバル一意識別にする必要があります。 この名前は、一時テーブルの名前になります。 前の例では、という名前のテーブルで \#NetworkAdapterInformation は実行の環境の初期化ステージで説明されているすべての列を含むに作成されます。 1 つの値名と同様に、リスト値の名前としても使用 vwNetworkAdapterInformation など、カスタム ビュー名の一部です。

&lt;列/&gt; の @type は &lt;datatype/&gt; によって定義されます

最終的なレポートのモックの UI には、次のようになります。

**物理ネットワークアダプターの情報**

ID | 名前 | タスクバーの検索ボックスに | (Mbps) の速度 | MAC アドレス
--- | --- | --- | --- | ---
 | <br> | | |
 | | | |


**キャプション** の属性 &lt;列/&gt; 列名として表示され、 **説明** の属性 &lt;列/&gt; の対応する列ヘッダーのツールヒントとして表示されます。 通常、ツールヒントは、データのソース ユーザー表示されます。 詳細については、次を参照してください。 [ツールヒント](#bkmk-tooltips)します。

場合によっては、テーブルの列が多数あり、行数が少なく、ように列と行のスワップは、テーブルが鮮明に表示します。 列と行をスワップするには、次のスタイル属性を追加できます。

``` syntax
<listValue style="Transpose"  
```

### <a name="defining-charting-elements"></a>グラフ要素の定義

任意の統計情報のキーを選択し、履歴グラフまたはトレンド グラフで値を表示できます。 統計情報の 2 種類があります。

* **静的な統計** がデザイン時にわかっている 1 つの値。 たとえば、システム ドライブの空きディスク領域は、静的な統計情報になります。

* **動的な統計** デザイン時に既知あります。 例、各コアの平均 CPU 使用率は、CPU コアの数がデザイン時に、システムのことがわからないために、動的な統計情報を示します。

統計のキーには、double データ型と互換性のあるデータである必要があります制限があります。 Integer、decimal、または double 型に変換できる文字列を指定できます。

SPA は、静的な統計情報と動的な統計情報をサポートするためにリスト値のテーブルをサポートするのに 1 つの値のグループを使用します。 次のセクションでは、静的な統計と動的な統計のキーを定義する方法について説明します。

### <a name="static-statistics"></a>静的な統計情報

前述のように、静的な統計情報は、単一の値です。 論理的には、任意の 1 つの値は、静的な統計として定義できます。 ただし、数値型にキャストできない 1 つの値を表示しても意味です。 静的な統計情報を定義する属性を単に追加できます **trendable** 対応する 1 つの値をキーに示すように下。

``` syntax
<value name="freediskSize" type="int" trendable="true"  
```

### <a name="dynamic-statistics"></a>動的な統計情報

動的な統計のキーは、使用可能な値の数が不明なため、デザイン時に認識されません。 ただし、複数の行では、リストの値が格納されている、ためになりますを簡単に動的な統計情報を格納するリストの値のテーブルを使用します。

たとえば、さまざまなコアの平均 CPU 使用率のグラフを表示する必要がある場合は、 **CpuId**と**AverageCpuUsage**の列を含むテーブルを定義できます。

``` syntax
<listValue name="CpuPerformance">
<column name="CpuId" type="string" caption="CPU ID" columntype="Key"/>
<column name="AverageCpuUsage" type="decimal" caption="Average" columntype="Value"/>
</listValue>
```

もう1つの属性である**columntype**には、**キー**、**値**、または**情報**を指定できます。 データ型、 **キー** 列を二重にする必要がありますまたは double に変換できます。 **キー**  列をテーブルに同じキーを挿入することはできません。 **値** または **情報** 列には、この制限はありません。

統計の値が格納されている **値** 列です。

**情報** 列は、通常のリストの値のテーブル内の通常の列のようにします。 **情報** 既定の列の種類は、いずれかを指定しない場合。 このような列の統計のキーの数に影響を与えるや統計に関連した計算に参加はできません。

サーバーに 2 つの CPU コアが設定されている場合、前の例を続行して、テーブルの結果はでした次のようになります。

CpuId | AverageCpuUsage
:---: | :---:
0 | 10
1 で保護されたプロセスとして起動されました | 30

同時に 2 つの統計のキーは、SPA フレームワークによって生成されます。 1 つは CPU 0 を CPU 1 のもう 1 つは.

複数の次の例に示す **値** 複数列 **キー** 列をサポートします。

CounterName | インスタンス名 | 平均 | 合計
--- | :---: | :---: | :---:
プロセッサ時間の割合 | _Total | 10 | 20
プロセッサ時間の割合 | CPU0 | 20 | 30 

この例である 2 つ **キー** 列と 2 つ **値** 列です。 SPA は、平均の列の 2 つの統計情報キーと合計列の別の 2 つのキーを生成します。 統計のキーは次のとおりです。

* CounterName (プロセッサ時間の割合)/InstanceName (\_合計)/平均

* CounterName (プロセッサ時間の割合)/InstanceName (CPU0)/平均

* CounterName (プロセッサ時間の割合)/InstanceName (\_合計)/合計

* CounterName (プロセッサ時間の割合)/InstanceName (CPU0)/合計

CounterName とインスタンス名は、1 つのキーとして結合されます。 結合されたキーには、重複を持つことはできません。

SPA は、多くの統計のキーを生成します。 一部の興味深いは、その UI からそれらを非表示にすることがあります。 SPA では、有用な統計情報のキーのみを表示するフィルターを作成することができます。

前の例では、システム管理者は、InstanceName が合計または CPU1 の \_キーのみを対象としている可能性があります。 フィルターは、次のように定義できます。

``` syntax
<listValue name="CpuPerformance">
<column name="CounterName" type="string" columntype="Key"/>
<column name="InstanceName" type="string" columntype="Key">
 <trendableKeyValues>
<value>_Total</value>
<value>CPU1</value>
 </trendableKeyValues>
</column>
<column name="Average" type="decimal" columntype="Value"/>
<column name="Sum" type="decimal" columntype="Value"/>
</listValue>
```

**&lt;trendableKeyValues/&gt;** 任意のキー列の下で定義することができます。 数より多い場合は、1 つのキー列がこのようなフィルターが構成されて、およびロジックが適用されます。

### <a name="developing-report-scripts"></a>レポートのスクリプトの開発

プロビジョニングのメタデータを定義した後は、T-SQL ストアド プロシージャは、レポートのスクリプトの作成を開始しました

ある **名** と **reportScript** 次に示すように、プロビジョニングのメタデータ ヘッダーの属性します。

``` syntax
<advisorPack name="Microsoft.ServerPerformanceAdvisor.CoreOS.V1" reportScript="ReportScript"  
```

結合することでメイン レポート スクリプトの名前は、 **名前** と **reportScript** 属性です。 次の例ではなります \[Microsoft.ServerPerformanceAdvisor.CoreOS.V2\].\[ReportScript\]します。

``` syntax
create PROCEDURE [Microsoft.ServerPerformanceAdvisor.CoreOS.V2].[ReportScript] AS SET NOCOUNT ON

- Set alert and notification

- Prepare data for report view
```

**名前** 属性は、名前空間などのデータベース スキーマ名として使用されます。 このルールは、リスト値やストアド プロシージャなど、現在の advisor パックに属している他のすべてのデータベース オブジェクトに適用されます。

データベース オブジェクトの前にこのスキーマ名を持つことのメリットは次のとおりです。

* 異なる advisor パックの名前の競合を回避します。

* セキュリティ保護を高める

既定のスキーマ名は、SQL Server データベースに **dbo**します。 データベース所有者の資格情報では、下にあるデータベース オブジェクトを操作するために必要な通常 **dbo**します。 Advisor パックごとにスキーマは作成しないと、その 2 つの advisor パックが一覧の値と同じ名前を定義する可能性があります。 これはできません関連するので、この問題を解決するためにスキーマの名前を導入することができます。 さらに、プロビジョニング解除の advisor パックははるかに簡単です。 以外の場合、advisor パック オブジェクトはスキーマに属しているため **dbo**, 、これにより、SPA を低いユーザー特権を使用して、それらにアクセスします。

標準レポートのスクリプトは、次を処理します。

* 生の収集されたデータにアクセス

* 生のデータに基づいて計算を実行します。

* 変更のアラートと推奨事項

* レポート ビューのデータを準備します。

### <a name="access-raw-collected-data"></a>Raw 収集されたデータにアクセス

収集されたすべてのデータは、次の対応するテーブルにインポートされます。 テーブル スキーマの詳細については、次を参照してください。 [データ コレクター セットを定義する](#bkmk-definedatacollector)です。

* レジストリ

    * registryKeys の \#

* WMI に関するページ

    * \#の Wmi オブジェクト

    * \#の Wmi Objectproperties

    * \#の Wmi クエリ

* パフォーマンス カウンター

    * \#PerformanceCounters

* ファイル

    * \#ファイル

* ETW

    * \#イベント

    * \#EventProperties

### <a name="set-rule-status"></a>ルールの状態の設定

\[Dbo\].\[SetNotification\] API のセット、ルールのステータスを表示できるように、 **成功** または **警告** UI のアイコン。

* @ruleName nvarchar (50)

* @adviceName nvarchar (50)

アラートおよび推奨されるメッセージは、プロビジョニングのメタデータ XML ファイルに格納されます。 これにより、レポートのスクリプトの管理が容易にします。

最初に、各ルールの状態は、該当なし。 この API を使用すると、アドバイス名を指定してルールの状態を設定します。 アドバイス名のレベルは、ルールの状態として使用されます。

次の規則を前に定義したことを思い出してください。

``` syntax
<rule name="freediskSize" caption="Free Disk Size on System Drive" description="This rule checks free disk size on the system drive ">
<advice name="SuccessAdvice" level="Success" message="No issue found.">No recommendation.</advice>
<advice name="WarningAdvice" level="Warning" message="Not enough free space on system drive.">Install the operating system on a larger disk.</advice>
</rule>
```

空き領域が 2 GB 未満であると仮定した場合、必要なルールに設定、 **警告** レベルです。 SQL スクリプトは次のようになります。

``` syntax
if (@freediskSizeInGB < 2)
BEGIN
    exec dbo.SetNotification N'freediskSize', N'WarningAdvice'
END
ELSE
BEGIN
    exec dbo.SetNotification N'freediskSize', N'SuccessAdvice'
END 
```

### <a name="get-threshold-value"></a>しきい値の値を取得します。

\[Dbo\].\[GetThreshold\] API がしきい値を取得します。

* @key nvarchar (50)

* @value float の出力

> [!NOTE]
> しきい値は、名前と値のペアと、それらはすべてのルールで参照することができます。 システム管理者は、SPA コンソールを使用して、しきい値を調整します。

 しきい値の前の例を続行定義は次のようになります。

``` syntax
<thresholds>
  <threshold name="freediskSize" caption="Free Disk Size (GB)" description="Free Disk Size  value="10" />
</thresholds>
<rule name="freediskSize" caption="Free Disk Size on System Drive" description="This rule checks free disk size on system drive ">
<advice name="SuccessAdvice" level="Success" message="No issue found.">No recommendation.</advice>
<advice name="WarningAdvice" level="Warning" message="Not enough free space on the system drive.">
Install the operating system on a larger disk.</advice>
<dependencies>
 <threshold ref="freediskSize"/>
</dependencies>
</rule>
```

レポートのスクリプトは、次のように変更できます。

``` syntax
DECLARE @freediskSize FLOat
exec dbo.GetThreshold N freediskSize , @freediskSize output

if (@freediskSizeInGB < @freediskSize)

```

### <a name="set-or-remove-the-single-value"></a>設定または単一の値を削除します。

\[Dbo\].\[SetSingleValue\] API が 1 つの値を設定します。

* @key nvarchar (50)

* @value sql\_variant

この値は、1 つの値の同じキーの複数回を実行できます。 最後の値が保存されます。

次の例では、単一の値が定義されているいくつか示しています。

``` syntax
<singleValue section="Systemoverview" caption="Facts">
<value name="OsName" type="string" caption="Operating System" description="WMI: Win32_OperatingSystem/Caption"/>
<value name="Osversion" type="string" caption="OS version" description="WMI: Win32_OperatingSystem/version"/>
<value name="OsLocation" type="string" caption="OS Location" description="WMI: Win32_OperatingSystem/SystemDrive"/>
</singleValue>
```

次に示すようにし、1 つの値を設定できます。

``` syntax
exec dbo.SetSingleValue N OsName ,  Windows 7 
exec dbo.SetSingleValue N Osversion ,  6.1.7601 
exec dbo.SetSingleValue N OsLocation ,  c:\ 
```

まれに、\[dbo\]を使用して、以前に設定した結果を削除することが必要になる場合があります。\[removeSingleValue\] API。

* @key nvarchar (50)

次のスクリプトを使用するには、以前に設定を削除する値。

``` syntax
exec dbo.removeSingleValue N Osversion 
```

### <a name="get-data-collection-information"></a>データ コレクションの情報を取得します。

\[Dbo\].\[GetDuration\] API は、データ収集の秒単位の期間を指定されたユーザーを取得します。

* @duration int の出力

レポートスクリプトの例を次に示します。

``` syntax
DECLARE @duration int
exec dbo.GetDuration @duration output
```

\[Dbo\].\[GetInternal\] API は、パフォーマンス カウンターの間隔を取得します。 現在のレポートにはパフォーマンス カウンター情報がない場合は、NULL を返すことでした。

* @interval int の出力

レポートスクリプトの例を次に示します。

``` syntax
DECLARE @interval int
exec dbo.GetInterval @interval output
```

### <a name="set-a-list-value-table"></a>リスト値のテーブルを設定します。

値のテーブルを一覧表示を更新するための API はありません。 ただし、値のテーブルの一覧を直接アクセスできます。 初期化段階では、各リスト値に対応する一時テーブルが作成されます。

次の例は、リスト値のテーブルを示しています。

``` syntax
<listValue name="NetworkAdapterInformation" section="NetworkIOFacts" caption="Physical Network Adapter Information">
<column name="NetworkAdapterId" type="string" caption="ID" description="WMI: Win32_NetworkAdapter/DeviceID"/>
<column name="NetworkAdapterName" type="string" caption="Name" description="WMI: Win32_NetworkAdapter/Name"/>
<column name="type" type="string" caption="type" description="WMI: Win32_NetworkAdapter/Adaptertype"/>
<column name="Speed" type="decimal" caption="Speed (Mbps)" description="WMI: Win32_NetworkAdapter/Speed"/>
<column name="MACaddress" type="string" caption="MAC address" description="WMI: Win32_NetworkAdapter/MACaddress"/>
</listValue>
```

挿入、更新、または結果を削除するには、SQL スクリプトを記述できます。

``` syntax
INSERT INTO #NetworkAdapterInformation (
  NetworkAdapterId,
  NetworkAdapterName,
  type,
  Speed,
  MACaddress
)
VALUES (

)
```

## <a name="development-and-debugging"></a>開発とデバッグ


### <a name="writing-logs"></a>ログを書き込み

システム管理者に通知する情報がある場合は、ログを書き込むことができます。 特定のレポートのすべてのログがある場合、レポート ヘッダーに黄色いバナーが表示されます。 次の例では、ログを作成する方法を示しています。

``` syntax
exec dbo.WriteSystemLog N'Any information you want to show to the system administrators , N Warning 
```

最初のパラメーターは、ログに表示するメッセージが表示されます。 2 番目のパラメーターは、ログ レベルです。 2 番目のパラメーターの有効な入力可能性があります **情報**, 、**警告**, 、または **エラー**します。

### <a name="debug"></a>Debug

SPA コンソールを実行できる 2 つのモードでデバッグやリリースします。 リリース モードは、既定では、およびレポートが生成された後、収集された生データはすべてがクリーンアップされます。 デバッグ モードですべての生データ、ファイル共有と、データベースが、将来のレポートのスクリプトをデバッグできます。

**レポートスクリプトをデバッグするには**

1.  Microsoft SQL Server Management Studio (SSMS) をインストールします。

2.  SSMS の起動後に、localhost に接続\\SQLExpress です。 ではなく、localhost を使用する必要があることに注意してください。 の順に移動します。 それ以外の場合、SQL Server で、デバッガーを起動できない可能性がありますできません。

3.  デバッグ モードを有効にするのには、次のスクリプトを実行します。

    ``` syntax
    USE SPADB
    UPdate dbo.Configurations
    SET Value = N'true'
    WHERE Name = N'Debugmode'
    ```

4.  SPA コンソールを起動してデバッグする advisor パックを実行します。

5.  タスクが完了するまで待ちます。 レポートが正常に生成された場合は、SSMS に戻るし、最新のタスクを探します。

    ``` syntax
    select TOP 1 * FROM dbo.Tasks OrdER BY Id DESC
    ```

    たとえば、出力があります。

    ID | セッション Id | AdvisoryPackageId | ReportStatusId | LastUpdatetime | ThresholdversionId
    :---: | :---: | :---: | :---: | :---: | :---:
    12 | 17 | 1 で保護されたプロセスとして起動されました | 2 で保護されたプロセスとして起動されました | 2011-05-11 05:35: 24.387 | 1 で保護されたプロセスとして起動されました

6.  次のスクリプトは、Id 12 のレポートのスクリプトを実行する回数だけ実行できます。

    ``` syntax
    exec dbo.DebugReportScript 12
    ```

    **メモ**F11 キーを押して、前のステートメントにステップインし、デバッグすることもできます。



実行している \[dbo\].\[DebugReportScript\] など、複数の結果セットを返します。

1.  Microsoft SQL Server のメッセージと advisor パック ログ

2.  ルールの結果

3.  統計のキーと値

4.  単一の値

5.  すべてのテーブルな一覧の値

## <a name="best-practices"></a>ベスト プラクティス

### <a name="naming-convention-and-styles"></a>名前付け規則とスタイル

|                                                                 Pascal 形式の文字種                                                                 |                       camel 規約に従った大文字小文字の使い分け                        |             大文字             |
|-----------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------|-----------------------------------|
| <ul><li>Provisionmetadata.xml の名前</li><li>ストアド プロシージャ</li><li>関数</li><li>ビュー名</li><li>一時テーブル名</li></ul> | <ul><li>パラメーター名</li><li>ローカル変数</li></ul> | すべての SQL 予約キーワードに使用する |

### <a name="other-recommendations"></a>他の推奨事項

* 最も論理部分を他のストアド プロシージャおよびユーザー定義関数に移動します。

* メンテナンスの目的でできるだけ短くして、メイン スクリプトを確認します。

* SQL オブジェクトの完全名を使用します。

* SQL コードは、大文字と小文字を扱います。

* 追加 **SET NOCOUNT ON** すべてのストアド プロシージャの先頭にします。

* 膨大な量のデータを転送する一時テーブルを使用してください。

* 使用を検討して **設定 XACT\_中止に** エラーが発生した場合は、プロセスを終了します。

* 常に advisor パックの表示名にメジャー バージョン番号が含まれます。

## <a href="" id="bkmk-advancedtopics"></a>高度なトピック

### <a name="run-multiple-advisor-packs-simultaneously"></a>複数の advisor パックを同時に実行します。

SPA は、同時に複数の advisor パックを実行しているサポートしています。 これは、インターネット インフォメーション サービス (IIS) と同時に中核となるオペレーティング システムのパフォーマンスを確認する場合に特に便利です。 IIS advisor パックによって使用されている多くのデータ コレクターは、コア OS advisor パックによっても使用可能性があります。 複数の Advisor パックが同じターゲット コンピューターで実行されている場合、SPA は同じデータを 2 回収集することはありません。

次の例では、2 つの advisor パックを実行するためのワークフローを示します。

![複数の advisor パックを実行しています。](../media/server-performance-advisor/spa-dev-guide-multi-advisor-packs.png)

合併データ コレクター セットは、パフォーマンス カウンターと ETW のデータ ソースを収集するためだけです。 次の結合規則が適用されます。

1. SPA には、最大期間は新しい実行時間がかかります。

2. マージ競合がある場合、次の規則が適用されます。

   1. 新しい間隔として最短の間隔を取得します。

   2. パフォーマンス カウンターのスーパー セットを考慮します。 たとえば、 **process (\*)\\% Processor time** and **process (\*)\\\*、\\process (\*)\\** \\* はさらに多くのデータを返します。そのため、**プロセス (\*)\\% processor time** and **process (\*)** \\\\* はマージされたデータコレクターセットから削除されます。

### <a name="collect-dynamic-data"></a>動的なデータを収集します。

SPA ニーズで定義されているデータ コレクターの設定はデザイン時です。 さらに、動的なデータとクエリ パスは認識されていないため、依存するデータが使用可能になるまでデータがレポートの生成に必要なトピックをできることとは限りません。

たとえば、ネットワークアダプターのすべてのフレンドリ名を一覧表示するには、まず WMI に対してクエリを実行し、すべてのネットワークアダプターを列挙する必要があります。 各返す WMI オブジェクトがレジストリ キーのパスでは、フレンドリ名を格納する場所です。 レジストリ キーのパスは、デザイン時では既知ではありません。 この場合は、動的データ必要をサポートします。

すべてのネットワーク アダプターを列挙するには、Windows PowerShell を使用して以下の WMI クエリを使用できます。

``` syntax
Get-WmiObject -Namespace Root\Cimv2 -query "select PNPDeviceID FROM Win32_NetworkAdapter" | forEach-Object { Write-Output $_.PNPDeviceID }
```

ネットワーク アダプター オブジェクトの一覧を返します。 各オブジェクトと呼ばれるプロパティには **PNPDeviceID**, 、相対的なレジストリ キーのパスを維持します。 前のクエリからのサンプル出力を次に示します。

``` syntax
ROOT\*ISatAP\0001
PCI\VEN_8086&DEV_4238&SUBSYS_11118086&REV_35\4&372A6B86&0&00E4
ROOT\*IPHTTPS\0000

```

**FriendlyName**値を調べるには、レジストリエディターを開き、 **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\** を前のサンプルの各行と組み合わせて、レジストリ設定に移動します。 (例: **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\ ROOT\\\*IPHTTPS\\0000**。

SPA プロビジョニング メタデータには、前の手順を変換するには、次のコード サンプルでは、スクリプトを追加します。

``` syntax
<advisorPack>
<dataSourceDefinition xmlns="https://microsoft.com/schemas/ServerPerformanceAdvisor/dc/2010">
 <dataCollectorSet >
<registryKeys>
 ?<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\$(NetworkAdapter.PNPDeviceID)\FriendlyName</registryKey>
</registryKeys>
<managementpaths>
 ?<path name="NetworkAdapter">Root\Cimv2:select PNPDeviceID FROM Win32_NetworkAdapter</path>
</managementpaths>
```

この例では、まず managementpaths の下に WMI クエリを追加し、キー名**ネットワークアダプター**を定義します。 レジストリ キーを追加しを参照してください **ネットワーク アダプター** 構文を使って **$(NetworkAdapter.PNPDeviceID)** します。

次の表では、SPA 内のデータ コレクターには、動的なデータと他のデータ コレクターによって参照されるかどうかがサポートされている場合を定義します。

［データの種類］ | 動的データをサポートします。 | 参照することができます。
--- | :---: | :---:
レジストリ キー●れじすとり きー○ | [はい] | [はい]
WMI に関するページ | [はい] | [はい]
ファイル | [はい] | 必須ではない
パフォーマンス カウンター | 必須ではない | 必須ではない
ETW | 必須ではない | 必須ではない

WMI のデータ コレクターは、各 WMI オブジェクトは、多くの接続されている属性を持ちます。 すべての種類の WMI オブジェクトには、\_\_名前空間、\_\_クラス、\_\_RELpath の3つの属性があります。

その他のデータ コレクターによって参照されているデータ コレクターを定義するには、割り当て、 **名前** 、ProvisionMetadata.xml 内の一意のキーを持つ属性です。 このキーは、動的なデータを生成する業務用のデータ コレクターによって使用されます。

レジストリキーの例を次に示します。

``` syntax
<registryKey  name="registry">HKEY_LOCAL_MACHINE </registryKey>
```

WMI の例:

``` syntax
<path name="wmi">Root\Cimv2:select PNPDeviceID FROM Win32_NetworkAdapter</path>
```

次の構文の使用に依存するデータ コレクターを定義する: $( *{name}* . *{属性}* )。

*{name}* *{属性}* プレース ホルダーであります。

SPA は、ターゲット サーバーからデータを収集するとき、次のように、パターン $ (\*.\*) を参照データ コレクターから収集した実際のデータ (レジストリ キー/WMI) に動的に置き換えます。

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\$(registry.key)\ </registryKey>
<registryKey  name="registry">HKEY_LOCAL_MACHINE\$(wmi.Relativeregistrypath)\ </registryKey>
<path name="wmi"> </path>
<file>$(wmi.FileName)</file>
```

**メモ**SPA は、無制限の参照をサポートしますが、レベルが多すぎる場合は、パフォーマンスのオーバーヘッドに注意してください。 循環参照がないか、自己参照サポートされていないことを確認してください。

### <a name="versioning-limitations"></a>バージョン管理の制限事項

SPA は、リセットとマイナー バージョン更新プログラムをサポートします。 これらのプロセスでは、同じアルゴリズムを使用します。 プロセスは、すべてのデータベース オブジェクトとしきい値の設定の更新を既存のデータを確保するためです。 これは、新しいバージョンにアップグレードすることができます。 または下位バージョンにダウン グレードします。 advisor パックを選択し、SPA の **[Advisor パックの構成]** ダイアログボックスで **[リセット]** をクリックして、または更新プログラムをリセットまたは適用します。

この機能は、主に小規模な更新です。 UI の表示要素を大幅に変更できません。 大幅に変更する場合は、別の advisor パックを作成する必要です。 Advisor パック名では、メジャー バージョンを含める必要があります。

マイナーバージョンの変更**には、次のような**制限があります。

* スキーマ名を変更する

* 任意の1つの値グループまたはリスト値テーブルの列のデータ型を変更する

* しきい値の追加または削除

* ルールの追加または削除

* アドバイスの追加または削除

* 単一の値を追加または削除する

* リスト値の追加または削除

* リスト値の列を追加または削除する

### <a href="" id="bkmk-tooltips"></a>ツールヒント

ほぼすべて **説明** 属性は、SPA コンソールで、ツールヒントとして表示されます。

リスト値テーブルでは、次の属性を追加することで行ベースのツールヒントを実現できます。

``` syntax
<listValue descriptionColumn="Description">
<column name="Name"/>
<column name="Description"/>
</listValue>
```

**DescriptionColumn** 属性列の名前を参照します。 この例では、[説明] 列は物理的な列としては表示されません。 ただし、表示、ツールヒントとして最初の列の行ごとにマウスを置くとされます。

ツール ヒントが、ユーザーにデータ ソースを表示することをお勧めします。 データ ソースを表示するための形式を次に示します。

[データ ソース] | 表記 | 例
--- | --- | ---
WMI に関するページ | WMI: &lt;wmiclass&gt;/&lt;フィールド&gt; | [WMI] Win32_OperatingSystem/キャプション
パフォーマンス カウンター | Perfcounter: &lt;の区分名&gt;/&lt;InstanceName&gt; | Perfcounter: Process/% Processor time
レジストリ | レジストリ: &lt;registerKey&gt; | レジストリ: HKLM\SOFTWARE\Microsoft<br>\\ASP.NET\\Rootver
［構成ファイル］ | ConfigFile: &lt;Filepath&gt;\[;Xpath: &lt;Xpath&gt;\]<br>**注:**<br>Xpath は省略可能で、ファイルが xml ファイルである場合にのみ有効です。 | ConfigFile: windir%\\System32\\inetsrv\config\\Applicationhost.config<br>Xpath: configuration&frasl;System.webserver<br>&frasl;httpProtocol&frasl;@allowKeepAlive
ETW | ETW: &lt;Provider/&gt;(キーワード) | ETW: Windows カーネル トレース (プロセス、net)

### <a name="table-collation"></a>テーブルの照合順序

Advisor パックが複雑になると、独自の変数のテーブルまたはレポートのスクリプトに中間結果を格納する一時テーブルを作成できます。

文字列型の列の照合問題となる可能性を作成するテーブルの照合順序は、SPA フレームワークによって作成されたものと異なる可能性があるためです。 さまざまなテーブルに 2 つの文字列の列を関連付ける場合は、照合順序のエラーを参照してください可能性があります。 この問題を回避するには、常として列の照合順序の文字列を定義する必要があります **SQL\_Latin1\_全般\_CP1\_CI\_AS** テーブルを定義します。

ここでは、変数テーブルを定義する方法を説明します。

``` syntax
DECLARE @filesIO TABLE (
 Name nvarchar(500) COLLatE SQL_Latin1_General_CP1_CI_AS,
 AverageFileAccessvolume float,
 AverageFileAccessCount float,
 Filepath nvarchar(500) COLLatE SQL_Latin1_General_CP1_CI_AS
)
```

### <a name="collect-etw"></a>ETW を収集します。

Provisionmetadata.xml ファイルに ETW を定義する方法を次に示します。

``` syntax
<dataSourceDefinition>
  <providers>
    <provider session="NT Kernel Logger" guid="{9E814AAD-3204-11D2-9A82-006008A86939}"/>
  </providers>
</dataSourceDefinition>
```

ETW を収集するために使用する次のプロバイダーの属性を紹介します。

備わっている | タスクバーの検索ボックスに | 説明
--- | --- | ---
guid | GUID | プロバイダーの GUID
セッション | string | ETW セッション名 (省略可能のカーネル イベント用にのみ必要)
keywordsany | 16 進数 | 任意のキーワード (省略可能、0 x プレフィックスなし)
keywordsAll | 16 進数 | すべてのキーワード (省略可能)
プロパティ | 16 進数 | (省略可能) のプロパティ
level | 16 進数 | (省略可能) レベル
bufferSize | 整数 | バッファーのサイズ (省略可能)
flushtime | 整数 | (省略可能) 時間をフラッシュします。
maxBuffer | 整数 | 最大バッファー (省略可能)
minBuffer | 整数 | 最小バッファー (省略可能)

2 つの出力テーブルがある次のようにします。

**\#Events テーブルスキーマ**

列名 | SQL データ型 | 説明
--- | --- | ---
SequenceID | Int 型の NULL でないです。 | 相関関係のシーケンス ID
EventtypeId | Int 型の NULL でないです。 | イベントの種類 ID ([dbo] を参照してください。 [Eventtypes])
プロセス Id | BigInt NOT NULL | ［プロセス ID］
スレッド Id | BigInt NOT NULL | ［スレッド ID］
timestamp | datetime2 NOT NULL | timestamp
カーネル時間 | BigInt NOT NULL | カーネル時間
Usertime | BigInt NOT NULL | ユーザー時間

**\#EventProperties テーブルスキーマ**

列名 | SQL データ型 | 説明
--- | --- | ---
SequenceID | Int 型の NULL でないです。 | 相関関係のシーケンス ID
名前 | Nvarchar (100) | プロパティ名
Value | Nvarchar (4000) | Value

### <a name="etw-schema"></a>ETW スキーマ

ETW スキーマは、.etl ファイルに対して tracerpt.exe を実行して生成できます。 Schema.man ファイルが生成されます。 .Etl ファイルの形式は、依存しているコンピューターであるために、次のスクリプトは次の状況でのみ動作します。

1.  コンピューター上の対応する .etl ファイルを収集する場所に、スクリプトを実行します。

2.  または、同じオペレーティング システムとコンポーネントがインストールされているコンピューターでスクリプトを実行します。

``` syntax
tracerpt *.etl -export
```

## <a name="glossary"></a>用語集


次の用語は、このドキュメントで使用されます。

**Advisor パック**

Advisor パックは、メタデータと、ターゲット サーバーから収集されたパフォーマンス ログを処理する SQL スクリプトのコレクションです。 Advisor パックは、パフォーマンス ログ データからレポートを生成します。 Advisor パック内のメタデータでは、パフォーマンスの測定のターゲット サーバーから収集するデータを定義します。 メタデータには、ルール、しきい値、およびレポートの形式のセットも定義します。 ほとんどの場合、たとえば、インターネット インフォメーション サービス (IIS)、単一のサーバーの役割専用の advisor パックが書き込まれます。

**SPA コンソール**

SPA コンソールは、Server Performance Advisor の中央に含まれている SpaConsole.exe を指します。 SPA は、テストしているターゲット サーバー上で実行する必要はありません。 SPA コンソールには、分析を実行して、レポートを表示するプロジェクトの設定から、SPA のすべてのユーザー インターフェイスが含まれています。 仕様では、SPA は、2 層アプリケーションです。 SPA コンソールには、UI 層とビジネス ロジック層の一部が含まれています。 SPA コンソールは、スケジュールを設定し、パフォーマンス分析の要求を処理します。

**SPA フレームワーク**

SPA には、2 つの主要な部分、フレームワーク、および advisor パックが含まれています。 SPA フレームワークでは、すべてのユーザー インターフェイス、ログ処理のパフォーマンス、構成、エラー処理とデータベース Api、および管理の手順を提供します。

**SPA プロジェクト**

SPA プロジェクトは、ターゲット サーバー、advisor パックおよび advisor パックの対象サーバーで生成されたパフォーマンス分析レポートに関するすべての情報を含むデータベースです。 比較して、同じ SPA プロジェクト内の履歴と傾向のグラフを表示できます。 ユーザーは、1 つ以上のプロジェクトを作成できます。 SPA プロジェクトは、別の独立しており、プロジェクト間で共有するデータはありません。

**対象サーバー**

ターゲット サーバーは、物理コンピューターまたは IIS などの特定のサーバーの役割と Windows Server を実行する仮想マシンです。

**データ分析セッション**

データの分析セッションは、特定のターゲット サーバーのパフォーマンス分析です。 データの分析セッションでは、複数の advisor パックを含めることができます。 これらの advisor パックからデータ コレクター セットは、1 つのデータ コレクター セットにマージされます。 1 つのデータの分析セッションのすべてのパフォーマンス ログは、同じ期間中に収集されます。 同じデータの分析セッションで実行されている advisor パックによって生成されるレポートの分析と、全体的なパフォーマンスの状況を理解し、パフォーマンスの問題の根本原因を特定のユーザーが役立つ場合があります。

**Windows イベント トレーシング**

[イベントのトレース](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) for Windows (ETW) は、Windows オペレーティング システムで提供されている高パフォーマンス、低オーバーヘッドでスケーラブルなトレース システムです。 プロファイリングとデバッグのさまざまなシナリオをトラブルシューティングするために使用できる機能を提供します。 SPA は、データ ソースとして、パフォーマンス レポートが生成される ETW イベントを使用します。 ETW に関する一般的な情報を参照してください。 [デバッグの向上およびパフォーマンス調整 ETW を](https://msdn.microsoft.com/magazine/cc163437.aspx)します。

**WMI query**

Windows Management Instrumentation (WMI) は、インフラストラクチャの管理データと Windows オペレーティング システムでの操作です。 WMI スクリプトまたはリモート コンピューター上の管理作業を自動化するアプリケーションを記述することができます。 WMI では、管理データ、オペレーティング システムの他の部分との製品にも利用できます。 SPA は WMI クラス情報とデータ ポイントをパフォーマンス レポートの生成のソースとして使用します。

**パフォーマンス カウンター**

パフォーマンス カウンターを使用して、でなく、オペレーティング システムまたはアプリケーション、サービス、またはドライバーの実行に関する情報を提供します。 パフォーマンス カウンター データは、システムのボトルネックの特定やシステムとアプリケーションのパフォーマンスの微調整に役立ちます。 オペレーティング システム、ネットワーク、およびデバイスは、システムのパフォーマンスがどの程度のグラフィック表示をユーザーに提供するアプリケーションを使用できるカウンターのデータを提供します。 SPA はパフォーマンス カウンターの情報とデータ ポイントをパフォーマンス レポートを生成するのにソースとして使用します。

**パフォーマンス ログと警告**

パフォーマンス ログと警告 (PLA) は、Windows オペレーティング システムの組み込みのサービスです。 パフォーマンス ログやトレースを収集するものではし、特定のトリガーが満たされたときにパフォーマンスの警告も発生します。 パフォーマンス カウンター、Windows (ETW)、WMI クエリ、レジストリ キー、および構成ファイルのトレース イベントを収集する PLA を使用できます。 PLA には、リモート プロシージャ コール (RPC) によるリモート データ収集もサポートしています。 ユーザーは、データを収集する、データ収集の頻度、データ コレクション期間、フィルター、結果ファイルの保存場所に関する情報を含んだデータ コレクター セットを定義します。 SPA は、ターゲット サーバーからすべてのパフォーマンス データを収集するのに PLA を使用します。

**1つのレポート**

1 つのレポートは、単一のターゲット サーバー上の 1 つの Advisor パックの 1 つのデータ分析セッションに基づいて生成される SPA レポートです。 通知とさまざまなデータ セクションに含めることができます。

**サイドバイサイドのレポート**

サイド バイ サイドのレポートは、同じ advisor パックの 2 つの単一のレポートを比較する SPA レポートです。 別のターゲット サーバーから、または同じターゲット サーバー上の別のパフォーマンス分析の実行から、2 つのレポートを生成できます。 サイド バイ サイドのレポートでは、ユーザーが異常な動作や、レポートのいずれかの設定を識別するための 2 つのレポートを比較する機能を作成します。 サイド バイ サイドのレポートには、通知とさまざまなデータ セクションが含まれています。 各セクションでは、両方のレポートからのデータは、一覧にサイド バイ サイドです。

**傾向グラフ**

トレンド グラフは、パフォーマンスの問題の繰り返しパターンの調査に使用する SPA レポートです。 多くの反復的なパフォーマンスの問題は、サーバーまたはクライアント コンピューターは、毎日発生することが、毎週にスケジュールされたサーバーの負荷の変化が原因です。 SPA は、24 時間のトレンド グラフとこれらの問題を識別するために 7 日間の傾向グラフを提供します。

ユーザーが 1 つまたは複数のデータ系列では 1 つのレポート内の数値をなどは一度に選択できる **合計 CPU 使用率の平均**します。 具体的には、数値は、特定の時間インスタンスで1つの AP によって生成される単一サーバーのスカラー値です。 SPA は 24 日 (7 日間レポートは、各曜日に 1 つずつ 7) の 1 時間ごとに 1 つのグループにこれらの値をグループ化します。 SPA は、平均、最小値、最大値、および各グループの標準偏差を計算します。

**履歴グラフ**

履歴のグラフは、特定のサーバーおよび advisor パックのペアの 1 つのレポート内の特定の数値で時間の経過と共に変更を表示するために使用される SPA レポートです。 ユーザーは、複数のデータ系列を選択し、別のデータ系列間の相関関係を理解する履歴のグラフにまとめて表示することができます。

**データ系列**

データ系列は、時間の期間にわたって、同じデータ ソースから収集される数値データです。 同じソースでは、データが、1 つのサーバーで IIS の要求の平均キュー長など、同じターゲット サーバーから取得することを意味します。

**ルール**

ルールは、ロジック、しきい値、および説明の組み合わせです。 これらは、潜在的なパフォーマンスの問題を表します。 各 advisor パックには、複数のルールが含まれています。 各ルールは、レポートの生成プロセスによりトリガされます。 ルールには、1 つのレポート内のデータにロジックとしきい値が適用されます。 条件が満たされる場合は、警告通知が発生します。 通知に設定されていない場合、 **OK** 状態です。 該当なし に、通知を設定するルールが適用されない場合 (**NA**) の状態。

**通知**

通知は、ユーザーにルールを表示する情報です。 規則の状態が含まれています (**OK**, 、**NA**, 、または **警告**)、ルール、およびパフォーマンスの問題に対処可能な推奨事項の名前。
