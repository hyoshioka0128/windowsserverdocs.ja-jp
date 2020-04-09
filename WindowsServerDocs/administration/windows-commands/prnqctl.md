---
title: prnqctl
description: テストページを印刷するか、プリンターを一時停止または再開します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8df9dfa7-984c-4276-bb7d-e7675e7c399e jpjofre
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: d07d8caa0568b26f5edc16258085a59ecdafcf4e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837205"
---
# <a name="prnqctl"></a>prnqctl

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

テスト ページを印刷を一時停止や、プリンターが再開プリンター キューをクリアします。  

## <a name="syntax"></a>構文  
```  
cscript Prnqctl {-z | -m | -e | -x | -?} [-s <ServerName>]   
[-p <printerName>] [-u <UserName>] [-w <Password>]  
```  
### <a name="parameters"></a>パラメーター  

|パラメーター|説明|  
|-------|--------|  
|~ z|**-p**パラメーターを使用して指定されたプリンターの印刷を一時停止します。|  
|-m|指定されているプリンタで印刷を再開、 **-p** パラメーター。|  
|-e|**-p**パラメーターを使用して指定されたプリンターにテストページを印刷します。|  
|-x|指定されているプリンタのすべての印刷ジョブが取り消される、 **-p** パラメーター。|  
|-s \<ServerName >|管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|  
|-p \<printerName >|管理するプリンターの名前を指定します。 必須。|  
|-u \<UserName >-w \<パスワード >|管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーにこれらのアクセス許可があるが、アクセス許可は、他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。|  
|/?|コマンド プロンプトでヘルプを表示します。|  

## <a name="remarks"></a>コメント  
- **Prnqctl.vbs**コマンドは、%windir%\system32\ printing_Admin_Scripts\\<language> ディレクトリにある Visual Basic スクリプトです。 このコマンドを使用するには、コマンドプロンプトで「 **cscript** 」と入力し、prnqctl.vbs ファイルへの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 例 :  
  ```  
  cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnqctl  
  ```  
- 入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (`"computer Name"`など)。  

## <a name="examples"></a><a name="BKMK_examples"></a>例  
\\Server1 コンピューターによって共有されている Laserprinter1 プリンターでテストページを印刷するには、次のように入力します。  
```  
cscript Prnqctl -e -s Server1 -p Laserprinter1  
```  
ローカルコンピューター上の Laserprinter1 プリンターで印刷を一時停止するには、次のように入力します。  
```  
cscript Prnqctl -z -p Laserprinter1  
```  
ローカルコンピューター上の Laserprinter1 プリンターのすべての印刷ジョブをキャンセルするには、次のように入力します。  
```  
cscript Prnqctl -x -p Laserprinter1  
```  

## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
[印刷コマンドのリファレンス](print-command-reference.md)  
