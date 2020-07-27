---
title: リモート デスクトップ サービス - Multi-factor Authentication
description: RDS で MFA を使用するための計画に関する情報。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 09ea784e-5644-417a-a3d9-bdbcebc313f9
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: 179feca4870e62f81ed71fabb7b8fd1cb418d391
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86962184"
---
# <a name="remote-desktop-services---multi-factor-authentication"></a>リモート デスクトップ サービス - Multi-factor Authentication

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

Multi-factor Authentication で Active Directory を活用し、ビジネス リソースの高度なセキュリティ保護を適用します。

デスクトップやアプリケーションに接続するエンドユーザーの場合、そのエクスペリエンスは、目的のリソースに接続するために 2 つ目の認証方法を実行するときに既に取り組んでいるものに似ています。
- RDP ファイルから、またはリモート デスクトップ クライアント アプリケーションを介して、デスクトップまたは RemoteApp を起動します
- セキュリティで保護されたリモート アクセスのために RD ゲートウェイに接続すると、SMS またはモバイル アプリケーションによる MFA チャレンジを受けます
- 正しく認証して、そのリソースに接続します。

構成プロセスの詳細については、[ネットワーク ポリシー サーバー (NPS) 拡張機能と Azure AD を使用してリモート デスクトップ ゲートウェイ インフラストラクチャを統合する](/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)ことに関するページを参照してください。
