---
title: 仮想マシンが、ゲストオペレーティングシステムでサポートされている場合にのみ sr-iov を使用するように構成する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 33cf5b68-e43e-47ef-adbc-6b266c1d4dce
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 1939aa6e866eddcf5ac99a784332b65cd594ceb8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935510"
---
# <a name="configure-virtual-machines-to-use-sr-iov-only-when-supported-by-the-guest-operating-system"></a>仮想マシンが、ゲストオペレーティングシステムでサポートされている場合にのみ sr-iov を使用するように構成する

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題
*1つ以上の仮想マシンがシングルルート i/o 仮想化 (SR-IOV) を使用するように構成されていますが、ゲストオペレーティングシステムが sr-iov をサポートしていません*

## <a name="impact"></a>影響
*Sr-iov 仮想機能は、次の仮想マシンには割り当てられません。*

\<list of virtual machines>

## <a name="resolution"></a>解決方法
*Sr-iov をサポートしていないゲストオペレーティングシステムを実行しているすべての仮想マシンで sr-iov を無効にします。*

Sr-iov は、一部の64ビット Windows ゲストでのみサポートされています。 詳細については、「 [hyper-v の機能と世代とゲストの互換性](../Hyper-V-feature-compatibility-by-generation-and-guest.md)」を参照してください。



