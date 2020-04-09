---
title: dfsdiag
description: DFS 名前空間の診断情報を提供する dfsdiag の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0891e67-0187-4f18-923d-5623e6127f90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c895dabbbafbe8ea253920d3bc6de17f42918e6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846195"
---
# <a name="dfsdiag"></a>dfsdiag

DFS 名前空間の診断情報を提供します。

## <a name="syntax"></a>構文

```
dfsdiag [ /TestDCs [/Domain:<Domain name>]| /TestSites </Machine:<server name>| /DFSPath:<namespace root or DFS folder> [/Recurse]> [/Full] | /TestDFSConfig /DFSRoot:<namespace> | /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full] | /TestReferral /DFSPath:<DFS path for getting referrals> [/Full] | /?] 

```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[Dfsdiag TestDCs](dfsdiag-testdcs.md)|ドメインコントローラーの構成を確認します。|
|[Dfsdiag TestSites](dfsdiag-testsites.md)|サイトの関連付けを確認します。|
|[Dfsdiag TestDFSConfig](dfsdiag-testdfsconfig.md)|DFS 名前空間の構成を確認します。|
|[Dfsdiag TestDFSIntegrity](dfsdiag-testdfsintegrity.md)|DFS 名前空間の整合性を確認します。|
|[Dfsdiag TestReferral](dfsdiag-testreferral.md)|紹介応答を確認します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)