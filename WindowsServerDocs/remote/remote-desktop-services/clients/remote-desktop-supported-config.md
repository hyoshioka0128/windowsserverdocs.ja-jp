---
title: リモート デスクトップ クライアントでサポートされている構成
description: リモート デスクトップ クライアントを使用してアクセスできる Pc を学習します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb932dad-6f74-484f-8f7b-dd957b615d44
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d38008b6387385917ad21ce7e169b8ff3f4d18ba
ms.sourcegitcommit: 96e968bbe8dc50ebb1535ae1c8ce92fa73c83171
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2018
ms.locfileid: "1978049"
---
# <a name="remote-desktop-client---supported-configuration"></a>リモート デスクトップ クライアントでサポートされている構成

## <a name="supported-pcs"></a>サポートされる PC
次の Windows オペレーティング システムを実行している Pc に接続することができます。
- Windows 10 Pro
- Windows 10 Enterprise
- Windows 8 Enterprise
- Windows 8 Professional
- Windows 7 Professional
- Windows 7 Enterprise
- Windows 7 Ultimate
- Windows 7 Ultimate
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows マルチポイント Server 2011
- Windows マルチポイント Server 2012
- Windows Small Business Server 2008
- Windows Small Business Server 2011

次のコンピューターには、リモート デスクトップ ゲートウェイを実行できます。

- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Small Business Server 2011

次のオペレーティング システムが、RD Web アクセスまたは RemoteApp サーバーとして使用できます。
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

## <a name="unsupported-windows-versions-and-editions"></a>サポートされていない Windows のバージョンとエディション

リモート デスクトップ クライアントはこれらの Windows のバージョンとエディションへの接続できません。

- Windows 7 Starter
- Windows 7 のホーム
- Windows 8 Home
- Windows 8.1 ホーム
- Windows 10 Home

Windows のバージョンがインストールされている次のいずれかであるコンピューターにアクセスする場合は、RDP をサポートしている Windows のバージョンにアップグレードすることをお勧めします。

## <a name="rd-gateway-messaging-is-not-supported"></a>RD ゲートウェイ メッセージングはサポートされていません
リモート デスクトップ クライアントは RD ゲートウェイ メッセージングをサポートしていません。 リモート デスクトップ リソースのアクセス ポリシー (RD 社) RD ゲートウェイ サーバーで**RD ゲートウェイ メッセージングのサポートを持つコンピューターのみを許可する**が指定されていない接続することはできないことを確認します。