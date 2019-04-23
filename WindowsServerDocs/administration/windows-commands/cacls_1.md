---
title: cacls
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5bdbaaa-4557-48b8-80df-e75ee0d2f27d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 289015ff580d7e2fba5ff911878028f5302cab8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838083"
---
# <a name="cacls"></a>cacls

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

表示または指定したファイルの随意アクセス制御リスト (DACL) を変更します。  
## <a name="syntax"></a>構文  
```  
cacls <filename> [/t] [/m] [/l] [/s[:sddl]] [/e] [/c] [/g user:<perm>] [/r user [...]] [/p user:<perm> [...]] [/d user [...]]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|\<filename\>|必須。 指定されたファイルの Acl を表示します。|  
|/t|現在のディレクトリとすべてのサブディレクトリ内の指定されたファイルの Acl を変更します。|  
|/m|ディレクトリにマウントされているボリュームの Acl を変更します。|  
|/l|ターゲットと自体シンボリック リンクで機能します。|  
|/s:sddl|SDDL 文字列で指定されている Acl を置き換えます (無効と **/e**、 **/g**、 **/r**、 **/p**、または **/d**).|  
|/e|置換することではなく、ACL を編集します。|  
|/c|アクセス拒否エラーが継続します。|  
|/g user:\<perm\>|許可は、ユーザー アクセス権を指定します。<br /><br />アクセス許可の有効な値:<br /><br />-n-なし<br />-   r - read<br />-   w - write<br />-c の変更 (書き込み)<br />-f - フル コントロール|  
|/r ユーザー [...]|指定したユーザーのアクセス権を取り消す (で唯一の有効な **/e**)。|  
|[ユーザーの/p:\<perm\> [...]|指定したユーザーのアクセス権を置き換えます。<br /><br />アクセス許可の有効な値:<br /><br />-n-なし<br />-   r - read<br />-   w - write<br />-c の変更 (書き込み)<br />-f - フル コントロール|  
|[/d ユーザー [...]|指定したユーザーのアクセスを拒否します。|  
|/?|コマンド プロンプトにヘルプを表示します。|  
## <a name="remarks"></a>注釈  
-   このコマンドは廃止されました。 使用してください[icacls](icacls.md)代わりにします。  
-   結果を解釈するのにには、次の表を使用します。  

    |出力|アクセス制御エントリ (ACE) を適用するには|  
    |-----|----------------------|  
    |OI|オブジェクトを継承します。 このフォルダーおよびファイルです。|  
    |CI|コンテナーを継承します。 このフォルダーとサブフォルダー。|  
    |IO|のみを継承します。 ACE は、現在のファイル/ディレクトリには適用されません。|  
    |出力メッセージはありません。|このフォルダーのみです。|  
    |(OI)(CI)|このフォルダー、サブフォルダー、およびファイル|  
    |(OI)(CI)(IO)|サブフォルダーとファイルのみです。|  
    |(CI)(IO)|サブフォルダーのみです。|  
    |(OI)(IO)|ファイルのみです。|  

-   ワイルドカードを使用することができます (**でしょうか。** **\***) を複数のファイルを指定します。  
-   1 つ以上のユーザーを指定することができます。  

#### <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)   
-   [icacls](icacls.md)  
