---
title: dfsdiag
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ab5c86ce7ed4760aef4941de55e8dcf8efe48c8f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819143"
---
# <a name="dfsdiag"></a>dfsdiag



`Dfsdiag`コマンドは、DFS 名前空間の診断情報を提供します。

## <a name="syntax"></a>構文

```
dfsdiag [ /TestDCs [/Domain:<Domain name>]| /TestSites </Machine:<server name>| /DFSPath:<namespace root or DFS folder> [/Recurse]> [/Full] | /TestDFSConfig /DFSRoot:<namespace> | /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full] | /TestReferral /DFSPath:<DFS path for getting referrals> [/Full] | /?] 

```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[Dfsdiag TestDCs](dfsdiag-testdcs.md)|ドメイン コント ローラーの構成を確認します。|
|[Dfsdiag TestSites](dfsdiag-testsites.md)|チェックはサイトの関連付けです。|
|[Dfsdiag TestDFSConfig](dfsdiag-testdfsconfig.md)|DFS Namespace 構成を確認します。|
|[Dfsdiag TestDFSIntegrity](dfsdiag-testdfsintegrity.md)|DFS Namespace の整合性を確認します。|
|[Dfsdiag TestReferral](dfsdiag-testreferral.md)|紹介の応答を確認します。|
|/?|コマンド プロンプトにヘルプを表示します。|

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)