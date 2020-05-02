---
title: regsvr32
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: beadc9e9e614e2fe4cffad5dc263cfb1d4aecf67
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722483"
---
# <a name="regsvr32"></a>regsvr32



レジストリ内のコマンド コンポーネントとして .dll ファイルを登録します。



## <a name="syntax"></a>構文

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <DllName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|/U|サーバーの登録を解除します。|
|/s|実行 **Regsvr32** せず、メッセージを表示します。|
|/n|実行 **Regsvr32** 呼び出さずに **DllRegisterServer**します。 (必要、 **/i** パラメーターです)。|
|/i:\<cmdline>|省略可能なコマンドライン文字列を渡します (*cmdline*) に **DllInstall**します。 組み合わせてこのパラメーターを使用する場合、 **/u** 呼び出しパラメーター、 **DllUninstall**します。|
|\<DllName>|登録される .dll ファイルの名前。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="examples"></a>例

Active Directory スキーマの .dll ファイルを登録するには、次のように入力します。
```
regsvr32 schmmgmt.dll
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)