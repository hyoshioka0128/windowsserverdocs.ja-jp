---
title: bitsadmin util と setieproxy
description: Bitsadmin util と setieproxy の Windows コマンドに関するトピックでは、サービスアカウントを使用してファイルを転送するときに使用するプロキシ設定を設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e9f31ba-3070-4ffd-a94c-388c8d78f688
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e7d8a9ff4e2388b61ee5ae00ae7afe421de68e6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848885"
---
# <a name="bitsadmin-util-and-setieproxy"></a>bitsadmin util と setieproxy

サービスアカウントを使用してファイルを転送するときに使用するプロキシ設定を設定します。

**BITSAdmin 1.5 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /Util /SetIEProxy <Account> <Usage>[/Conn <ConnectionName>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|アカウント|プロキシ設定を定義するサービスアカウントの種類を指定します。 設定可能な値は、次のとおりです。</br>-LOCALSYSTEM</br>-NETWORKSERVICE</br>-LOCALSERVICE|
|使用法|使用するプロキシ検出の形式を指定します。 設定可能な値は、次のとおりです。</br>-NO_PROXY —プロキシサーバーを使用しません。</br>-自動検出—プロキシ設定を自動的に検出します。</br>-MANUAL_PROXY —明示的なプロキシリストとバイパスリストを使用します。 使用状況タグのすぐ後に、プロキシリストとバイパスリストを指定します。 たとえば、MANUAL_PROXY proxy1, proxy2 NULL です。</br>    -プロキシリストは、使用するプロキシサーバーのコンマ区切りの一覧です。</br>    -バイパスリストは、ホスト名または IP アドレス (またはその両方) のスペース区切りの一覧であり、転送はプロキシ経由でルーティングされません。 これは、同じ LAN 上のすべてのサーバーを参照するローカル > \<できます。 NULL またはの値は、空のプロキシバイパスリストに使用できます。</br>-AUTOSCRIPT —自動検出と同じですが、スクリプトも実行されます。 使用状況タグの直後にスクリプト URL を指定します。 たとえば、AUTOSCRIPT http://server/proxy.jsします。</br>-RESET — NO_PROXY と同じですが、手動プロキシ Url (指定されている場合) と、自動検出を使用して検出された Url が削除される点が異なります。|
|ConnectionName|省略可能: **/Conn**パラメーターと共に使用して、使用するモデム接続を指定します。 **/Conn**パラメーターを指定しない場合、BITS は LAN 接続を使用します。 **/Conn**パラメーターの直後に、モデムの接続名を指定します。|

## <a name="remarks"></a>コメント

このスイッチを使用する後続の各呼び出しは、以前に指定された使用量を置き換えますが、以前に定義された使用法のパラメーターは置き換えられません。 たとえば、個別の呼び出しで NO_PROXY、自動検出、および MANUAL_PROXY を指定した場合、BITS は最後に指定された使用量を使用しますが、以前に定義した使用法のパラメーターを保持します。

> [!IMPORTANT]
> このコマンドを正常に完了するには、管理者特権のコマンドプロンプトから実行する必要があります。

## <a name="examples"></a>例

次の例では、ネットワークサービスアカウントのプロキシ使用法を設定します。

```
C:\>bitsadmin /Util /SetIEProxy localsystem AUTODETECT
```

その他の例を次に示します。

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1,proxy2,proxy3 NULL
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1:80 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)