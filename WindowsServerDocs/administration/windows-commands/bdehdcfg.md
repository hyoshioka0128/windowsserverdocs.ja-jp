---
title: bdehdcfg
description: '**Bdehdcfg**の Windows コマンドに関するトピックでは、BitLocker ドライブ暗号化に必要なパーティションを使用してハードドライブを準備します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: acfe2582905402f7be149148520784be6ad47453
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382191"
---
# <a name="bdehdcfg"></a>bdehdcfg



BitLocker ドライブ暗号化に必要なパーティションを使用してハードドライブを準備します。 BitLocker セットアップには、必要に応じてドライブを準備および再パーティションする機能が含まれているため、Windows 7 のほとんどのインストールでこのツールを使用する必要はありません。

> [!WARNING]
> コンピューターの構成 \ 管理用テンプレート \Windows コンポーネント \Bitlocker ドライブ暗号化 \ 固定データドライブにある [グループポリシー **BitLocker で保護されていない固定ドライブへの書き込みアクセスを拒否する**] 設定との間に既知の競合があります。.</br>このポリシー設定を有効にしたときに、コンピューターで Bdehdcfg が実行されている場合、次の問題が発生する可能性があります: ></br>>-ドライブを圧縮してシステムドライブを作成しようとすると、ドライブサイズが正常に縮小され、未加工のパーティションが作成されます。 ただし、初期化されていないパーティションはフォーマットされていません。 次のエラーメッセージが表示されます。"新しいアクティブドライブはフォーマットできません。 ドライブを BitLocker 用に手動で準備する必要がある可能性があります。」</br>>-未割り当て領域を使用してシステムドライブを作成しようとすると、未加工のパーティションが作成されます。 ただし、初期化されていないパーティションはフォーマットされていません。 次のエラーメッセージが表示されます。"新しいアクティブドライブはフォーマットできません。 ドライブを BitLocker 用に手動で準備する必要がある可能性があります。」</br>>-既存のドライブをシステムドライブにマージしようとすると、システムドライブを作成するために必要なブートファイルをターゲットドライブにコピーすることができません。 次のエラーメッセージが表示されます。"BitLocker セットアップでブートファイルをコピーできませんでした。 ドライブを BitLocker 用に手動で準備する必要がある可能性があります。」</br>> このポリシー設定が適用されている場合は、ドライブが保護されているため、ハードドライブを再パーティション分割できません。 組織内のコンピューターを以前のバージョンの Windows からアップグレードする場合に、それらのコンピューターに1つのパーティションが構成されている場合は、そのコンピューターにポリシー設定を適用する前に、必要な BitLocker システムパーティションを作成する必要があります。

このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
bdehdcfg [–driveinfo <DriveLetter>] [-target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}] [–newdriveletter] [–size <SizeinMB>] [-quiet]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[Bdehdcfg: driveinfo](bdehdcfg-driveinfo.md)|ドライブ文字、合計サイズ、最大空き領域、および指定されたドライブ上のパーティションのパーティション特性が表示されます。 有効なパーティションだけが一覧表示されます。 4つのプライマリパーティションまたは拡張パーティションが既に存在する場合、未割り当ての領域は表示されません。|
|[Bdehdcfg: ターゲット](bdehdcfg-target.md)|システムドライブとして使用するドライブの部分を定義し、その部分をアクティブにします。|
|[Bdehdcfg: newdriveletter](bdehdcfg-newdriveletter.md)|システムドライブとして使用されるドライブの部分に新しいドライブ文字を割り当てます。|
|[Bdehdcfg: サイズ](bdehdcfg-size.md)|新しいシステムドライブを作成するときのシステムパーティションのサイズを決定します。|
|[Bdehdcfg: quiet](bdehdcfg-quiet.md)|コマンドラインインターフェイスにすべてのアクションとエラーが表示されないようにします。 Bdehdcfg は、後続のドライブの準備中に発生する可能性がある "yes" または "No" の応答を使用するように指示します。|
|[Bdehdcfg: 再起動](bdehdcfg-restart.md)|ドライブの準備が完了した後で、コンピューターを再起動するように指示します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="BKMK_Examples"></a>例

次の例では、500 MB のシステムパーティションを作成するために、既定のドライブと共に使用されている Bdehdcfg を示しています。 ドライブ文字が指定されていないため、新しいシステムパーティションにはドライブ文字がありません。
```
bdehdcfg -target default -size 500
```
次の例では、システムパーティション (P:) を作成するために既定のドライブと共に使用されている Bdehdcfg を示しています。ドライブの未割り当て領域の既定のサイズ (300 MB)。 このツールでは、ユーザーに対してさらに入力を求めたり、エラーが表示されたりすることはありません。 システムドライブが作成されると、コンピューターが自動的に再起動します。
```
bdehdcfg -target unallocated –newdriveletter P: -quiet -restart
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)