---
title: pnpunattend
description: コンピューターでは、デバイス ドライバーし、ドライバーのサイレント インストールを実行する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fa88932-cff0-4dfc-936c-98c0e3dfbeb8 britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 7aa09636f8c23678f003bfa5ebf8be164e7fc683
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879523"
---
# <a name="pnpunattend"></a>pnpunattend

デバイス ドライバー用にコンピューターを監査およびドライバーの無人インストールを実行またはドライバーをインストールしなくても検索され、必要に応じて、コマンドラインに結果を報告します。 このコマンドを使用して、特定のハードウェア デバイスの特定のドライバーのインストールを指定します。 注釈をご覧ください。

## <a name="syntax"></a>構文

```
PnPUnattend.exe auditSystem [/help] [/?] [/h] [/s] [/L]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|auditSystem|オンラインでのドライバーのインストールを指定します。</br>必要に応じて、する場合を除く**pnpunattend**いずれかで実行される、 **/help**または **/でしょうか。** パラメーター。|
|/s|任意。 インストールしなくてもドライバーの検索を指定します。|
|/L|(省略可能)。 コマンド プロンプトで、このコマンドのログ情報を指定します。|
|/?|任意。 コマンド プロンプトで次のコマンドのヘルプを表示します。|

## <a name="remarks"></a>注釈

準備が必要です。 このコマンドを使用する前に、次のタスクを完了する必要があります。

1.  インストールするドライバー用のディレクトリを作成します。 たとえばでフォルダーを作成 **C:\Drivers\Video** のビデオ アダプターのドライバーです。
2.  ダウンロードして、デバイスのドライバー パッケージを抽出します。 オペレーティング システムのバージョンの INF ファイルを含むサブフォルダーおよびサブフォルダーの内容を作成したビデオ フォルダーにコピーします。 たとえば、ビデオ ドライバー ファイルを C:\Drivers\Video にコピーします。
3.  たとえば、手順 1. で作成したフォルダーにシステム環境のパス変数を追加 **C:\Drivers\Video**します。
4.  次のレジストリ キーを作成し、 **DriverPaths** キーセットを作成する、 **値のデータ** に **1**します。
-   レジストリ パスの移動の Windows® 7: **hkey_local_machine \software\microsoft\windows \currentversion\**、し、キーを作成します **\pnpunattend\driverpaths。\**
-   Windows Vista では、レジストリ パスに移動します **hk_lm \software\microsoft\windows \currentversion\**、キーを作成し = **\UnattendSettings\PnPUnattend\DriverPaths** .

## <a name="examples"></a>例

次のコマンド例は、使用する方法を示します、 **PNPUnattend.exe**ドライバーの更新、コンピューターを監査し、コマンド プロンプトに結果をレポートします。

```
pnpunattend auditsystem /s /l 
```

## <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)