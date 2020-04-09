---
title: manage-bde WipeFreeSpace 領域
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b8d83a2a-c5c8-4019-9041-23d1d6abf282
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a9995c6872380af61bec5d3b200e733c034ea6b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839715"
---
# <a name="manage-bde-wipefreespace"></a>manage-bde: WipeFreeSpace 領域



空間に存在するデータの断片を削除するボリュームに空き領域を消去します。 使用領域のみの暗号化方法を使用して暗号化されたボリュームでこのコマンドを実行すると、完全ボリューム暗号化の暗号化方法と同じレベルの保護が提供されます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde -WipeFreeSpace|-w [<Drive>] [-Cancel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >|続けて、コロン、ボリューム GUID パス、または、マウントされたボリュームのドライブ文字を表します。|
|-[キャンセル]|プロセスでは、空き領域のクリーン インストールをキャンセルします。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<名 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a><a name=BKMK_Examples></a>例

次の例を使用して、 **-w** を作成するコマンドは、C ドライブの空き領域をワイプ
```
manage-bde -w C:
```
次の例では、- **w**コマンドと **-cancel**パラメーターを使用して、ドライブ C の空き領域のワイプをキャンセルする方法を示します。
```
manage-bde -w -Cancel C:
```

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)