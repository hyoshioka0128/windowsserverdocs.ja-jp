---
title: 手順 2 は、RADIUS サーバーを構成します。
description: このトピックでは、ガイド Windows Server 2016 での OTP 認証を使用したリモート アクセスの展開の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0326818f-9144-496c-b946-f82be4eefbd3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9c111ce52f2cca0cc37ea4d5b873c5fde12bce18
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282446"
---
# <a name="step-2-configure-the-radius-server"></a>手順 2 は、RADIUS サーバーを構成します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

サポートするためにリモート アクセス サーバーを構成する前に、OTP を使用した DirectAccess のサポート、RADIUS サーバーを構成します。  
  
|タスク|説明|  
|----|--------|  
|[2.1.RADIUS のソフトウェア配布のトークンを構成します。](#BKMK_1.1)|RADIUS サーバーでは、ソフトウェア配布のトークンを構成します。|  
|[2.2.RADIUS のセキュリティ情報を構成します。](#BKMK_1.2)|RADIUS サーバーでは、ポートと使用される共有シークレットを構成します。|  
|[2.3 OTP のプローブのユーザー アカウントを追加します。](#BKMK_Probe)|RADIUS サーバーでは、OTP のプローブの新しいユーザー アカウントを作成します。|  
|[2.4 は、Active Directory と同期します。](#BKMK_Active)|RADIUS サーバーでは、Active Directory アカウントと同期されているユーザー アカウントを作成します。|  
|[2.5 は、RADIUS 認証エージェントを構成します。](#BKMK_AuthAgent)|RADIUS 認証エージェントとリモート アクセス サーバーを構成します。|  
  
## <a name="BKMK_1.1"></a>2.1 RADIUS のソフトウェア配布のトークンを構成します。  
RADIUS サーバーは、必要なライセンスと OTP での DirectAccess で使用されるソフトウェアやハードウェアの配布のトークンで構成する必要があります。 このプロセスは、各 RADIUS ベンダーの実装に固有になります。  
  
## <a name="BKMK_1.2"></a>2.2 RADIUS のセキュリティ情報を構成します。  
RADIUS サーバーの通信のために、UDP ポートを使用して、各 RADIUS ベンダーが独自の着信および発信の通信の既定の UDP ポート。 リモート アクセス サーバーと連携する RADIUS サーバーの場合に、必要に応じて、必要なポート経由でサーバーの DirectAccess と OTP サーバー間の UDP トラフィックを許可する、環境内のすべてのファイアウォールが構成されていることを確認します。  
  
RADIUS サーバーは、認証のために、共有シークレットを使用します。 RADIUS サーバーの共有シークレット、強力なパスワードを構成し、これが使用されることを DirectAccess OTP と使用するため、DirectAccess サーバーのクライアント コンピューターの構成を構成する際に注意してください。  
  
## <a name="BKMK_Probe"></a>2.3 OTP のプローブのユーザー アカウントを追加します。  
RADIUS サーバーと呼ばれる新しいユーザー アカウントを作成します。 **DAProbeUser**し、パスワードを付けます**daprobepass です**します。  
  
## <a name="BKMK_Active"></a>2.4 は、Active Directory と同期します。  
RADIUS サーバーで OTP を DirectAccess を使用する Active Directory ユーザーに対応するユーザー アカウントが必要です。  
  
#### <a name="to-synchronize-the-radius-and-active-directory-users"></a>RADIUS および Active Directory ユーザーを同期するには  
  
1.  Active Directory からユーザーの情報をすべての DirectAccess の OTP ユーザーを記録します。  
  
2.  ベンダー固有の手順を使用して、同一のユーザーを作成する**domain \username** RADIUS サーバーで記録されているアカウント。  
  
## <a name="BKMK_AuthAgent"></a>2.5 は、RADIUS 認証エージェントを構成します。  
リモート アクセス サーバーは、OTP の実装を含む DirectAccess 用の RADIUS 認証エージェントとして構成する必要があります。 RADIUS 認証エージェントとリモート アクセス サーバーを構成する RADIUS ベンダーの指示に従います。  
  


