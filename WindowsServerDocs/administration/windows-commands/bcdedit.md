---
title: bcdedit
description: '**Bcdedit**の Windows コマンドに関するトピック。新しいストアを作成し、既存のストアを変更して、ブートメニューパラメーターを追加します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ab2da47d-3aac-44a0-b7fd-bd9561d61553
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/27/2018
ms.openlocfilehash: f5bd39fa29dc99bba0d3600fc8609a355ffe540c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851075"
---
# <a name="bcdedit"></a>bcdedit

ブート構成データ (BCD) ファイルは、ブート アプリケーションとブート アプリケーション設定の記述に使用されるストアを提供します。 ストア内のオブジェクトと要素は、効果的に Boot.ini と置き換えられます。

BCDEdit は、BCD ストアを管理するためのコマンド ライン ツールです。 新しい店舗の作成、既存のストアの変更、ブートメニューパラメーターの追加など、さまざまな目的で使用できます。 BCDEdit は、基本的に Windows の初期のバージョンでの Bootcfg.exe と同じ目的に使用されますが、主に次の 2 つの点が向上しています。

- は、Bootcfg.exe よりも広い範囲のブートパラメーターを公開します。

- では、スクリプトのサポートが強化されています。

> [!NOTE]
> BCD を変更するために BCDEdit を使用するには、管理者特権が必要です。

BCDEdit は、Windows Vista 以降のバージョンの Windows のブート構成を編集するための主要なツールです。 これは、%WINDIR%\System32 フォルダーにある Windows Vista の配布に含まれています。

BCDEdit は、標準のデータの種類に限定され、主に BCD に単一の共通の変更を行うように設計されています。 より複雑な操作や標準以外のデータの種類に対しては、より強力で柔軟なカスタム ツールを作成する BCD Windows Management Instrumentation (WMI) アプリケーション プログラミング インターフェイス (API) の使用を検討してください。

## <a name="syntax"></a>構文

```
BCDEdit /Command [<Argument1>] [<Argument2>] ...
```

### <a name="parameters"></a>パラメーター

### <a name="general-bcdedit-command-line-option"></a>一般的な BCDEdit のコマンド ライン オプション

| オプション | 説明 |
| ------ | ----------- |
| /? | BCDEdit コマンドの一覧を表示します。 引数なしでこのコマンドを実行すると、使用可能なコマンドの概要が表示されます。 特定のコマンドの詳細なヘルプを表示するには、 **bcdedit/?** を実行します。 `<command>`。ここで `<command>` は、詳細情報を検索するコマンドの名前です。 たとえば、 **bcdedit/? createstore**では、createstore コマンドの詳細なヘルプが表示されます。 |

#### <a name="parameters-that-operate-on-a-store"></a>ストアで動作するパラメーター

| オプション | 説明 |
| ------ | ----------- |
| /createstore | 新しい空のブート構成データ ストアを作成します。 作成されたストアはシステム ストアではありません。 |
| /export | システム ストアの内容をファイルにエクスポートします。 このファイルは、後でシステム ストアの状態を復元するために使用できます。 このコマンドは、システム ストアに対してのみ有効です。 |
| /import | **/Export**オプションを使用して以前に生成したバックアップデータファイルを使用して、システムストアの状態を復元します。 このコマンドは、インポートを行う前にシステム ストア内の既存のエントリを削除します。 このコマンドは、システム ストアに対してのみ有効です。 |
| /store | このオプションは、使用するストアを指定するためにほとんどの BCDedit コマンドで使用できます。 このオプションを指定しないと、BCDEdit はシステム ストア上で動作します。 **Bcdedit/store**コマンドを単独で実行することは、 **bcdedit/enum active**コマンドを実行することと同じです。 |

#### <a name="parameters-that-operate-on-entries-in-a-store"></a>ストア内のエントリを操作するパラメーター

| パラメーター | 説明 |
| ------ | ----------- |
| /copy | 同じシステム ストア内で指定されたブート エントリのコピーを作成します。 |
| /create | ブート構成データ ストア内に新しいエントリを作成します。 既知の識別子が指定されている場合、 **/application**、 **/inherit**、および **/device**パラメーターを指定することはできません。 識別子が指定されていないか、よく知られていない場合は、 **/application**、 **/inherit**、または **/device**オプションを指定する必要があります。 |
| /delete | 指定されたエントリから要素を削除します。 |

#### <a name="parameters-that-operate-on-entry-options"></a>入力オプションで動作するパラメーター

| パラメーター | 説明 |
| ------ | ----------- |
| /deletevalue | ブート エントリから指定された要素を削除します。 |
| /set | エントリ オプション値を設定します。 |

#### <a name="parameters-that-control-output"></a>出力を制御するパラメーター

| パラメーター | 説明 |
| ------ | ----------- |
| /enum | ストア内のエントリを一覧表示します。 **/Enum**オプションは bcedit の既定値であるため、パラメーターを指定せずに**bcdedit**コマンドを実行することは、 **bcdedit/enum active**コマンドを実行することと同じです。 |
| /v | 詳細モード。 通常、既知のエントリ ID は、わかりやすい短い形式で示されます。 **/V**をコマンドラインオプションとして指定すると、すべての識別子が完全に表示されます。 **Bcdedit/v**コマンドを単独で実行することは、 **bcdedit/enum active/v**コマンドを実行することと同じです。 |

#### <a name="parameters-that-control-the-boot-manager"></a>ブートマネージャーを制御するパラメーター

| パラメーター | 説明 |
| ------ | ----------- |
| /bootsequence | 次の起動時にのみ使用する、1 回限りの表示順序を指定します。 このコマンドは、次にコンピューターを起動するときにのみ使用される点を除いて、 **/displayorder**オプションに似ています。 このコマンドの実行後、コンピューターは元の表示順序に戻ります。 |
| /default | タイムアウトとなった場合に、ブート マネージャーが選択する既定のエントリを指定します。 |
| /displayorder | ブートパラメーターをユーザーに表示するときにブートマネージャーが使用する表示順序を指定します。 |
| /timeout | ブート マネージャーが既定のエントリを選択するまで、待機する時間を秒単位で指定します。 |
| /toolsdisplayorder | **[ツール]** メニューを表示するときに使用するブートマネージャーの表示順序を指定します。 |

#### <a name="parameters-that-control-emergency-management-services"></a>緊急管理サービスを制御するパラメーター

| パラメーター | 説明 |
| ------ | ----------- |
| /bootems | 指定されたエントリの緊急管理サービス (EMS) を有効または無効にします。 |
| /ems | 指定されたオペレーティング システムのブート エントリの EMS を有効または無効にします。 |
| /emssettings | コンピューターのグローバル EMS 設定を設定します。 **/emssettings**では、特定のブートエントリの EMS を有効または無効にすることはできません。 |

#### <a name="parameters-that-control-debugging"></a>デバッグを制御するパラメーター

| パラメーター | 説明 |
| ------ | ----------- |
| /bootdebug | 指定されたブート エントリのブート デバッガーを有効または無効にします。 このコマンドは任意のブート エントリに使用できますが、ブート アプリケーションにのみ効果があります。 |
| /dbgsettings | システムのグローバル デバッガー設定を指定または表示します。 このコマンドは、enablepose 無効にします。 個々のグローバルデバッガー設定を設定するには、 **bcdedit/set** `<dbgsettings> <type> <value>` コマンドを使用します。 |
| /debug | 指定されたブート エントリのカーネル デバッガーを有効または無効にします。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

BCDEdit の使用方法の例については、 [Bcdedit オプションのリファレンス](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcd-boot-options-reference)記事を参照してください。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
