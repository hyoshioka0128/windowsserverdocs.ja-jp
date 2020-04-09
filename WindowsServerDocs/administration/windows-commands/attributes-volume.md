---
title: 属性のボリューム
description: Windows コマンドに関するトピックでは、ボリュームの属性を表示、設定、またはクリアする**属性ボリューム**について説明しています。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e40e8284-3d57-4de8-a46c-e4ade34a0d53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 00991cdba57f0728cfa348dea2b0916ad758b34a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851235"
---
# <a name="attributes-volume"></a>属性のボリューム

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ボリュームの属性を表示、設定、またはクリアします。

## <a name="syntax"></a>構文  

```
attributes volume [{set | clear}] [{hidden | readonly | nodefaultdriveletter | shadowcopy}] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
| パラメーター | 説明 |  
| ------- | -------- |  
| set | フォーカスがあるボリュームの指定された属性を設定します。 |  
| クリア | フォーカスがあるボリュームの指定された属性をクリアします。 |  
| readonly | ボリュームを読み取り専用に指定します。 |  
| hidden | ボリュームを非表示に指定します。 |  
| nodefaultdriveletter | ボリュームに既定のドライブ文字を割り当てないように指定します。 |  
| shadowcopy | ボリュームをシャドウ コピー ボリュームに指定します。 |  
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |  
  
## <a name="remarks"></a>コメント  
  
- ベーシックマスタブートレコード (MBR) ディスクでは、 **hidden**、 **readonly**、および**nodefaultdriveletter**各パラメータがディスク上のすべてのボリュームに適用されます。  
  
- 基本的な GUID パーティションテーブル (GPT) ディスク、およびダイナミック MBR および GPT ディスクでは、 **hidden**、 **readonly**、および**nodefaultdriveletter**各パラメーターは、選択したボリュームにのみ適用されます。  
  
- **属性 volume**コマンドを正常に実行するには、ボリュームを選択する必要があります。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。  
  
## <a name="examples"></a><a name=BKMK_examples></a>例

選択したボリュームの現在の属性を表示するには、次のように入力します。  
  
```
attributes volume  
```  
  
選択したボリュームを非表示または読み取り専用として設定するには、次のように入力します。  
  
```
attributes volume set hidden readonly  
```  
  
選択したボリュームの非表示属性と読み取り専用属性を削除するには、次のように入力します。  
  
```
attributes volume clear hidden readonly  
```  
  
## <a name="additional-references"></a>その他の参照情報  

- [コマンド ライン構文の記号](command-line-syntax-key.md)