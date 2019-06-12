---
title: リモート デスクトップ サービスの多要素認証
description: Rds. で MFA を使用するための情報のプランニング
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09ea784e-5644-417a-a3d9-bdbcebc313f9
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: 5ca2a29b0287dbd940afeb4404a85f1d978447f9
ms.sourcegitcommit: d888e35f71801c1935620f38699dda11db7f7aad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66805113"
---
# <a name="remote-desktop-services---multi-factor-authentication"></a>リモート デスクトップ サービスの多要素認証

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

Multi-factor Authentication と Active Directory を活用、ビジネスのリソースの高度なセキュリティ保護を適用します。

デスクトップやアプリケーションに接続するエンドユーザー、エクスペリエンスと既に直面している、目的のリソースに接続する 2 番目の認証メジャーを実行したときと同様です。
- デスクトップまたは RemoteApp の RDP ファイルまたはリモート デスクトップ クライアント アプリケーションを起動します。
- セキュリティで保護されたリモート アクセスの RD ゲートウェイに、接続時に、SMS またはモバイル アプリケーション MFA チャレンジが表示されます。
- 正しく認証し、そのリソースに接続します。

構成のプロセスの詳細については、チェック アウト[ネットワーク ポリシー サーバー (NPS) 拡張機能と Azure AD を使用してリモート デスクトップ ゲートウェイ インフラストラクチャの統合](https://docs.microsoft.com/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)します。
