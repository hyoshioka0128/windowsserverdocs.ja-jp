---
title: Sc クエリ
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac365f89-4b20-4de6-a582-b204c5e7d0eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ed9ee813e3ea41f24ce5c012eecd278ef051138
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879293"
---
# <a name="sc-query"></a>Sc クエリ



取得し、指定されたサービス、ドライバー、サービスの種類またはドライバーの種類に関する情報を表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
sc [<ServerName>] query [<ServiceName>] [type= {driver | service | all}] [type= {own | share | interact | kernel | filesys | rec | adapt}] [state= {active | inactive | all}] [bufsize= <BufferSize>] [ri= <ResumeIndex>] [group= <GroupName>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<サーバー名 >|サービスが配置されているリモート サーバーの名前を指定します。 名前は、汎用名前付け規則 (UNC) 形式を使用する必要があります (たとえば、 \\ \\myserver)。 SC.exe をローカルで実行するには、このパラメーターを省略します。|
|\<ServiceName >|によって返されるサービスの名前を指定、 **られて** 操作します。 これは、 **クエリ** と共にその他のパラメーターは使用されません **クエリ** パラメーター (以外の *ServerName*)。|
|型 = {ドライバー | サービス (service) | すべて}|列挙の対象を指定します。 最初の型の既定値は **サービス**します。</br>-ドライバー。ドライバーのみが列挙されることを指定します。</br>-サービス。サービスのみが列挙されることを指定します。</br>-すべて。ドライバーとサービスの両方が列挙されることを指定します。|
|型 = {所有 | 共有 | 操作 | kernel | filesys | 推奨値 | 適応}|サービスの型または列挙するドライバーの種類を指定します。 2 番目の型の既定値は **独自**します。</br>-独自。サービスが、独自のプロセスで実行されることを指定します。 実行可能ファイルは他のサービスと共有されません。</br>-共有します。サービスを共有プロセスとして実行することを指定します。 その他のサービス実行可能ファイルを共有します。</br>-操作します。サービスはユーザーからの入力を受け取って、デスクトップと対話できることを指定します。 対話型サービスは、LocalSystem アカウントで実行する必要があります。</br>-カーネル。ドライバーを指定します。</br>-filesys:ファイル システム ドライバーを指定します。|
|状態 = {アクティブ | 非アクティブ | すべて}|列挙するサービスの開始状態を指定します。 既定の状態は **active**します。</br>-active:すべてのアクティブなサービスを指定します。</br>-使用頻度の低い。すべての一時停止または停止したサービスを指定します。</br>-すべて。すべてのサービスを指定します。|
|bufsize= \<BufferSize>|列挙バッファーのサイズをバイト単位で指定します。 既定のバッファー サイズは、1,024 バイトです。 クエリの結果の表示が 1,024 バイトを超えると、列挙型のバッファーのサイズを増やす必要があります。|
|ri = \<ResumeIndex >|列挙を開始または再開するにはインデックス番号を指定します。 既定値は **0** (ゼロ)。 組み合わせてこのパラメーターを使用して、 **bufsize =** パラメーターの詳細については、バッファーの既定で表示できるよりも、クエリによって返されたとき。|
|グループ = \<GroupName >|列挙するサービス グループを指定します。 既定では、すべてのグループが列挙される (**グループ =""**)。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   パラメーターと値の間のスペースのない (つまり、 **型 = 独自**, ではなく、 **型 = 独自**)、操作は失敗します。
-   **クエリ**操作には、サービスの詳細については、次の情報が表示されます。WIN32_EXIT_B、SERVICE_EXIT_B、チェックポイント、および WAIT_HINT (状態は使用できない) および状態 (サービスのレジストリ サブキーの名前)、サービス名を入力します。
-   **型 =** 場合によってはで 2 回パラメーターを使用することができます。 最初の外観、 **型 =** パラメーターでは、サービス、ドライバー、またはその両方のクエリを実行するかどうかを指定します (**すべて**)。 2 つ目の外観、 **型 =** パラメーターから型を指定、 **作成** さらに、クエリの範囲を絞り込むに操作します。
-   ときに起因する表示、 **クエリ** コマンドは、列挙型のバッファーのサイズを超える場合、次のようなメッセージが表示されます。  
    ```
    Enum: more data, need 1822 bytes start resume at index 79
    ```  
    残りを表示する **クエリ** については、再実行 **クエリ**, 設定 **bufsize =** バイトと設定の数値を指定する **ri =** 指定したインデックス。 たとえば、残りの出力は、コマンド プロンプトで次を入力して表示されるは。  
    ```
    sc query bufsize= 1822 ri= 79
    ```

## <a name="BKMK_examples"></a>例

アクティブなサービスのみの情報を表示するには、次のコマンドのいずれかを入力します。
```
sc query
sc query type= service
```
アクティブなサービスの情報を表示し、2,000 バイトのバッファー サイズを指定するには、次のように入力します。
```
sc query type= all bufsize= 2000
```
WUAUSERV サービスの情報を表示するには、次のように入力します。
```
sc query wuauserv
```
すべてのサービス (アクティブおよび非アクティブ) の情報を表示するには、次のように入力します。
```
sc query state= all
```
すべてのサービス (アクティブおよび非アクティブ)、56 行目から始まる情報を表示するには、次のように入力します。
```
sc query state= all ri= 56
```
対話型サービスの情報を表示するには、次のように入力します。
```
sc query type= service type= interact
```
ドライバーのみの情報を表示するには、次のように入力します。
```
sc query type= driver
```
ドライバーの情報を表示するには、Network Driver Interface Specification (NDIS) グループで、次のように入力します。
```
sc query type= driver group= ndis
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)