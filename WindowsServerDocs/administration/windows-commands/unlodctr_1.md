---
title: unlodctr
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85a66b521f404358705962078f33af4bec1ebae5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363900"
---
# <a name="unlodctr"></a>unlodctr

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サービスまたはデバイスドライバーのパフォーマンスカウンター名と説明テキストをシステムレジストリから削除します。   

## <a name="syntax"></a>構文  
```  
Unlodctr <DriverName>   
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|\<DriverName >|Windows Server 2003 レジストリから、ドライバーまたはサービス <DriverName> のパフォーマンスカウンターの名前の設定と説明のテキストを削除します。|  
|/?|コマンド プロンプトにヘルプを表示します。|  

## <a name="remarks"></a>コメント  
> [!WARNING]  
> レジストリを正しく編集しないと、システムが正常に動作しなくなる場合があります。 レジストリを変更する前に、コンピューター上の重要なデータのバックアップを作成する必要があります。  

入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (例: "<DriverName>")。  

## <a name="BKMK_Examples"></a>例  
Simple Mail Transfer Protocol (SMTP) サービスの現在のパフォーマンスレジストリ設定とカウンターの説明テキストを削除するには、次の手順を実行します。  
```  
unlodctr SMTPSVC  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
