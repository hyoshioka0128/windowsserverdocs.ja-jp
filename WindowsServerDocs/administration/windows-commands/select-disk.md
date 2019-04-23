---
title: select disk
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6e8352b45cf3a46f14828c9c6796e4ec73499d5a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858963"
---
# <a name="select-disk"></a>select disk

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたディスクを選択し、それに、フォーカスを移動します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
select disk={ <n> | <disk path> | system | next }  
```  
  
> [!NOTE]  
> **<disk path>**、**システム**、および**次**パラメーターは、Windows 7 および Windows Server 2008 R2 で使用できるのみです。  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|<n>|フォーカスを受け取るディスクの数を指定します。 コンピューター上のすべてのディスク番号を表示するにを使用して、 **リスト ディスク** diskpart コマンドです。 **注:** 複数のディスクにシステムを構成するときに使用しないでください**select ディスク\=0**システム ディスクを指定します。 コンピューターは、コンピュータを再起動して、同じディスク構成を持つ別のコンピューターが別のディスク番号を持つ場合、ディスク番号を再割り当てできます。|  
|<disk path>|たとえば、フォーカスを受け取るディスクの場所を指定します**PCIROOT\(0\)\#PCI\(0F02\)\#atA\(C00T00L00\)** . ディスクの場所のパスを表示するには、それを選択し、入力 **詳細ディスク**します。|  
|システム|BIOS コンピューターにそのディスク 0 のフォーカスを指定します。 コンピューターでは EFI、EFI システム パーティションを含むディスク \(ESP\) ために使用される現在のブートがフォーカスを受け取るためです。 1 つ以上の ESP がある場合、ESP がないか、Windows プレインストール環境から、コンピューターが起動と EFI コンピューターで、コマンドが失敗\(Windows PE\)します。|  
|次へ|ディスクを選択すると、このコマンドは、そのディスクの一覧のすべてのディスクを反復します。 このコマンドを実行すると、一覧の次のディスクがフォーカスを受け取る。|  
  
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
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

  

