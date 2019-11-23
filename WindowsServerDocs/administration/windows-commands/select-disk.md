---
title: select disk
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0da614b-09d9-433b-b4eb-9127f84431cb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6d9078242264b01ee4bc24dc590df24b1e53e548
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371081"
---
# <a name="select-disk"></a>select disk

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたディスクを選択し、そのディスクにフォーカスを移動します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
select disk={ <n> | <disk path> | system | next }  
```  
  
> [!NOTE]  
> **<disk path>** 、**システム**、および**次**のパラメーターは、Windows 7 および windows Server 2008 R2 でのみ使用できます。  
  
## <a name="parameters"></a>パラメーター  
  
|  パラメーター  |                                                                                                                                                                                                            説明                                                                                                                                                                                                            |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     <n>     | フォーカスを受け取るディスクの数を指定します。 コンピューター上のすべてのディスク番号を表示するにを使用して、 **リスト ディスク** diskpart コマンドです。 **注:** システムを複数のディスクを構成する場合は使用しないでください **select ディスク\=0** システム ディスクを指定します。 コンピューターは、コンピュータを再起動して、同じディスク構成を持つ別のコンピューターが別のディスク番号を持つ場合、ディスク番号を再割り当てできます。 |
| <disk path> |                                                                                                                 フォーカスを受け取るディスクの場所を指定します。たとえば、 **PCIROOT\(0\)\#PCI\(0F02\)\#atA\(C00T00L00\)** です。 ディスクの場所のパスを表示するには、それを選択し、入力 **詳細ディスク**します。                                                                                                                  |
|   システム    |                                 BIOS コンピューターにそのディスク 0 のフォーカスを指定します。 コンピューターでは EFI、EFI システム パーティションを含むディスク \(ESP\) ために使用される現在のブートがフォーカスを受け取るためです。 EFI コンピューターでは、esp が存在しない場合、または ESP が複数ある場合、コマンドは失敗します。または、Windows プレインストール環境 \(Windows PE\)からコンピューターが起動されます。                                  |
|    次へ     |                                                                                                                                     ディスクを選択すると、このコマンドは、そのディスクの一覧のすべてのディスクを反復します。 このコマンドを実行すると、一覧の次のディスクがフォーカスを受け取る。                                                                                                                                      |
  
## <a name="BKMK_examples"></a>例  
ディスク 1 にフォーカスを切り替えるには、次のように入力します。  
  
```  
select disk=1  
```  
  
ディスクを選択して、その場所のパスを使用して、次のように入力します。  
  
```  
select disk=PCIROOT(0)#PCI(0100)#atA(C00T00L01)  
```  
  
システム ディスクにフォーカスを次のように入力します。  
  
```  
select disk=system  
```  
  
フォーカスを次のディスクをコンピューターに、次のように入力します。  
  
```  
select disk=next  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

