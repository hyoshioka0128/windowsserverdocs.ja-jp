---
title: bitsadmin setproxysettings
description: Bitsadmin setproxysettings の Windows コマンドに関するトピックでは、指定されたジョブのプロキシ設定を設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be8edb1b-614e-4d0b-a8f8-64b4bde3e64b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4dea72d956d12070b2638f953a7a00dcb1ed7a9c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849205"
---
# <a name="bitsadmin-setproxysettings"></a>bitsadmin setproxysettings

指定されたジョブのプロキシ設定を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetProxySettings <Job> <Usage> [List] [Bypass]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|使用法|次のいずれかの値です。</br>-PRECONFIG —所有者の Internet Explorer の既定値を使用します。</br>-NO_PROXY —プロキシサーバーを使用しません。</br>-OVERRIDE —明示的なプロキシリストとバイパスリストを使用します。 プロキシとプロキシのバイパスリストは、の後に続く必要があります。</br>-自動検出—プロキシ設定を自動的に検出します。|
|一覧|*Usage*パラメーターが OVERRIDE に設定されている場合に使用します。には、使用するプロキシサーバーのコンマ区切りの一覧が含まれています。|
|通過|*Usage*パラメーターが OVERRIDE に設定されている場合に使用されます。には、転送がプロキシ経由でルーティングされない、ホスト名または IP アドレスのスペース区切りの一覧、またはその両方が含まれています。 これは、同じ LAN 上のすべてのサーバーを参照する**ローカル >\<** できます。 NULL またはの値は、空のプロキシバイパスリストに使用できます。|

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのプロキシ設定を設定します。

```
C:\>bitsadmin /SetProxySettings myDownloadJob PRECONFIG
```

その他の例を次に示します。

```
bitsadmin /setproxysettings myDownloadJob NO_PROXY
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1:80 
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1,proxy2,proxy3 NULL
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)