---
title: bootcfg
description: ファイル設定 Boot.ini 構成、クエリ、または変更を行う、bootcfg コマンドのリファレンス記事です。
ms.topic: article
ms.assetid: 3deb354c-5717-4066-bc79-b9323d559e44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: edab8bc0b4e63544282e53f0a7b6e1fc255a4be7
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880528"
---
# <a name="bootcfg"></a>bootcfg

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Boot.ini ファイルの設定の構成、クエリ、または変更を行います。

## <a name="syntax"></a>構文

```
bootcfg <parameter> [arguments...]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| [bootcfg addsw](bootcfg-addsw.md) | 指定したオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを追加します。 |
| [bootcfg copy](bootcfg-copy.md) | 既存のブートエントリのコピーを作成します。これには、コマンドラインオプションを追加できます。 |
| [bootcfg dbg1394](bootcfg-dbg1394.md) | 指定されたオペレーティングシステムエントリに対して1394ポートデバッグを構成します。 |
| [bootcfg debug](bootcfg-debug.md) | 指定したオペレーティングシステムエントリのデバッグ設定を追加または変更します。 |
| [bootcfg default](bootcfg-default.md) | 既定値として指定するオペレーティングシステムエントリを指定します。 |
| [bootcfg delete](bootcfg-delete.md) | Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリを削除します。 |
| [bootcfg ems](bootcfg-ems.md) | ユーザーが、緊急管理サービスコンソールをリモートコンピューターにリダイレクトするための設定を追加または変更できるようにします。 |
| [bootcfg query](bootcfg-query.md) | Boot.ini の [ブートローダー] セクションと [オペレーティングシステム] セクションのエントリを照会して表示します。 |
| [bootcfg raw](bootcfg-raw.md) | 文字列として指定されたオペレーティングシステムの読み込みオプションを、Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリに追加します。 |
| [bootcfg rmsw](bootcfg-rmsw.md) | 指定したオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを削除します。 |
| [bootcfg timeout](bootcfg-timeout.md) | オペレーティングシステムのタイムアウト値を変更します。 |
