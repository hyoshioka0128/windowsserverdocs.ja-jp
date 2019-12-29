---
title: テストラボガイド-OTP 認証と RSA SecurID を使用した DirectAccess のデモンストレーション
description: このトピックは、「テストラボガイド-OTP 認証を使用した DirectAccess のデモンストレーション」と「RSA SecurID for Windows Server 2016」に含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10c7a49c-5671-4bec-b562-13fdd67f4629
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f226c4c4b8a7517458ede95b4e237b567e0c49df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404665"
---
# <a name="test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid"></a>テスト ラボ ガイド: OTP 認証と RSA SecurID を使用した DirectAccess のデモンストレーション

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

リモートアクセスは、windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 オペレーティングシステムのサーバーの役割であり、リモートユーザーがルーティングを使用して、DirectAccess または仮想プライベートネットワーク (Vpn) を使用して内部ネットワークリソースに安全にアクセスできるようにします。およびリモートアクセスサービス (RRAS)。 このガイドでは、「リモートアクセスのワンタイムパスワード (OTP) 構成をデモンストレーションするための、 [IPv4 と IPv6 の混在を使用した DirectAccess シングルサーバーセットアップのデモンストレーション」の「テストラボガイド」](https://go.microsoft.com/fwlink/p/?LinkId=237004)を拡張する手順について説明します。  
  
> [!WARNING]  
> このテストラボガイドの設計には、Windows Server 2012 R2 または Windows Server 2012 を実行しているドメインコントローラー、証明機関 (CA) などのインフラストラクチャサーバーが含まれています。 このテストラボガイドを使用して、他のオペレーティングシステムを実行しているインフラストラクチャサーバーを構成することはできません。また、他のオペレーティングシステムを構成する手順については、このガイドでは説明しません。  
  
## <a name="about-this-guide"></a>このガイドについて  
Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 のリモートアクセスでは、OTP を使用したクライアント認証のサポートが追加されます。 このテストラボでは、リモートアクセスを使用した OTP 機能を示すために RSA SecurID のみを使用します。 その他の RADIUS ベースの OTP ソリューションもサポートされていますが、このテストラボの範囲外です。 このガイドでは、6 台のサーバーと 2 台のクライアント コンピューターを使うリモート アクセスを構成し、デモンストレーションを行う手順について説明します。 「OTP を使用したリモートアクセスの完了」テストラボでは、イントラネット、インターネット、ホームネットワークをシミュレートし、さまざまなインターネット接続シナリオでリモートアクセス機能を示します。  
  
> [!IMPORTANT]  
> このラボは、最小限のコンピューターを使って概念を実証するためのものです。 このガイドで詳しく説明されている構成は、テスト ラボでの使用のみを目的としています。運用環境では使用しないでください。  
  


