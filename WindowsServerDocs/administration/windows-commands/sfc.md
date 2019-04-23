---
title: sfc
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c58c25da-e028-42a6-9e10-973484a4b953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1db0ab81c9469c88ddb64a367a9dc98a1fd9b70c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832393"
---
# <a name="sfc"></a>sfc

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

スキャンし、保護されているすべてのシステムの整合性がファイルし、正しいバージョンと正しくないバージョンが置き換えられますことを確認します。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文
```
sfc [/scannow] [/verifyonly] [/scanfile=<file>] [/verifyfile=<file>] [/offwindir=<offline windows directory> /offbootdir=<offline boot directory>]
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/scannow|すべての保護されたシステム ファイルの整合性をスキャンし、可能であれば、問題のあるファイルを修復します。|
|/verifyonly|すべての保護されたシステム ファイルの整合性をスキャンします。 修復操作は実行されません。|
|/scanfile|指定されたファイルの整合性をスキャンし、可能であれば、問題が検出された場合、ファイルを修復します。|
|\<file>|指定した完全なパスとファイル名|
|/verifyfile|指定したファイルの整合性を確認します。 修復操作は実行されません。|
|/offwindir|オフライン修復用のオフラインの windows ディレクトリの場所を指定します。|
|/offbootdir|オフラインのオフライン ブート ディレクトリの場所を指定します|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   実行する管理者グループのメンバーとしてログオンする必要があります **sfc.exe**します。
-   場合**sfc**検出こと、保護されたファイルが上書きされている、元のファイルの正しいバージョンを取得、 **systemroot \system32\dllcache**フォルダー、正しくないファイルを置き換えます。
-   機能の違いがある**sfc** Windows Server 2003、Windows Server 2008、および Windows Server 2008 R2:
-   詳細については**sfc** Windows Server 2003 では、次を参照してください。[記事 310747](https://go.microsoft.com/fwlink/?LinkId=227069)マイクロソフト サポート技術情報でします。
-   詳細については**sfc** 、Windows Server 2008 および Windows Server 2008 R2 では、次を参照してください。[システム ファイル チェッカー](https://go.microsoft.com/fwlink/?LinkId=227071)します。

## <a name="BKMK_examples"></a>例
確認する、 **kernel32.dll ファイル**, 、種類。
```
sfc /verifyfile=c:\windows\system32\kernel32.dll
```
セットアップのオフライン修復するには、 **kernel32.dll** 設定オフライン ブート ディレクトリとファイル **d:** とオフラインの windows ディレクトリに設定 **d:\windows**, 、種類。
```
sfc /scanfile=d:\windows\system32\kernel32.dll /offbootdir=d:\ /offwindir=d:\windows
```

## <a name="additional-references"></a>その他の参照情報
-   [コマンドライン構文キー](command-line-syntax-key.md)

