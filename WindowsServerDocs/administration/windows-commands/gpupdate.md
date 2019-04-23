---
title: gpupdate
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fd4e567-2ce1-4637-b611-c2f0895e5708
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 61131d2bf253c66d93408bc66b78d1dca2502087
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840593"
---
# <a name="gpupdate"></a>gpupdate



グループ ポリシー設定を更新します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
gpupdate [/target:{Computer | User}] [/force] [/wait:<VALUE>] [/logoff] [/boot] [/sync] [/?]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/target: {コンピューター | ユーザー}|ユーザーまたはコンピューターのポリシー設定のみのみを更新します。|
|/force|すべてのポリシー設定を再適用されます。 既定では、変更されたポリシー設定のみが適用されます。|
|/wait:\<VALUE>|ポリシーの処理、コマンド プロンプトに戻る前に完了するまで待機する秒数を設定します。 時間制限を超えたときに、コマンド プロンプトが表示されたらは、ポリシーの処理が続行されます。 既定値は、600 秒です。 値**0**待機しないことを意味します。 値 **-1**無制限に待機することを意味します。</br>スクリプトでは、このコマンドを指定すると、制限時間を使用して行うことができます**gpupdate**の完了時に依存しないコマンドを続行**gpupdate**します。 指定された時間制限なしでこのコマンドを使用する代わりに、 **gpupdate**それに依存するその他のコマンドを実行する前に実行が終了します。|
|/logoff|グループ ポリシー設定を更新した後は、ログオフをによりします。 バック グラウンドの更新サイクルでポリシーを処理しないが、ユーザーがログオンしたときにポリシーの処理はグループ ポリシー クライアント側拡張機能のために必要です。 例には、ユーザーを対象としたソフトウェアのインストールとフォルダー リダイレクトが含まれます。 拡張機能の呼び出しには、ログオフが必要な場合は、このオプションを指定しても効果はありません。|
|/boot|グループ ポリシー設定が適用された後は、コンピューターの再起動をによりします。 バック グラウンドの更新サイクルでポリシーを処理しないが、コンピューターの起動時にポリシーの処理はグループ ポリシー クライアント側拡張機能のために必要です。 例には、コンピューターを対象としたソフトウェアのインストールが含まれます。 拡張機能の呼び出しには、再起動が必要な場合は、このオプションを指定しても効果はありません。|
|/sync|同期的に実行する次のフォア グラウンド ポリシー アプリケーション。 フォア グラウンドのポリシーは、コンピューターのブートとユーザーのログオン時に適用されます。 これを指定するにはユーザー、コンピューター、またはその両方を使用して、 **/target**パラメーター。 **/Force**と **/wait**したり、指定した場合、パラメーターは無視されます。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>注釈

-   **Gpupdate**コマンドは Windows Server 2008 R2、Windows Server 2008、Windows 7 Ultimate、Windows 7 Professional、Windows Vista Ultimate、Windows Vista Enterprise、および Windows Vista Business で使用できます。

## <a name="BKMK_Examples"></a>例

変更されたかどうかに関係なく、すべてのグループ ポリシー設定のバック グラウンドの更新を強制します。
```
gpupdate /force
```

#### <a name="additional-references"></a>その他の参照情報

-   [グループ ポリシーの TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   [コマンドライン構文キー](command-line-syntax-key.md)