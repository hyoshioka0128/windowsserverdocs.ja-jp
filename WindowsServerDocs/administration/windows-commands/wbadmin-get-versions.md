---
title: wbadmin get バージョン
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b986acc4-d083-4d32-9434-862314ed5e97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e4ebbd0d78de0ffbff1ee8c658d6d9811b87df1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813533"
---
# <a name="wbadmin-get-versions"></a>wbadmin get バージョン



詳細については、ローカル コンピューターまたは別のコンピューターに保存されている使用可能なバックアップを一覧表示します。 このサブコマンドを使用して、パラメーターを指定せず、それらのバックアップが利用できない場合でも、ローカル コンピューターのすべてのバックアップが一覧表示します。 バックアップの詳細情報には、バックアップの時刻、バックアップ記憶域の場所、バージョン識別子が含まれます (に必要な**wbadmin 項目を取得**サブコマンドと回復を実行する)、および種類の回復を行うことができます。

このサブコマンドを使用して、使用可能なバックアップに関する詳細を取得するには、メンバーである、 **Backup Operators**グループまたは**管理者**グループ、またはをされている必要が適切な委任アクセス許可。 さらに、実行する必要があります **wbadmin** 管理者特権でコマンド プロンプトからです。 (管理者特権でコマンド プロンプトを開くに**コマンド プロンプト**し**管理者として実行**)。

このサブコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文

```
wbadmin get versions
[-backupTarget:{<BackupTargetLocation> | <NetworkSharePath>}]
[-machine:BackupMachineName]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-backuptarget|バックアップの詳細を格納するストレージの場所を指定します。 そのターゲットの場所に格納されているバックアップを一覧表示するために使用します。 バックアップ ターゲットの位置には、ローカルに接続されたディスク ドライブ、ボリューム、リモート共有フォルダー、DVD ドライブなどのリムーバブル メディアまたはその他の光メディアを指定できます。 場合**wbadmin のバージョンを取得する**実行は、バックアップが作成された、同じコンピューターでこのパラメーターは必要ありません。 ただし、このパラメーターは、別のコンピューターから作成されたバックアップに関する情報の取得に必須です。|
|-コンピューター|コンピューターのバックアップの詳細を指定します。 複数のコンピューターのバックアップが同じ場所に格納されている場合に使用します。 ときに使用する必要があります **-backuptarget**を指定します。|

## <a name="remarks"></a>注釈

リストの項目は、特定のバックアップからの回復に使用できるを使用して**wbadmin get 項目**します。

## <a name="BKMK_examples"></a>例

H のボリュームに格納されている使用可能なバックアップの一覧を表示するには、次のように入力します。
```
wbadmin get versions -backupTarget:h:
```
リモート共有フォルダーに格納されている使用可能なバックアップの一覧を表示する\\\\型であるコンピューター server01 の servername\share:
```
wbadmin get versions -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get-WBBackupTarget](https://technet.microsoft.com/library/jj902447.aspx) cmdlet