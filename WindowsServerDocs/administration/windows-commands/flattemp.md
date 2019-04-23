---
title: flattemp
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 059a0960-1fd9-4382-87fe-a85d5dccdaea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3fc14a6fe1a355f7c20c130fba3fb1f17e49b6f1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872933"
---
# <a name="flattemp"></a>flattemp

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

有効または、フラットな一時フォルダーを無効にします。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。

## <a name="syntax"></a>構文
```
flattemp {/query | /enable | /disable}
```

## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/query|現在の設定を照会します。|
|/enable|フラットな一時フォルダーを有効にします。 ユーザーのホーム フォルダーに一時フォルダーが存在する場合を除き、ユーザーは、一時フォルダーを共有します。|
|/disable|フラットな一時フォルダーを無効にします。 各ユーザーの一時フォルダーは、(ユーザーのセッション id によって決まります) を別のフォルダーに置かれます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   **Flattemp**コマンドは Windows Server 2008 R2 を実行するコンピューターで Windows Server 2008 または rd セッション ホスト役割サービスを実行するコンピューターにターミナル サーバーの役割サービスをインストールしたときにのみ使用できます。
-   管理資格情報を実行する必要があります**flattemp**します。
-   各ユーザーは、一意の一時フォルダーを使用して**flattemp/enable**フラットな一時フォルダーを有効にします。
-   (通常は、TEMP と TMP 環境変数によって指さ) 複数のユーザーの一時フォルダーを作成するための既定の方法が内のサブフォルダーを作成するには、 **\Temp**フォルダー、サブフォルダー名として、logonID を使用しています。 たとえば、TEMP 環境変数は、C:\Temp をポイントしている場合ユーザー logonID 4 に割り当てられている一時フォルダーは C:\Temp\4 します。 使用して**flattemp**、\Temp フォルダを直接ポイントし、サブフォルダーが形成することを防ぐことができます。 これは、ユーザーの一時フォルダーに、rd セッション ホスト サーバーのローカル ドライブであるかどうか、または共有ネットワーク ドライブ上のホーム フォルダー、格納する場合に便利です。 使用する必要があります、 **flattemp/enable**ユーザーごとに別々 の一時フォルダーがある場合にのみコマンドします。
-   ユーザーの一時フォルダーがネットワーク ドライブにある場合は、アプリケーション エラーが発生する可能性があります。 これには、共有ネットワーク ドライブにネットワークに一時的にアクセスできなくなったときに発生します。 アプリケーションの一時ファイルがアクセスできないか同期であるために、ディスクが停止した場合に応答します。 ネットワーク ドライブに一時フォルダーを移動することは推奨されません。 既定では、ローカルのハード ディスク上の一時フォルダーを保持します。 予期しない動作や特定のアプリケーションでディスク破損エラーが発生した場合、ネットワークを安定化または一時フォルダーをローカル ハード_ディスクに移動します。
-   セッションを使用して別の一時フォルダーごとに、無効にした場合**flattemp**設定は無視されます。 このオプションは、リモート デスクトップ サービスの構成ツールで設定されます。

## <a name="BKMK_examples"></a>例
-   フラットな一時フォルダーの現在の設定を表示するには、次のように入力します。
    ```
    flattemp /query
    ```
-   フラットな一時フォルダーを有効にするには、次のように入力します。
    ```
    flattemp /enable
    ```
-   フラットな一時フォルダーを無効にするには、次のように入力します。
    ```
    flattemp /disable
    ```

## <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)

[リモート デスクトップ サービス&#40;ターミナル サービス&#41;コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
