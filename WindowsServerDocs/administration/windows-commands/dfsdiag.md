---
title: dfsdiag
description: DFS 名前空間の診断情報を提供する dfsdiag のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d5a9b147994628ccad6a723311decbccbe82ec6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719551"
---
# <a name="dfsdiag"></a>dfsdiag

DFS 名前空間の診断情報を提供します。

## <a name="syntax"></a>構文

```
dfsdiag [ /TestDCs [/Domain:<Domain name>]| /TestSites </Machine:<server name>| /DFSPath:<namespace root or DFS folder> [/Recurse]> [/Full] | /TestDFSConfig /DFSRoot:<namespace> | /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full] | /TestReferral /DFSPath:<DFS path for getting referrals> [/Full] | /?] 

```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|[Dfsdiag TestDCs](dfsdiag-testdcs.md)|ドメインコントローラーの構成を確認します。|
|[Dfsdiag TestSites](dfsdiag-testsites.md)|サイトの関連付けを確認します。|
|[Dfsdiag TestDFSConfig](dfsdiag-testdfsconfig.md)|DFS 名前空間の構成を確認します。|
|[Dfsdiag TestDFSIntegrity](dfsdiag-testdfsintegrity.md)|DFS 名前空間の整合性を確認します。|
|[Dfsdiag TestReferral](dfsdiag-testreferral.md)|紹介応答を確認します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)