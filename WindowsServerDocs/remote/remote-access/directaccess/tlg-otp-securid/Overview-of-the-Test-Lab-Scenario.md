---
title: テスト ラボのシナリオの概要
description: このトピックでは、OTP 認証と Windows Server 2016 で RSA SecurID を使用した DirectAccess のデモンストレーションのテスト ラボ ガイドの一部
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce584811-b209-48fe-ab2b-4c399bd0bd79
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 944a38438d81bfffcff002336a5eb0427ab9e5ea
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283153"
---
# <a name="overview-of-the-test-lab-scenario"></a>テスト ラボのシナリオの概要

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

リモート アクセス サーバーの役割では、Windows Server 2016 とは、リモート ユーザーの内部に安全にアクセスできるようにする Windows Server 2012 R2 および Windows Server 2012 のオペレーティング システムが DirectAccess を使用してリソースをネットワークまたは仮想プライベート ネットワーク (Vpn) を使用しますルーティングとリモート アクセスのサービス (RRAS)。 このガイドには拡張するための手順が含まれています、[テスト ラボ ガイド。IPv4 と IPv6 混在での DirectAccess 単一サーバー セットアップのデモンストレーション](https://go.microsoft.com/fwlink/p/?LinkId=237004)をリモート アクセスのワンタイム パスワード (OTP) 構成を示します。  
  
> [!WARNING]  
> このテスト ラボ ガイドの設計には、インフラストラクチャ サーバー、ドメイン コント ローラーと Windows Server 2016、Windows Server 2012 R2 または Windows Server 2012 のいずれかを実行している証明機関 (CA) などが含まれています。 このテスト ラボ ガイドを使用して、他のオペレーティング システムを実行しているインフラストラクチャ サーバーを構成するがテストされていない、および他のオペレーティング システムを構成する手順については、このガイドには含まれません。  
  
## <a name="about-this-guide"></a>このガイドについて  
Windows Server 2016、Windows Server 2012 R2 および Windows Server 2012 でのリモート アクセスは、otp クライアント認証のサポートを追加します。 このテスト ラボの目的では、RSA SecurID のみを使用してをリモート アクセス権を持つ OTP の機能を示します。 その他の RADIUS ベースの OTP ソリューションは、同様に、サポートされますが、このテスト ラボの範囲外です。 このガイドでは、6 台のサーバーと 2 台のクライアント コンピューターを使うリモート アクセスを構成し、デモンストレーションを行う手順について説明します。 OTP のテスト ラボを完成したリモート アクセスは、イントラネット、インターネットと、ホーム ネットワークをシミュレートし、さまざまなインターネット接続のシナリオでのリモート アクセス機能を紹介します。  
  
> [!IMPORTANT]  
> このラボは、最小限のコンピューターを使って概念を実証するためのものです。 このガイドで詳しく説明されている構成は、テスト ラボでの使用のみを目的としています。運用環境では使用しないでください。  
  


