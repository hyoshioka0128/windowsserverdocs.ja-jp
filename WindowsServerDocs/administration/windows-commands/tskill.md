---
title: tskill
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08986e6a-6900-4ece-85a1-8f73b14db1b3 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 697363c91837ff675a14099fd212f4f0753b739b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392337"
---
# <a name="tskill"></a>tskill

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバー上のセッションで実行されているプロセスを終了します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。

## <a name="syntax"></a>構文
```
tskill {<ProcessID> | <ProcessName>} [/server:<ServerName>] [/id:<SessionID> | /a] [/v]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|\<ProcessID >|終了するプロセスの ID を指定します。|
|\<ProcessName >|終了するプロセスの名前を指定します。 このパラメーターには、ワイルドカード文字を含めることができます。|
|/server:\<ServerName >|終了するプロセスを含むターミナルサーバーを指定します。 **/Server**が指定されていない場合は、現在の RD セッションホストサーバーが使用されます。|
|/id:\<SessionID >|指定されたセッションで実行されているプロセスを終了します。|
|/a|すべてのセッションで実行されているプロセスを終了します。|
|/v|実行されているアクションに関する情報を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
- **Tskill**を使用すると、管理者でない限り、自分に属しているプロセスのみを終了できます。 管理者は、すべての**tskill**関数にフルアクセスでき、他のユーザーセッションで実行されているプロセスを終了できます。
- セッションで実行されているすべてのプロセスが終了すると、セッションも終了します。
- *ProcessName*パラメーターと **/server:** <em>ServerName</em>パラメーターを使用する場合は、 **/id:** <em>SessionID</em>または **/a**パラメーターも指定する必要があります。

## <a name="BKMK_examples"></a>例
- プロセス6543を終了するには、次のように入力します。
  ```
  tskill 6543
  ```
- セッション5で実行されている "エクスプローラー" のプロセスを終了するには、次のように入力します。
  ```
  tskill explorer /id:5
  ```
  #### <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文キー](command-line-syntax-key.md)
  [リモート デスクトップ サービスと&#40;です。ターミナル サービスと&#41;です。コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
