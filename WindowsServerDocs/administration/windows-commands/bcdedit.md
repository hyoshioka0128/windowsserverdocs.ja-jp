---
title: bcdedit
description: Windows コマンド」のトピック**bcdedit** - 新しいストアを作成、既存のストアを変更およびブート メニューのパラメーターを追加します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab2da47d-3aac-44a0-b7fd-bd9561d61553
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/27/2018
ms.openlocfilehash: c1ac016b299cbd72a406121c54762f4457b24286
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872443"
---
# <a name="bcdedit"></a>bcdedit



ブート構成データ (BCD) ファイルでは、ブート アプリケーションし、ブート アプリケーション設定に使用されるストアを提供します。 オブジェクトと、ストア内の要素効果的に Boot.ini と置き換えられます。

BCDEdit は、BCD ストアを管理するためのコマンド ライン ツールです。 さまざまな新しいストアを作成するなど、目的のために使用できます、変更する既存のストアの追加 メニューのパラメーターを起動します。 BCDEdit は基本的に、2 つの主要な機能強化が、Windows の以前のバージョンでの Bootcfg.exe と同じ目的があります。
-   Bootcfg.exe よりも広範なブート パラメーターを公開します。
-   スクリプトのサポートが向上しました。

> [!NOTE]
> BCDEdit を使用して BCD を変更するには、管理者特権が必要です。

BCDEdit は、以降のバージョンの Windows と Windows Vista のブート構成を編集するための主要なツールです。 %WINDIR%\System32 フォルダーに Windows Vista の配布に付属しています。

BCDEdit は、標準的なデータ型に制限は BCD に 1 つの一般的な変更を実行するには、主に設計されています。 複雑な操作または非標準のデータ型の場合より強力で柔軟なカスタム ツールを作成する BCD Windows Management Instrumentation (WMI) アプリケーション プログラミング インターフェイス (API) を使用を検討してください。

## <a name="syntax"></a>構文

```
BCDEdit /Command [<Argument1>] [<Argument2>] ...
```

## <a name="parameters"></a>パラメーター

### <a name="general-bcdedit-command-line-option"></a>一般的な BCDEdit のコマンド ライン オプション

|オプション|説明|
|------|-----------|
|/?|BCDEdit のコマンドの一覧が表示されます。 引数を指定しないでこのコマンドを実行するには、使用可能なコマンドの概要が表示されます。 特定のコマンドの詳細なヘルプを表示するには実行**bcdedit/でしょうか。** \<コマンド > ここで、<command>に関する詳細情報を検索するコマンドの名前を指定します。 たとえば、 **bcdedit/でしょうか。 createstore** Createstore コマンドの詳細なヘルプを表示します。|

### <a name="parameters-that-operate-on-a-store"></a>ストアを操作するためのパラメーター

|オプション|説明|
|------|-----------|
|/createstore|新しい空のブート構成データ ストアを作成します。 作成されたストアは、システム ストアではありません。|
|/export|ファイルに格納するシステムの内容をエクスポートします。 このファイルは、システム ストアの状態を復元する後で使用できます。 このコマンドは、システム ストアに対してのみ有効です。|
|/import|使用して以前に生成されたバックアップ データ ファイルを使用して、システム ストアの状態を復元、 **/export**オプション。 このコマンドは、インポートが行われる前に、システム ストア内の既存のエントリを削除します。 このコマンドは、システム ストアに対してのみ有効です。|
|/store|このオプションは、使用するストアを指定する、ほとんどの BCDedit コマンドで使用できます。 このオプションが指定されていない場合は、BCDEdit はシステム ストアで動作します。 実行している、 **bcdedit/store**を単独でコマンドを実行すると、 **bcdedit/enum active**コマンド。|

### <a name="parameters-that-operate-on-entries-in-a-store"></a>ストア内のエントリを操作するためのパラメーター

|パラメーター|説明|
|---------|-----------|
|/copy|同じシステム ストアで、指定されたブート エントリのコピーを作成します。|
|作成します|ブート構成データ ストアに新しいエントリを作成します。 既知の識別子が指定されている場合、 **/アプリケーション**、 **/inherit**、および **/device**パラメーターを指定することはできません。 識別子が指定されているか、不明がない場合、 **/アプリケーション**、 **/inherit**、または **/device**オプションを指定する必要があります。|
|/delete|指定されたエントリから要素を削除します。|

### <a name="parameters-that-operate-on-entry-options"></a>エントリ オプション上で動作するパラメーター

|パラメーター|説明|
|---------|-----------|
|/deletevalue|ブート エントリから、指定された要素を削除します。|
|/set|エントリ オプション値を設定します。|

### <a name="parameters-that-control-output"></a>出力を制御するパラメーター

|パラメーター|説明|
|---------|-----------|
|/enum|ストア内のエントリを一覧表示します。 **/Enum**オプションは BCEdit、実行するための既定値、 **bcdedit**パラメーターを指定しないでコマンドを実行すると、 **bcdedit/enum active**コマンド。|
|/v|詳細モード。 通常は、任意の既知のエントリの識別子は、わかりやすい短い形式で表されます。 指定する **/v**コマンド ライン オプションは、完全にすべての識別子を表示します。 実行している、 **bcdedit/v**を単独でコマンドを実行すると、 **bcdedit/enum active/v**コマンド。|

### <a name="parameters-that-control-the-boot-manager"></a>ブート マネージャーを制御するパラメーター

|パラメーター|説明|
|---------|-----------|
|/bootsequence|次回の起動時に使用する 1 回限りの表示順序を指定します。 このコマンドと似ています、 **/displayorder**オプション、点を除いてが使用されるだけで、次に、コンピューターを起動します。 その後、コンピューターは、元の表示順序に戻ります。|
|/default|タイムアウトの期限が切れると、ブート マネージャーが選択する既定のエントリを指定します。|
|/displayorder|ブート パラメーターをユーザーに表示するときに、ブート マネージャーが使用する表示順序を指定します。|
|/timeout|ブート マネージャーが、既定のエントリを選択するまでの秒の待機時間を指定します。|
|/toolsdisplayorder|表示するときに使用するブート マネージャーの表示順序を指定、**ツール**メニュー。|

### <a name="parameters-that-control-emergency-management-services"></a>緊急管理サービスを制御するパラメーター

|パラメーター|説明|
|---------|-----------|
|/bootems|有効または、指定されたエントリの緊急管理サービス (EMS) を無効にします。|
|/ems|有効または、指定したオペレーティング システムのブート エントリの EMS を無効にします。|
|/emssettings|コンピューターのグローバル EMS 設定を設定します。 **/emssettings**も有効または特定のブート エントリの EMS を無効にします。|

### <a name="parameters-that-control-debugging"></a>デバッグを制御するパラメーター

|パラメーター|説明|
|---------|-----------|
|/bootdebug|有効または、指定されたブート エントリのブート デバッガーを無効にします。 このコマンドは、任意のブート エントリは、ブート アプリケーションに対してのみ有効です。|
|/dbgsettings|指定またはシステムのグローバルなデバッガ設定を表示します。 このコマンドは、有効にまたはカーネル デバッガーを無効にします。使用して、 **/debug**目的のためのオプション。 個々 のグローバル デバッガー設定を設定するには、使用、 **bcdedit/set** \<dbgsettings > <type> <value> コマンドなど) を指定します。|
|/debug|有効または、指定されたブート エントリのカーネル デバッガーを無効にします。|

## <a name="examples"></a>例

BCDEdit の例については、次を参照してください。、[オプションの参照を BCDEdit](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcd-boot-options-reference)します。