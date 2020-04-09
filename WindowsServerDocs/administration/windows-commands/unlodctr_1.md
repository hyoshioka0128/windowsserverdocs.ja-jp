---
title: unlodctr
description: Unlodctr の Windows コマンドのトピックでは、システムレジストリからサービスまたはデバイスドライバーのパフォーマンスカウンターの名前と説明テキストを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe7fc3c9eafefd59a5daab625e3af06b6addd292
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832259"
---
# <a name="unlodctr"></a>unlodctr

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サービスまたはデバイスドライバーの**パフォーマンスカウンター**名と**説明**テキストをシステムレジストリから削除します。   

## <a name="syntax"></a>構文  
```  
Unlodctr <DriverName>   
```  
#### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|\<ドライバーの >|Windows Server 2003 レジストリから、ドライバーまたはサービス <DriverName> のパフォーマンスカウンターの名前の設定と説明のテキストを削除します。|  
|/?|コマンド プロンプトでヘルプを表示します。|  

## <a name="remarks"></a>コメント  
> [!WARNING]  
> レジストリの編集を誤ると、システムに重大な損害を与える可能性があります。 レジストリを変更する前に、コンピューター上の重要なデータのバックアップを作成する必要があります。  

入力する情報にスペースが含まれる場合は、テキストを囲む引用符を使用して (たとえば、 <DriverName>)。  

## <a name="examples"></a><a name=BKMK_Examples></a>例  
Simple Mail Transfer Protocol (SMTP) サービスの現在のパフォーマンスレジストリ設定とカウンターの説明テキストを削除するには、次の手順を実行します。  
```  
unlodctr SMTPSVC  
```  
## <a name="additional-references"></a>その他の参照情報  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
