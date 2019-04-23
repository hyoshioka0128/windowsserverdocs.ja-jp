---
title: デスクトップ ホスティングの参照アーキテクチャ
description: デスクトップ ホスティング RDS と Azure でソリューションを作成するためのアーキテクチャに関するガイダンス。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 11/02/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1bac5dd3-8430-46ee-8bef-10cc4b7cc437
author: lizap
manager: dongill
ms.openlocfilehash: 6f235fd89c34c00601c802f4ea71e440af630169
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890243"
---
# <a name="desktop-hosting-reference-architecture"></a>デスクトップ ホスティングの参照アーキテクチャ

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

Windows デスクトップおよびアプリケーションがホストされている、マルチ テナントを作成するリモート デスクトップ サービス (RDS) と Microsoft Azure virtual machines を使用して、この記事では一連のアーキテクチャ ブロックを定義しますサービスは、"デスクトップ ホスティング"と呼ばれる。 このアーキテクチャの参照を使用すると、高いセキュリティで保護された、拡張性と信頼性の高いデスクトップ ホスティング ソリューションを 5 ~ 5000 のユーザーと小規模および中規模の組織を作成します。    
  
この参照アーキテクチャの主な対象者がいるホスティング プロバイダーを使用して複数のテナントにデスクトップ ホスティング サービスを提供する Microsoft Azure インフラストラクチャ サービスとサブスクライバー アクセス ライセンス (Sal) を活用する、 [Microsoft サービス プロバイダー ライセンス契約](https://www.microsoft.com/hosting/en/us/licensing/splabenefits.aspx)(SPLA) プログラム。 この参照アーキテクチャの 2 つ目の対象ユーザーが作成および管理を使用して、独自の従業員の Microsoft Azure インフラストラクチャ サービスでのデスクトップ ホスティング ソリューションを希望するエンド カスタマー[拡張ソフトウェアを介して権限 RDS ユーザー Cal保証](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf)(SA)。   
  
デスクトップ ホスティング ソリューションのホストを提供するには、パートナーと SA のお客様は、Windows ユーザーのビジネス ユーザーやコンシューマーになじみのあるアプリケーション エクスペリエンスを提供する Windows Server を活用します。 Windows 10 の基盤上に構築された Windows Server 2016 では使い慣れたアプリケーションのサポートとユーザー エクスペリエンスします。    
  
このドキュメントのスコープに制限されています。   
  
* サービスをホストしているデスクトップのアーキテクチャの設計ガイダンスです。 展開手順、パフォーマンス、および容量計画などの詳細情報については、個別のドキュメントに説明します。 Azure インフラストラクチャ サービスの概要については、次を参照してください。 [Microsoft Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/)します。   
  
* セッション ベースのデスクトップ、RemoteApp アプリケーション、および Windows Server 2016 リモート デスクトップ セッション ホスト (RD セッション ホスト) を使用するサーバー ベースの個人用デスクトップ。 Windows クライアント オペレーティング システム用 Service Provider License Agreement (SPLA) がないために、Windows クライアント ベースの仮想デスクトップ インフラストラクチャは説明しません。 Windows Server ベースの仮想デスクトップ インフラストラクチャが、SPLA の下で許可されているし、Windows クライアント ベースの仮想デスクトップ インフラストラクチャは特定のシナリオでのエンド カスタマー ライセンスを持つ専用のハードウェアで許可します。 ただし、クライアント ベースの仮想デスクトップ インフラストラクチャでは、範囲外のこのドキュメントにします。   
  
* Microsoft の製品と機能、主に Windows Server 2016 と Microsoft Azure インフラストラクチャ サービス。   
  
* デスクトップの範囲は 5 からサイズを 5000 人のユーザーをテナントにサービスをホストしています。   大規模なテナントでは、十分なパフォーマンスを提供するには、このアーキテクチャを変更する必要があります。 サーバー マネージャーの RDS のグラフィカル ユーザー インターフェイス (GUI) は使用しないで展開 500 を超えるユーザー。 ユーザーが 500 ~ 5000 の RDS のデプロイを管理するは、PowerShell をお勧めします。   
  
* コンポーネントと、デスクトップ ホスティング サービスに必要なサービスの最小セット。 多くのオプションのコンポーネントと、デスクトップ ホスティング サービスを強化するために追加できるサービスがあるが、これらは、範囲外のこのドキュメントにします。    
  
このドキュメントを読むには、リーダーを理解する必要があります。   
- Microsoft Azure サービスのベースにしたソリューションをホストしている、セキュリティで保護された信頼性の高いマルチ テナントのデスクトップを提供するために必要な構成要素。  
- 各構成要素の目的は、およびそれらの組み合わせ。  
  
このアーキテクチャに基づくソリューションをホストしているデスクトップを構築する複数の方法はあります。 このアーキテクチャでは、統合と azure で Windows Server 2016 の機能強化について説明します。 他のデプロイ オプションは、[デスクトップ ホスティング参照アーキテクチャ ガイド](https://go.microsoft.com/fwlink/p/?LinkId=517389)Windows Server 2012 r2。    
  
次のトピックについて説明します。  
- [デスクトップ ホスティングの論理アーキテクチャ](Desktop-hosting-logical-architecture.md)  
- [RDS の役割を理解します。](Understanding-RDS-roles.md)
- [デスクトップ ホスティング環境を理解します。](Understanding-the-desktop-hosting-environment.md)  
- [Azure サービスとデスクトップをホストするための考慮事項](Azure-services-and-considerations-for-desktop-hosting.md)
  
 


