---
title: bcdedit
description: '**Bcdedit**の Windows コマンドに関するトピック: 新しいストアを作成し、既存のストアを変更して、ブートメニューパラメーターを追加します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 9448f4461a089a93382ef8cd9e804b382fca27e4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382247"
---
# <a name="bcdedit"></a>bcdedit



ブート構成データ (BCD) ファイルは、ブートアプリケーションとブートアプリケーション設定を記述するために使用されるストアを提供します。 ストア内のオブジェクトと要素は、Boot.ini を効果的に置き換えます。

BCDEdit は、BCD ストアを管理するためのコマンドラインツールです。 新しい店舗の作成、既存のストアの変更、ブートメニューパラメーターの追加など、さまざまな目的で使用できます。 BCDEdit は基本的に、以前のバージョンの Windows では Bootcfg.exe と同じ目的で機能しますが、主に2つの改善点があります。
-   は、Bootcfg.exe よりも広い範囲のブートパラメーターを公開します。
-   では、スクリプトのサポートが強化されています。

> [!NOTE]
> BCDEdit を使用して BCD を変更するには、管理者特権が必要です。

BCDEdit は、Windows Vista 以降のバージョンの Windows のブート構成を編集するための主要なツールです。 これは、%WINDIR%\System32 フォルダーにある Windows Vista の配布に含まれています。

BCDEdit は、標準的なデータ型に限定されており、主に BCD に対して1つの一般的な変更を行うことを目的としています。 より複雑な操作または非標準のデータ型の場合は、BCD Windows Management Instrumentation (WMI) アプリケーションプログラミングインターフェイス (API) を使用して、より強力で柔軟性の高いカスタムツールを作成することを検討してください。

## <a name="syntax"></a>構文

```
BCDEdit /Command [<Argument1>] [<Argument2>] ...
```

## <a name="parameters"></a>パラメーター

### <a name="general-bcdedit-command-line-option"></a>一般的な BCDEdit コマンドラインオプション

|OPTION|説明|
|------|-----------|
|/?|BCDEdit コマンドの一覧を表示します。 引数を指定せずにこのコマンドを実行すると、使用可能なコマンドの概要が表示されます。 特定のコマンドの詳細なヘルプを表示するには、 **bcdedit/?** を実行します。 \<command >。ここで <command> は、詳細情報を検索するコマンドの名前です。 たとえば、 **bcdedit/? createstore**では、createstore コマンドの詳細なヘルプが表示されます。|

### <a name="parameters-that-operate-on-a-store"></a>ストアで動作するパラメーター

|OPTION|説明|
|------|-----------|
|/createstore|新しい空のブート構成データストアを作成します。 作成されたストアはシステムストアではありません。|
|/export|システムストアの内容をファイルにエクスポートします。 このファイルは、後でシステムストアの状態を復元するために使用できます。 このコマンドは、システムストアに対してのみ有効です。|
|/import|**/Export**オプションを使用して以前に生成したバックアップデータファイルを使用して、システムストアの状態を復元します。 このコマンドは、インポートが行われる前に、システムストア内の既存のエントリを削除します。 このコマンドは、システムストアに対してのみ有効です。|
|/store|このオプションは、ほとんどの BCDedit コマンドで使用して、使用するストアを指定できます。 このオプションが指定されていない場合、BCDEdit はシステムストアに対して動作します。 **Bcdedit/store**コマンドを単独で実行することは、 **bcdedit/enum active**コマンドを実行することと同じです。|

### <a name="parameters-that-operate-on-entries-in-a-store"></a>ストア内のエントリを操作するパラメーター

|パラメーター|説明|
|---------|-----------|
|/copy|指定されたブートエントリのコピーを同じシステムストアに作成します。|
|作成します|ブート構成データストアに新しいエントリを作成します。 既知の識別子が指定されている場合、 **/application**、 **/inherit**、および **/device**パラメーターを指定することはできません。 識別子が指定されていないか、よく知られていない場合は、 **/application**、 **/inherit**、または **/device**オプションを指定する必要があります。|
|/delete|指定されたエントリから要素を削除します。|

### <a name="parameters-that-operate-on-entry-options"></a>入力オプションで動作するパラメーター

|パラメーター|説明|
|---------|-----------|
|/deletevalue|指定された要素をブートエントリから削除します。|
|/set|エントリオプションの値を設定します。|

### <a name="parameters-that-control-output"></a>出力を制御するパラメーター

|パラメーター|説明|
|---------|-----------|
|/enum|ストア内のエントリを一覧表示します。 **/Enum**オプションは bcedit の既定値であるため、パラメーターを指定せずに**bcdedit**コマンドを実行することは、 **bcdedit/enum active**コマンドを実行することと同じです。|
|/v|詳細モード。 通常、よく知られているエントリ識別子は、わかりやすい短縮形で表されます。 **/V**をコマンドラインオプションとして指定すると、すべての識別子が完全に表示されます。 **Bcdedit/v**コマンドを単独で実行することは、 **bcdedit/enum active/v**コマンドを実行することと同じです。|

### <a name="parameters-that-control-the-boot-manager"></a>ブートマネージャーを制御するパラメーター

|パラメーター|説明|
|---------|-----------|
|/bootsequence|次回の起動時に使用される1回限りの表示順序を指定します。 このコマンドは、次にコンピューターを起動するときにのみ使用される点を除いて、 **/displayorder**オプションに似ています。 その後、コンピューターは元の表示順序に戻ります。|
|/default|タイムアウトが経過したときにブートマネージャーが選択する既定のエントリを指定します。|
|/displayorder|ブートパラメーターをユーザーに表示するときにブートマネージャーが使用する表示順序を指定します。|
|/timeout|ブートマネージャーが既定のエントリを選択するまでの待機時間を秒単位で指定します。|
|/ツール displayorder|**[ツール]** メニューを表示するときに使用するブートマネージャーの表示順序を指定します。|

### <a name="parameters-that-control-emergency-management-services"></a>緊急管理サービスを制御するパラメーター

|パラメーター|説明|
|---------|-----------|
|/bootems|指定されたエントリの緊急管理サービス (EMS) を有効または無効にします。|
|/ems|指定されたオペレーティングシステムブートエントリの EMS を有効または無効にします。|
|/emssettings|コンピューターのグローバル EMS 設定を設定します。 **/emssettings**では、特定のブートエントリの EMS を有効または無効にすることはできません。|

### <a name="parameters-that-control-debugging"></a>デバッグを制御するパラメーター

|パラメーター|説明|
|---------|-----------|
|/bootdebug|指定されたブートエントリのブートデバッガーを有効または無効にします。 このコマンドはどのブートエントリに対しても機能しますが、ブートアプリケーションに対してのみ有効です。|
|/dbgsettings|システムのグローバルデバッガー設定を指定または表示します。 このコマンドは、カーネルデバッガーを有効または無効にしません。そのためには、 **/debug**オプションを使用します。 個々のグローバルデバッガー設定を設定するには、 **bcdedit/set** \<dbgsettings > <type> を使用します。 <value> コマンドなど) を指定します。|
|/debug|指定されたブートエントリのカーネルデバッガーを有効または無効にします。|

## <a name="examples"></a>使用例

BCDEdit の例については、 [bcdedit のオプションリファレンス](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcd-boot-options-reference)を参照してください。