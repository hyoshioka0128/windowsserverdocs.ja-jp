---
title: pnpunattend
description: コンピューターのデバイスドライバーを監査する方法と、サイレントドライバインストールを実行する方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fa88932-cff0-4dfc-936c-98c0e3dfbeb8 britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 569b879caf29aac6d1592d822072f35021cec9d3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723303"
---
# <a name="pnpunattend"></a>pnpunattend

デバイス ドライバー用にコンピューターを監査およびドライバーの無人インストールを実行またはドライバーをインストールしなくても検索され、必要に応じて、コマンドラインに結果を報告します。 このコマンドを使用して、特定のハードウェア デバイスの特定のドライバーのインストールを指定します。 「解説」を参照してください。

## <a name="syntax"></a>構文

```
PnPUnattend.exe auditSystem [/help] [/?] [/h] [/s] [/L]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|auditSystem|オンラインでのドライバーのインストールを指定します。</br>**Pnpunattend**が **/help**または **/?** のいずれかで実行されている場合を除き、必須です。 %2!d! です。|
|/s|任意。 インストールしなくてもドライバーの検索を指定します。|
|/L|任意。 コマンド プロンプトで、このコマンドのログ情報を指定します。|
|/?|任意。 コマンド プロンプトで次のコマンドのヘルプを表示します。|

## <a name="remarks"></a>Remarks

準備が必要です。 このコマンドを使用する前に、次のタスクを完了する必要があります。

1. インストールするドライバー用のディレクトリを作成します。 たとえばでフォルダーを作成 **C:\Drivers\Video** のビデオ アダプターのドライバーです。
2. ダウンロードして、デバイスのドライバー パッケージを抽出します。 オペレーティング システムのバージョンの INF ファイルを含むサブフォルダーおよびサブフォルダーの内容を作成したビデオ フォルダーにコピーします。 たとえば、ビデオ ドライバー ファイルを C:\Drivers\Video にコピーします。
3. たとえば、手順 1. で作成したフォルダーにシステム環境のパス変数を追加 **C:\Drivers\Video**します。
4. 次のレジストリ キーを作成し、 **DriverPaths** キーセットを作成する、 **値のデータ** に **1**します。
5. Windows®7の場合は、レジストリパス**HKEY_LOCAL_Machine \software\microsoft\windows NT\CurrentVersion\\**に移動し、キー **UnattendSettings\PnPUnattend\DriverPaths\\ **を作成します。
6. Windows Vista では、レジストリ パスに移動: **HK_LM\Software\Microsoft\Windows \currentversion\\**, 、キーを作成し、= **\UnattendSettings\PnPUnattend\DriverPaths**します。

## <a name="examples"></a>例

**PNPUnattend**を使用して、可能なドライバーの更新についてコンピューターを監査し、結果をコマンドプロンプトに報告する方法を示します。

```
pnpunattend auditsystem /s /l 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)