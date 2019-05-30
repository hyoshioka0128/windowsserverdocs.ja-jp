---
title: bitsadmin util と setieproxy
description: Windows コマンド」のトピック**bitsadmin util と setieproxy** -サービス アカウントを使用してファイルを転送するときに使用するプロキシ設定を設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f31ba-3070-4ffd-a94c-388c8d78f688
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81bb333e2bb776bc75789b52ab41d7ef64016f51
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266464"
---
# <a name="bitsadmin-util-and-setieproxy"></a>bitsadmin util と setieproxy

サービス アカウントを使用してファイルを転送するときに使用するプロキシ設定を設定します。

**1.5 およびそれ以前の BITSAdmin**: サポートされません。

## <a name="syntax"></a>構文

```
bitsadmin /Util /SetIEProxy <Account> <Usage>[/Conn <ConnectionName>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|アカウント|サービス アカウントを定義するプロキシ設定の種類を指定します。 設定可能な値は、次のとおりです。</br>ローカル システム</br>-NETWORKSERVICE</br>-LOCALSERVICE|
|使用方法|使用するプロキシ検出の形式を指定します。 設定可能な値は、次のとおりです。</br>-NO_PROXY — プロキシ サーバーを使用しません。</br>-AUTODETECT: プロキシ設定を自動的に検出します。</br>-MANUAL_PROXY: 明示的なプロキシのリストを使用し、リストをバイパスします。 プロキシ一覧を指定し、すぐ後に、使用状況のタグ リストをバイパスします。 たとえば、MANUAL_PROXY proxy1、proxy2 NULL です。</br>    プロキシ一覧は、使用するプロキシ サーバーのコンマ区切り一覧を示します。</br>    -バイパス リストは、スペースで区切られた一覧のホスト名または IP アドレス、またはその両方を対象の転送はプロキシを経由してルーティングします。 これは、\<ローカル > を同じ LAN 上のすべてのサーバーを参照してください。 NULL 値または""を空のプロキシ バイ パス一覧の使用可能性があります。</br>-AUTOSCRIPT — ことを除けば、自動検出と同じでもスクリプトを実行します。 使用状況のタグの直後に続くスクリプトの URL を指定します。 たとえば、AUTOSCRIPT http://server/proxy.jsします。</br>リセット-手動プロキシの Url を削除ことを除けば、NO_PROXY と同じには、(選択した場合のみ) し、Url では、自動検出を使用して検出されました。|
|ConnectionName|省略可能: と併用、 **/conn**パラメーターを使用するモデム接続を指定します。 指定しない場合、 **/conn**パラメーター、BITS は LAN 接続を使用します。 直後に続くモデム接続名を指定、 **/conn**パラメーター。|

## <a name="remarks"></a>注釈

このスイッチを使用して連続する各呼び出しは、以前に指定された使用量が以前に定義された使用状況のパラメーターではなく、置き換えられます。 たとえば、NO_PROXY、自動で検出および MANUAL_PROXY を個別の呼び出しで指定した場合ビットは最後の指定された使用法を使用してが以前に定義された使用状況からパラメーターを保持します。

> [!IMPORTANT]
> このコマンドは、正常に完了するための管理者特権でコマンド プロンプトから実行する必要があります。

## <a name="examples"></a>例

次の例では、NETWORK SERVICE アカウントに対するプロキシの使用を設定します。

```
C:\>bitsadmin /Util /SetIEProxy localsystem AUTODETECT
```

他の例を示します。

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1,proxy2,proxy3 NULL
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1:80 ""
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)