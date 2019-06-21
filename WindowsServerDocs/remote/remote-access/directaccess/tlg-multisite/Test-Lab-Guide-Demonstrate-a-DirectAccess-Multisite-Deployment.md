---
title: 'テスト ラボ ガイド: DirectAccess マルチサイト展開のデモンストレーション'
description: このトピックは一部のテスト ラボ ガイド-DirectAccess マルチサイト展開の Windows Server 2016 のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c98106c-67cc-406a-810e-f2e09f7e2c5e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 87c1f629d96d247d273d48066797795b9fe724e6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281380"
---
# <a name="test-lab-guide-demonstrate-a-directaccess-multisite-deployment"></a>テスト ラボ ガイド:DirectAccess のマルチサイト展開をデモンストレーションします。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

リモート アクセスは、リモート ユーザーが DirectAccess または RRAS VPN を使用して内部ネットワーク リソースに安全にアクセスできるようにする、Windows Server 2016、Windows Server 2012 R2 および Windows Server 2012 オペレーティング システムでサーバーの役割です。 このガイドには拡張するための手順が含まれています、[テスト ラボ ガイド。IPv4 と IPv6 混在での DirectAccess 単一サーバー セットアップのデモンストレーション](https://go.microsoft.com/fwlink/p/?LinkId=237004)マルチサイトのシナリオでリモート アクセスを示します。  
  
マルチサイトのシナリオでリモート アクセスを展開するには、地理的に多様な場所でのリモート アクセス サーバーを構成することができます。 以前は、リモート ユーザーが常に特定の DirectAccess サーバー経由で企業ネットワークに接続する必要があります。 Windows Server 2016、Windows Server 2012 R2 または Windows Server 2012 と Windows 10 または Windows 8、使用には、展開に地理的な場所ごとのエントリ ポイントを構成できます。 各エントリ ポイントは、単一のリモート アクセス サーバーまたはリモート アクセス サーバーのクラスターを指定できます。 リモート ユーザーには、組織のリモート アクセスのエントリ ポイントのいずれかに接続するオプションがあります。 たとえば、リモート ユーザーは、通常、アジアにあるリモート アクセスのエントリ ポイントに接続し、出張がヨーロッパに場合は、クライアント コンピューターは自動的に最も近いリモート アクセスのエントリ ポイントに接続します。  
  
## <a name="about-this-guide"></a>このガイドについて  
このガイドには、構成および 9 つのサーバーと 3 つのクライアント コンピューターを使用してリモート アクセスのデモを行うのための手順が含まれています。 完了したリモート アクセスのマルチサイトのテスト ラボでは、イントラネット、インターネットやホーム ネットワークをシミュレートし、さまざまなインターネット接続のシナリオでのリモート アクセス機能を紹介します。  
  
> [!IMPORTANT]  
> このラボは、最小限のコンピューターを使って概念を実証するためのものです。 このガイドで詳しく説明されている構成は、テスト ラボでの使用のみを目的としています。運用環境では使用しないでください。  
  


