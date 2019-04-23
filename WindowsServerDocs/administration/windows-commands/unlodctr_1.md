---
title: unlodctr
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: e1a662da10acc65b4ad2fd0d055cf9d46de603be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886653"
---
# <a name="unlodctr"></a>unlodctr

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

システム レジストリからパフォーマンス カウンターの名前と説明のテキストをサービスまたはデバイス ドライバーを削除します。   

## <a name="syntax"></a>構文  
```  
Unlodctr <DriverName>   
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|\<ドライバー名 >|カウンター名の設定とドライバーやサービスの説明テキストを削除パフォーマンス<DriverName>Windows Server 2003 のレジストリから。|  
|/?|コマンド プロンプトにヘルプを表示します。|  

## <a name="remarks"></a>注釈  
> [!WARNING]  
> レジストリを正しく編集しないと、システムが正常に動作しなくなる場合があります。 レジストリを変更する前に、コンピューター上の重要なデータのバックアップを作成する必要があります。  

入力する情報にスペースが含まれている場合は、テキストを囲む引用符を使用して (たとえば、"<DriverName>")。  

## <a name="BKMK_Examples"></a>例  
現在のパフォーマンスのレジストリ設定を解除し、簡易メール転送プロトコル (SMTP) サービスの説明テキストをカウンターします。  
```  
unlodctr SMTPSVC  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
  
