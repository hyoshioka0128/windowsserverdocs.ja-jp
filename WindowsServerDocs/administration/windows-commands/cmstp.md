---
title: cmstp
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0ee5c5189b4eab21994def221dd757b0061ef22d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836383"
---
# <a name="cmstp"></a>cmstp

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

インストールまたは接続マネージャー サービスのプロファイルを削除します。 省略可能なパラメーターを指定せずに使用される**cmstp**オペレーティング システムおよびユーザーのアクセス許可に適切な既定の設定で、サービス プロファイルをインストールします。 
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
|< ServiceProfileFileName >.exe|インストール パッケージをインストールするプロファイルを含むを名前を指定します。<br /><br />構文 2 で必須の構文 1 が有効ではありません。|
|/q:a|ユーザーに確認しないで、プロファイルをインストールすることを指定します。 インストールが成功した確認のメッセージが表示されます。<br /><br />構文 2 で必須の構文 1 が有効ではありません。|
|[ドライブ:][パス]<ServiceProfileFileName>.inf|必須。 プロファイルのインストール方法を決定する構成ファイルを名前を指定します。<br /><br />[ドライブ:] [path] パラメーターは構文 1 では無効です。|
|/nf|サポート ファイルをインストールされていないことを指定します。|
|/ni|デスクトップ アイコンを作成しないことを指定します。 このパラメーターは Windows 95、Windows 98、Windows NT 4.0、または Windows Millennium edition を実行しているコンピューターのみです。|
|/ns|デスクトップ ショートカットを作成しないことを指定します。 このパラメーターは Windows Server 2003 ファミリ、Windows 2000、Windows XP のメンバーを実行しているコンピューターのみです。|
|/s|サービス プロファイルをインストールまたはサイレント (ユーザーからの応答メッセージを表示またはなしの確認メッセージを表示する) をアンインストールすることを指定します。|
|/su|すべてのユーザーではなく、1 人のユーザーのサービスのプロファイルをインストールすることを指定します。 このパラメーターは Windows Server 2003、Windows 2000、または Windows XP を実行しているコンピューターのみです。|
|/au|すべてのユーザーに対してサービス プロファイルをインストールすることを指定します。 このパラメーターは Windows Server 2003、Windows 2000、または Windows XP を実行しているコンピューターのみです。|
|/u|サービス プロファイルをアンインストールすることを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
**/s**と組み合わせて使用できる唯一のパラメーターは、 **/u**します。
構文 1 は、カスタム インストール アプリケーションで使用される一般的な構文です。 この構文を使用することを実行する必要があります**cmstp**を含むディレクトリから、 <ServiceProfileFileName>.exe ファイルです。
## <a name="BKMK_Examples"></a>例
サポート ファイルなしに fiction サービスをインストールするには、次のように入力します。
```
fiction.exe /c:"cmstp.exe fiction.inf /nf"
```
単一のユーザーに fiction サービスをサイレント モードでインストールするには、次のように入力します。
```
fiction.exe /c:"cmstp.exe fiction.inf /s /su"
```
Fiction サービスをサイレント モードでアンインストールするには、次のように入力します。
```
fiction.exe /c:"cmstp.exe fiction.inf /s /u"
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
