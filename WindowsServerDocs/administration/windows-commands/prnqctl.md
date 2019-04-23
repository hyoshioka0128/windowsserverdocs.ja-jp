---
title: prnqctl
description: テスト ページを印刷、一時停止またはプリンターを再開します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8df9dfa7-984c-4276-bb7d-e7675e7c399e jpjofre
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 26af9527b7b16b42fd9d389f3409143dfc3e9aa9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858083"
---
# <a name="prnqctl"></a>prnqctl

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

テスト ページを印刷を一時停止や、プリンターが再開プリンター キューをクリアします。  
  
## <a name="syntax"></a>構文  
```  
cscript Prnqctl {-z | -m | -e | -x | -?} [-s <ServerName>]   
[-p <printerName>] [-u <UserName>] [-w <Password>]  
```  
## <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|~ z|指定されているプリンタで印刷を一時停止、 **-p**パラメーター。|  
|-m|指定されているプリンタで印刷を再開、 **-p** パラメーター。|  
|-e|指定されているプリンタにテスト ページを印刷、 **-p**パラメーター。|  
|-x|指定されているプリンタのすべての印刷ジョブが取り消される、 **-p** パラメーター。|  
|-s \<ServerName>|管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|  
|-p \<printerName>|管理するプリンターの名前を指定します。 必須。|  
|-u \<UserName> -w \<Password>|管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーにこれらのアクセス許可があるが、アクセス許可は、他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。|  
|/?|コマンド プロンプトにヘルプを表示します。|  

## <a name="remarks"></a>注釈  
-   **Prnqctl**コマンドは、%WINdir%\System32\printing_Admin_Scripts にある Visual Basic スクリプト\\<language>ディレクトリ。 このコマンドでは、コマンド プロンプトで、使用する入力**cscript** prnqctl ファイル、または適切なフォルダーにディレクトリを変更する、完全なパスを続けています。 次に、例を示します。  
    ```  
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnqctl  
    ```  
-   入力する情報にスペースが含まれている場合は、テキストを囲む引用符を使用して (たとえば、 `"computer Name"`)。  

## <a name="BKMK_examples"></a>例  
共有される Laserprinter1 プリンターでテスト ページを印刷する、 \\\Server1 コンピューターを入力します。  
```  
cscript Prnqctl -e -s Server1 -p Laserprinter1  
```  
ローカル コンピューター上の Laserprinter1 プリンターで印刷を一時停止には、次のように入力します。  
```  
cscript Prnqctl -z -p Laserprinter1  
```  
ローカル コンピューター上の Laserprinter1 プリンターですべての印刷ジョブを取り消すには、次のように入力します。  
```  
cscript Prnqctl -x -p Laserprinter1  
```  

#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
[印刷コマンドのリファレンス](print-command-reference.md)  
