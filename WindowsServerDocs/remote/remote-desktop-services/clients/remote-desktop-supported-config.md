---
title: リモート デスクトップ クライアントでサポートされる構成
description: リモート デスクトップ クライアントを使用してアクセスできる PC について説明します
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
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "63748964"
---
# <a name="remote-desktop-client---supported-configuration"></a>リモート デスクトップ クライアントでサポートされる構成

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
- Windows Multipoint Server 2011
- Windows Multipoint Server 2012
- Windows Small Business Server 2008
- Windows Small Business Server 2011

次のコンピューターには、リモート デスクトップ ゲートウェイを実行できます。

- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Small Business Server 2011

次のオペレーティング システムは、RD Web アクセスまたは RemoteApp のサーバーとして使用できます。
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

## <a name="unsupported-windows-versions-and-editions"></a>サポートされていない Windows のバージョンとエディション

リモート デスクトップ クライアントは、これらの Windows のバージョンとエディションには接続できません。

- Windows 7 Starter
- Windows 7 ホーム
- Windows 8 Home
- Windows 8.1 Home
- Windows 10 Home

インストールされている Windows のバージョンの 1 つを持つコンピューターにアクセスする場合は、RDP をサポートする Windows バージョンにアップグレードをお勧めします。

## <a name="rd-gateway-messaging-is-not-supported"></a>RD ゲートウェイ メッセージングがサポートされていません
リモート デスクトップ クライアントは RD ゲートウェイのメッセージングをサポートしていません。 リモート デスクトップ リソースのアクセス ポリシー (RD RAP)、RD ゲートウェイ サーバーを指定しないことを確認 **RD ゲートウェイのメッセージングをサポートしているコンピューターのみを許可** と接続することはできません。