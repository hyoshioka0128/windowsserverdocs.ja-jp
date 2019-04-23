---
title: QoS ポリシーのアーキテクチャ
description: このトピックでは、グループ ポリシーを使用して、特定のアプリケーションおよび Windows Server 2016 でのサービスのネットワーク トラフィックの帯域幅の優先順位を設定することができるサービスの品質 (QoS) ポリシーの概要を示します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bad37ba3558137b02ae495fe8dd9be2c903cdd97
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843143"
---
# <a name="qos-policy-architecture"></a>QoS ポリシーのアーキテクチャ

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、QoS ポリシーのアーキテクチャについて説明します。

次の図は、ポリシー ベースの QoS のアーキテクチャを示します。

![QoS ポリシーのアーキテクチャ](../../media/QoS/QoS-Policy-Architecture.jpg)

ポリシー ベースの QoS のアーキテクチャは、次のコンポーネントで構成されます。

- **グループ ポリシー クライアント サービス**します。 ユーザーとコンピューターの構成グループ ポリシー設定を管理する Windows サービス。

- **グループ ポリシー エンジン**します。 起動時に、定期的に、Active Directory からユーザーとコンピューターの構成グループ ポリシー設定を取得するグループ ポリシー クライアント サービスのコンポーネントの変更を確認\(既定で 90 分おき\)します。 変更が検出された場合、グループ ポリシー エンジンは、新しいグループ ポリシー設定を取得します。 グループ ポリシー エンジンは、受信の Gpo を処理し、QoS ポリシーが更新されたときに、QoS のクライアント側拡張機能を通知します。

- **QoS のクライアント側の拡張子**します。 QoS ポリシーが変更されたグループ ポリシー エンジンからを示す値を待機し、QoS の検査モジュールに通知するグループ ポリシー クライアント サービスのコンポーネント。

- **TCP/IP スタック**します。 IPv4 と IPv6 の統合サポートが含まれていて、Windows フィルタ リング プラットフォームをサポートしている TCP/IP スタックです。 

- **QoS 検査**します。 QoS のクライアント側拡張機能から QoS ポリシーの変更の兆候が待機する TCP/IP スタック内でモジュール A コンポーネントは、QoS ポリシーの設定を取得し、内部的には、QoS に一致するトラフィックをマークするには、トランスポート層と Pacer.sys 対話ポリシー。

- **NDIS 6.x**します。 ネットワークのカーネル モード ドライバーと Windows Server とクライアント オペレーティング システムのオペレーティング システムの間の標準のインターフェイス。 NDIS 6.x サポート軽量フィルター。 これはパフォーマンスを向上、NDIS 中間ドライバとミニポート ドライバーの簡略化されたドライバー モデルです。

- **QoS ネットワーク プロバイダー インターフェイス\(NPI\)** します。 Pacer.sys と対話するカーネル モード ドライバー用のインターフェイスです。

- **Pacer.sys**します。 ポリシー ベースの QoS と汎用の QoS を使用するアプリケーションのトラフィックにパケットがスケジュール設定を制御する NDIS 6.x ライトウェイト フィルター ドライバー \(GQoS\)とトラフィックの制御\(TC\) Api。 Pacer.sys には、Windows Server 2003 および Windows XP で Psched.sys が置き換えられます。 Pacer.sys は、ネットワーク接続またはアダプターのプロパティから QoS パケット スケジューラ コンポーネントと共にインストールされます。

次のトピックでは、このガイドでは、次を参照してください。 [QoS ポリシー シナリオ](qos-policy-scenarios.md)します。

このガイドの最初のトピックを参照してください。[サービスの品質 (QoS) ポリシー](qos-policy-top.md)します。

