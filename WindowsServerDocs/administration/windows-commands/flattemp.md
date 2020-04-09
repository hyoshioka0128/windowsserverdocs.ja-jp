---
title: flattemp
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 059a0960-1fd9-4382-87fe-a85d5dccdaea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a291c102d70ff9166a7bb0261e506792a49dc18
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844575"
---
# <a name="flattemp"></a>flattemp

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

有効または、フラットな一時フォルダーを無効にします。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

> [!NOTE]
> Windows Server 2008 R2 では、ターミナル サービスはリモート デスクトップ サービスという名前に変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

## <a name="syntax"></a>構文
```
flattemp {/query | /enable | /disable}
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/query|現在の設定に対してクエリを行います。|
|/enable|フラット一時フォルダーを有効にします。 一時フォルダーがユーザーのホームフォルダーに存在しない限り、ユーザーは一時フォルダーを共有します。|
|/disable|フラット一時フォルダーを無効にします。 各ユーザーの一時フォルダーは、(ユーザーのセッション ID によって決定される) 別のフォルダーに格納されます。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント
-   **Flattemp**コマンドを使用できるのは、windows server 2008 を実行しているコンピューターにターミナルサーバーの役割サービスがインストールされている場合、または windows Server 2008 R2 を実行しているコンピューターに Rd セッションホストの役割サービスがインストールされている場合のみです。
-   **Flattemp**を実行するには、管理者の資格情報が必要です。
-   各ユーザーが一意の一時フォルダーを持つようになったら、 **flattemp/enable**を使用してフラット一時フォルダーを有効にします。
-   複数のユーザー用の一時フォルダー (通常、TEMP および TMP 環境変数が指す) を作成する既定の方法は、logonID をサブフォルダー名として使用することによって、 **\temp**フォルダーにサブフォルダーを作成することです。 たとえば、TEMP 環境変数が C:\Temp を指している場合、ユーザー logonID 4 に割り当てられた一時フォルダーは C:\Temp\4. になります。 **Flattemp**を使用すると、\temp フォルダーを直接参照して、サブフォルダーが形成されないようにすることができます。 これは、rd セッションホストサーバーのローカルドライブ上にあるか、共有ネットワークドライブ上にあるかにかかわらず、ユーザーの一時フォルダーがホームフォルダーに含まれるようにする場合に便利です。 各ユーザーに個別の一時フォルダーがある場合にのみ、 **flattemp/enable**コマンドを使用してください。
-   ユーザーの一時フォルダーがネットワークドライブ上にある場合、アプリケーションエラーが発生することがあります。 このエラーは、ネットワーク上で共有ネットワークドライブが一時的にアクセスできなくなった場合に発生します。 アプリケーションの一時ファイルは、アクセスできないか、同期されていないため、ディスクが停止しているかのように応答します。 一時フォルダーをネットワークドライブに移動することはお勧めしません。 既定では、一時フォルダーはローカルハードディスクに保持されます。 特定のアプリケーションで予期しない動作やディスク破損エラーが発生した場合は、ネットワークを安定させるか、一時フォルダーをローカルハードディスクに移動します。
-   セッションごとに個別の一時フォルダーを使用することを無効にした場合、 **flattemp**設定は無視されます。 このオプションは、リモートデスクトップサービス構成ツールで設定します。

## <a name="examples"></a><a name=BKMK_examples></a>例
-   フラット一時フォルダーの現在の設定を表示するには、次のように入力します。
    ```
    flattemp /query
    ```
-   フラット一時フォルダーを有効にするには、次のように入力します。
    ```
    flattemp /enable
    ```
-   フラット一時フォルダーを無効にするには、次のように入力します。
    ```
    flattemp /disable
    ```

## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)

[リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
