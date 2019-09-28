---
title: 手順 2 RADIUS サーバーを構成する
description: このトピックは、「Windows Server 2016 で OTP 認証を使用してリモートアクセスを展開する」の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0326818f-9144-496c-b946-f82be4eefbd3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 00ea76d6995f875e509a3bc9ef0bab3d2689c52b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367020"
---
# <a name="step-2-configure-the-radius-server"></a>手順 2 RADIUS サーバーを構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

OTP サポートを使用して DirectAccess をサポートするようにリモートアクセスサーバーを構成する前に、RADIUS サーバーを構成します。  
  
|タスク|説明|  
|----|--------|  
|[2.1。RADIUS ソフトウェアの配布トークンを構成する @ no__t-0|RADIUS サーバーで、ソフトウェアの配布トークンを構成します。|  
|[2.2。RADIUS セキュリティ情報を構成する @ no__t-0|RADIUS サーバーで、使用するポートと共有シークレットを構成します。|  
|[2.3 OTP プローブ用のユーザーアカウントの追加](#BKMK_Probe)|RADIUS サーバーで、OTP プローブ用の新しいユーザーアカウントを作成します。|  
|[2.4 Active Directory との同期](#BKMK_Active)|RADIUS サーバーで、Active Directory アカウントと同期されるユーザーアカウントを作成します。|  
|[2.5 RADIUS 認証エージェントの構成](#BKMK_AuthAgent)|リモートアクセスサーバーを RADIUS 認証エージェントとして構成します。|  
  
## <a name="BKMK_1.1"></a>2.1 RADIUS ソフトウェア配布トークンの構成  
RADIUS サーバーは、OTP で DirectAccess によって使用される、必要なライセンス、ソフトウェア、およびハードウェア配布トークンを使用して構成する必要があります。 このプロセスは、各 RADIUS ベンダーの実装に固有のものです。  
  
## <a name="BKMK_1.2"></a>2.2 RADIUS セキュリティ情報を構成する  
RADIUS サーバーは、通信のために UDP ポートを使用します。各 RADIUS ベンダーには、着信および発信通信用に独自の既定の UDP ポートがあります。 RADIUS サーバーがリモートアクセスサーバーで動作するようにするには、環境内のすべてのファイアウォールが、必要なポートを介して、DirectAccess サーバーと OTP サーバー間の UDP トラフィックを必要に応じて許可するように構成されていることを確認します。  
  
RADIUS サーバーは、認証のために共有シークレットを使用します。 RADIUS サーバーは、共有シークレット用の強力なパスワードを使用して構成します。これは、DirectAccess で directaccess で使用するように DirectAccess サーバーのクライアントコンピューターの構成を構成するときに使用されることに注意してください。  
  
## <a name="BKMK_Probe"></a>2.3 OTP プローブ用のユーザーアカウントの追加  
RADIUS サーバーで、 **DAProbeUser**という名前の新しいユーザーアカウントを作成し、パスワード**daprobepass です**を指定します。  
  
## <a name="BKMK_Active"></a>2.4 Active Directory との同期  
RADIUS サーバーには、OTP で DirectAccess を使用する Active Directory 内のユーザーに対応するユーザーアカウントが必要です。  
  
#### <a name="to-synchronize-the-radius-and-active-directory-users"></a>RADIUS と Active Directory ユーザーを同期するには  
  
1.  OTP ユーザーを使用して、すべての DirectAccess の Active Directory からユーザー情報を記録します。  
  
2.  ベンダー固有の手順を使用して、記録された RADIUS サーバーに同一のユーザー **domain\username**アカウントを作成します。  
  
## <a name="BKMK_AuthAgent"></a>2.5 RADIUS 認証エージェントの構成  
リモートアクセスサーバーは、OTP を実装する DirectAccess の RADIUS 認証エージェントとして構成されている必要があります。 Radius ベンダーの指示に従って、RADIUS 認証エージェントとしてリモートアクセスサーバーを構成します。  
  


