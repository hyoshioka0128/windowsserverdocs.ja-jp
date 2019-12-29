---
title: dfsdiag
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 61a6ab9a90e4d0220cfe27d2d21120be19b9ff1f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378311"
---
# <a name="dfsdiag"></a>dfsdiag



@No__t-0 コマンドは、DFS 名前空間の診断情報を提供します。

## <a name="syntax"></a>構文

```
dfsdiag [ /TestDCs [/Domain:<Domain name>]| /TestSites </Machine:<server name>| /DFSPath:<namespace root or DFS folder> [/Recurse]> [/Full] | /TestDFSConfig /DFSRoot:<namespace> | /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full] | /TestReferral /DFSPath:<DFS path for getting referrals> [/Full] | /?] 

```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[Dfsdiag TestDCs](dfsdiag-testdcs.md)|ドメインコントローラーの構成を確認します。|
|[Dfsdiag TestSites](dfsdiag-testsites.md)|サイトの関連付けを確認します。|
|[Dfsdiag TestDFSConfig](dfsdiag-testdfsconfig.md)|DFS 名前空間の構成を確認します。|
|[Dfsdiag TestDFSIntegrity](dfsdiag-testdfsintegrity.md)|DFS 名前空間の整合性を確認します。|
|[Dfsdiag TestReferral](dfsdiag-testreferral.md)|紹介応答を確認します。|
|/?|コマンド プロンプトにヘルプを表示します。|

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)