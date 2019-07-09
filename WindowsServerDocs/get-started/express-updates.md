---
title: 2018 年 11 月の更新用に再度有効になった Windows Server 2016 の高速更新プログラム
description: Windows Server 2016 の高速更新プログラムに関する情報を提供します
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.openlocfilehash: 1644a61c87953e465895e23c3c8454bae7f3a056
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "66443387"
---
# <a name="express-updates-for-windows-server-2016-re-enabled-for-november-2018-update"></a>2018 年 11 月の更新用に再度有効になった Windows Server 2016 の高速更新プログラム

> Joel Frauenheim
> 
> 適用先:Windows Server 2016

2018 年 11 月 13 日の火曜日の更新から、Windows では Windows Server 2016 の高速更新プログラムを再発行します。 Windows Server 2016 の高速更新プログラムは、更新プログラムが正常にインストールできなくなる重大な問題が見つかった後、2017 年中頃に停止されました。 問題は 2017 年 11 月に修正されましたが、更新チームは、ほとんどのお客様が 2017 年 11 月 14 日の更新プログラム ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) をサーバー環境にインストールして問題の影響を受けないようにするために、高速パッケージの公開に対して保守的なアプローチを採用しました。

WSUS および System Center Configuration Manager (SCCM) のシステム管理者は、2018 年の 11 月に、Windows Server 2016 更新用の 2 つのパッケージ、すなわち完全更新プログラムと高速更新プログラムが再度確認できることに注意する必要があります。 サーバー環境に高速更新プログラムを使用するシステム管理者は、デバイスが 2017 年 11 月 14 日以降の完全更新プログラム ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) を適用して、高速更新プログラムが正しくインストールされるようにする必要があります。 2017 年 11 月 14 日の更新 ([KB 4048953](https://support.microsoft.com/help/4048953/windows-10-update-kb4048953)) 以降更新されていないすべてのデバイスは、高速更新が試行された場合、無限ループに入って帯域幅や CPU リソースを消費する繰り返しエラーが発生します。  この状態を修復するには、システム管理者が高速更新のプッシュを停止し、最新の完全な更新プログラムをプッシュしてエラー ループを停止します。

2018 年 11 月 13 日の高速更新を適用すると、お客様は、管理システムと Windows Server 2016 のエンドポイントの間のパッケージ サイズが直ちに削減されることを確認できます。  