---
title: bdehdcfg
description: Windows コマンド」のトピック**bdehdcfg** -BitLocker ドライブ暗号化のために必要なパーティションを含むハード ドライブを準備します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c92cd74-188e-4fec-b7c4-fe4e8903e032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4fda562f4aa6b8caa885fcd70155b7150c91d12
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869703"
---
# <a name="bdehdcfg"></a>bdehdcfg



BitLocker ドライブ暗号化のために必要なパーティションを含むハード ドライブを準備します。 Windows 7 のインストールのほとんどは、BitLocker のセットアップに準備し、必要に応じてドライブのパーティションを再作成する機能が含まれているために、このツールを使用する必要はありません。

> [!WARNING]
> 既知の競合がある、 **BitLocker で保護されていない固定ドライブへの書き込みアクセスを拒否**グループ ポリシー設定の場所で**コンピューターの構成 \ 管理用テンプレート \windows コンポーネント \bitlocker\Bitlocker データ ドライブのドライブ**します。</br>> このポリシー設定を有効にすると、Bdehdcfg はコンピューターで実行される場合は、次の問題が発生する可能性があります。</br>> - ドライブを圧縮して、システム ドライブを作成しようとする場合に、ドライブのサイズが減少して、未処理のパーティションが作成されます。 ただし、初期化されていないパーティションはフォーマットされていません。 次のエラー メッセージが表示されます。"新しいアクティブ ドライブをフォーマットすることはできません。 ドライブを BitLocker 用に手動で準備する必要がある可能性があります。」</br>> の場合、システム ドライブを作成する未割り当て領域を使用しようとすると、未処理のパーティションが作成されます。 ただし、初期化されていないパーティションはフォーマットされていません。 次のエラー メッセージが表示されます。"新しいアクティブ ドライブをフォーマットすることはできません。 ドライブを BitLocker 用に手動で準備する必要がある可能性があります。」</br>>-既存のドライブをシステム ドライブにマージしようとすると、システム ドライブを作成するターゲット ドライブに必要なブート ファイルをコピーするツールは失敗します。 次のエラー メッセージが表示されます。"BitLocker のセットアップにブート ファイルをコピーできませんでした。 ドライブを BitLocker 用に手動で準備する必要がある可能性があります。」</br>> このポリシー設定が適用されている場合、ドライブが保護されているためにハード ドライブを直すことはできません。 Windows の以前のバージョンから、組織内のコンピューターをアップグレードして、これらのコンピューターが 1 つのパーティションで構成された場合、は、コンピューターにポリシー設定を適用する前に必要な BitLocker システム パーティションを作成する必要があります。

このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
bdehdcfg [–driveinfo <DriveLetter>] [-target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}] [–newdriveletter] [–size <SizeinMB>] [-quiet]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[Bdehdcfg: driveinfo](bdehdcfg-driveinfo.md)|指定されたドライブ上のドライブ文字、合計サイズ、最大の空き領域、およびパーティションのパーティションの特性を表示します。 有効なパーティションのみが一覧表示されます。 4 つのプライマリまたは拡張パーティションが既に存在する場合は、未割り当て領域は表示されません。|
|[Bdehdcfg: target](bdehdcfg-target.md)|システム ドライブとして使用するドライブをのどの部分を定義し、部分をアクティブになります。|
|[Bdehdcfg: newdriveletter](bdehdcfg-newdriveletter.md)|システム ドライブとして使用されるドライブの領域に新しいドライブ文字を割り当てます。|
|[bdehdcfg: サイズ](bdehdcfg-size.md)|新しいシステム ドライブを作成するときは、システム パーティションのサイズを決定します。|
|[Bdehdcfg: quiet](bdehdcfg-quiet.md)|すべての操作やコマンド ライン インターフェイスでエラーが表示されないようにし、[はい] に"Yes"の応答を使用する Bdehdcfg]、[ドライブの準備に後続の中に発生する画面の指示はないです。|
|[bdehdcfg: 再起動](bdehdcfg-restart.md)|ドライブの準備が完了した後に再起動するコンピューターに指示します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="BKMK_Examples"></a>例

次の例は、500 MB のシステム パーティションを作成する既定のドライブで使用されている Bdehdcfg を示しています。 ドライブ文字が指定されていないため、新しいシステム パーティションには、ドライブ文字はありません。
```
bdehdcfg -target default -size 500
```
次の例では、システム パーティション (p:) を作成する既定のドライブで使用されている Bdehdcfg を示しています。ドライブ上の未割り当て領域外の 300 MB の既定のサイズ。 ツールは、ユーザーにさらに、入力を求めないも、すべてのエラーが表示されます。 システム ドライブが作成されたら、コンピューターは自動的に再起動します。
```
bdehdcfg -target unallocated –newdriveletter P: -quiet -restart
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)