---
title: QoS ポリシーのアーキテクチャ
description: このトピックでは、グループ ポリシーを使用して、特定のアプリケーションと Windows Server 2016 でのサービスのネットワーク トラフィックの帯域幅の優先順位を設定することができるサービスの品質 (QoS) ポリシーの概要を示します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 00d36604c57add6bf9f45b0166b08c1fb15be467
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="qos-policy-architecture"></a>QoS ポリシーのアーキテクチャ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、QoS ポリシーのアーキテクチャについて説明します。

次の図は、ポリシー ベースの QoS のアーキテクチャを示します。

![QoS ポリシーのアーキテクチャ](../../media/QoS/QoS-Policy-Architecture.jpg)

ポリシー ベースの QoS のアーキテクチャは、次のコンポーネントで構成されます。

- **グループ ポリシー クライアント サービス**します。 ユーザーとコンピューターの構成のグループ ポリシー設定を管理する Windows サービス。

- **グループ ポリシー エンジン**します。 スタートアップ時に、定期的に、Active Directory からユーザーとコンピューターの構成のグループ ポリシー設定を取得しているグループ ポリシー クライアント サービスのコンポーネントによって変更が確認 \ (既定ではすべて 90 minutes\)。 変更が検出された場合、グループ ポリシー エンジンは、新しいグループ ポリシー設定を取得します。 グループ ポリシー エンジンは、入力方向の Gpo を処理し、QoS ポリシーを更新する場合に、QoS のクライアント側拡張機能を通知します。

- **QoS のクライアント側拡張機能**します。 QoS ポリシーが変更されているグループ ポリシー エンジンから示してするまで待機し、QoS 検査モジュールに通知しているグループ ポリシー クライアント サービスのコンポーネントです。

- **TCP/IP スタック**します。 TCP/IP スタックを IPv4 および IPv6 の統合のサポートが含まれており、Windows フィルタ リング プラットフォームをサポートしています。 

- **QoS 検査**します。 QoS クライアント側拡張機能から QoS ポリシーの変更の兆候を待機する TCP/IP スタック内のモジュール A コンポーネントは、QoS ポリシーの設定を取得しは内部で QoS ポリシーに一致するトラフィックをマークするには、トランスポート層と Pacer.sys と対話します。

- **NDIS 6.x**します。 ネットワークのカーネル モード ドライバーと Windows Server とクライアント オペレーティング システムのオペレーティング システムの間での標準インターフェイス。 NDIS 6.x サポート軽量フィルター、パフォーマンスを向上 NDIS 中間ドライバとミニポート ドライバーの簡略化されたドライバー モデルであります。

- **QoS ネットワーク プロバイダー インターフェイス \(NPI\)**します。 カーネル モード ドライバー Pacer.sys と対話するためのインターフェイス。

- **Pacer.sys**します。 ポリシー ベースの QoS と汎用的な QoS \(GQoS\) とトラフィックの制御 \(TC\) API を使用するアプリケーションのトラフィックにパケットのスケジュール設定によって制御される NDIS 6.x 軽量フィルター ドライバーです。 Pacer.sys には、Windows Server 2003 および Windows XP で Psched.sys が置き換えられます。 Pacer.sys には、ネットワーク接続またはアダプターのプロパティから、QoS パケット スケジューラ コンポーネントがインストールされます。

このガイドの次のトピックを参照してください。[QoS ポリシーのシナリオ](qos-policy-scenarios.md)します。

このガイドで最初のトピックを参照してください。[サービスの品質 (QoS) ポリシー](qos-policy-top.md)します。

