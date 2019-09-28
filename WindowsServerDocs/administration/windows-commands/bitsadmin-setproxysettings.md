---
title: bitsadmin setproxysettings
description: '**Bitsadmin setproxysettings**の Windows コマンドのトピック-指定したジョブのプロキシ設定を設定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be8edb1b-614e-4d0b-a8f8-64b4bde3e64b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38987c88bcfc93ea9251583b7914f982cf79e057
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380468"
---
# <a name="bitsadmin-setproxysettings"></a>bitsadmin setproxysettings



指定されたジョブのプロキシ設定を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetProxySettings <Job> <Usage> [List] [Bypass]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|使用方法|次のいずれかの値です。</br>-PRECONFIG —所有者の Internet Explorer の既定値を使用します。</br>-NO_PROXY —プロキシサーバーを使用しません。</br>-OVERRIDE —明示的なプロキシリストとバイパスリストを使用します。 プロキシとプロキシのバイパスリストは、の後に続く必要があります。</br>-自動検出—プロキシ設定を自動的に検出します。|
|リスト|*Usage*パラメーターが OVERRIDE に設定されている場合に使用します。には、使用するプロキシサーバーのコンマ区切りの一覧が含まれています。|
|通過|*Usage*パラメーターが OVERRIDE に設定されている場合に使用されます。には、転送がプロキシ経由でルーティングされない、ホスト名または IP アドレスのスペース区切りの一覧、またはその両方が含まれています。 これは、同じ LAN 上のすべてのサーバーを参照するために **、\< のローカル >** にすることができます。 空のプロキシバイパスリストには、NULL または "" の値を使用できます。|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのプロキシ設定を設定します。

```
C:\>bitsadmin /SetProxySettings myDownloadJob PRECONFIG
```

その他の例を次に示します。

```
bitsadmin /setproxysettings myDownloadJob NO_PROXY
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1:80 ""
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1,proxy2,proxy3 NULL
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)