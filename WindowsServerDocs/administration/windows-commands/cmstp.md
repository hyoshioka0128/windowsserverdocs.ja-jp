---
title: cmstp
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34aad544-11c3-4e85-8bbf-5bc5a971da93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd2e8dbb08b41875335b35dd802007a0bd1fbd41
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379269"
---
# <a name="cmstp"></a>cmstp

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

接続マネージャーサービスプロファイルをインストールまたは削除します。 オプションのパラメーターを指定せずに、 **cmstp.exe**では、オペレーティングシステムとユーザーのアクセス許可に適した既定の設定を使用してサービスプロファイルがインストールされます。 
## <a name="syntax"></a>構文
構文 1:
```
ServiceProfileFileName .exe /q:a /c:"cmstp.exe ServiceProfileFileName .inf [/nf] [/ni] [/ns] [/s] [/su] [/u]"
```
構文 2:
```
cmstp.exe [/nf] [/ni] [/ns] [/s] [/su] [/u]  [Drive:][path]ServiceProfileFileName.inf"
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|< >|インストールするプロファイルを含むインストールパッケージを名前で指定します。<br /><br />構文1では必須ですが、構文2では無効です。|
|/q:a|ユーザーにメッセージを表示せずにプロファイルをインストールするように指定します。 インストールが成功したことを示す確認メッセージが引き続き表示されます。<br /><br />構文1では必須ですが、構文2では無効です。|
|[ドライブ:][パス] <ServiceProfileFileName>.inf|必須。 プロファイルのインストール方法を決定する構成ファイルを名前で指定します。<br /><br />[Drive:] [path] パラメーターは、構文1では無効です。|
|/nf|サポートファイルをインストールしないことを指定します。|
|/ni|デスクトップアイコンを作成しないことを指定します。 このパラメーターは、Windows 95、Windows 98、Windows NT 4.0、または Windows Millennium edition を実行しているコンピューターでのみ有効です。|
|/ns|デスクトップショートカットを作成しないことを指定します。 このパラメーターは、Windows Server 2003 ファミリ、Windows 2000、または Windows XP のメンバーを実行しているコンピューターでのみ有効です。|
|/s|サービスプロファイルをサイレントインストールまたはアンインストールすることを指定します (ユーザーの応答を求めたり、確認メッセージを表示したりする必要はありません)。|
|/su|サービスプロファイルをすべてのユーザーではなく、1人のユーザーにインストールするように指定します。 このパラメーターは、Windows Server 2003、Windows 2000、または Windows XP を実行しているコンピューターでのみ有効です。|
|/au|すべてのユーザーにサービスプロファイルをインストールする必要があることを指定します。 このパラメーターは、Windows Server 2003、Windows 2000、または Windows XP を実行しているコンピューターでのみ有効です。|
|/u|サービスプロファイルをアンインストールする必要があることを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
**/s**は、 **/u**と組み合わせて使用できる唯一のパラメーターです。
構文1は、カスタムインストールアプリケーションで使用される一般的な構文です。 この構文を使用するには、<ServiceProfileFileName>の .exe ファイルが格納されているディレクトリから**cmstp.exe**を実行する必要があります。
## <a name="BKMK_Examples"></a>例
サポートファイルを使用せずに、架空のサービスプロファイルをインストールするには、次のように入力します。
```
fiction.exe /c:"cmstp.exe fiction.inf /nf"
```
1人のユーザーの架空のサービスプロファイルをサイレントインストールするには、次のように入力します。
```
fiction.exe /c:"cmstp.exe fiction.inf /s /su"
```
架空のサービスプロファイルをサイレントモードでアンインストールするには、次のように入力します。
```
fiction.exe /c:"cmstp.exe fiction.inf /s /u"
```
## <a name="additional-references"></a>その他の参照情報
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
