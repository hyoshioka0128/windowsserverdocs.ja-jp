---
ms.assetid: e22d84a5-113d-4bec-b484-036ed29f0c28
title: Join to Workplace from 任意のデバイス用の SSO とシームレスな 2 要素認証を企業アプリケーション間で
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 12/05/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4926eb32a0bbffb092ec02ca2508fe97d52d1466
ms.sourcegitcommit: 46439194e5deb0fa5f338b428f95dd6b5b799337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2018
---
# <a name="join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications"></a>Join to Workplace from 任意のデバイス用の SSO とシームレスな 2 要素認証を企業アプリケーション間で

>Windows Server 2012 R2 の適用対象:

コンシューマー向けデバイスと場所を問わず情報へのアクセスの数の急激な増加がユーザーが自分のテクノロジを認識する方法を変更します。 定数については、簡単にアクセスすると共に、1 日をとおして情報テクノロジの使用には、仕事と生活ホーム間の従来の境界は、ぼかし効果です。 この境界のような変化が伴ってテクノロジ選択され、ユーザーのパーソナリティ、アクティビティ、およびスケジュールに合わせてカスタマイズされたそのパーソナル-職場にまで拡張する必要があります。 対応するため、要求が高まって個人用のコンシューマー デバイスを企業ネットワークに接続する、次の価値提案導入しています。

-   管理者は、アプリケーション、ユーザー、デバイス、および場所に基づいて、会社のリソースへのアクセスを持つユーザーを制御できます。

-   従業員は、デバイスを問わずにアプリケーションやデータ、あらゆる場所にアクセスできます。 従業員は、ブラウザー アプリケーションや企業アプリケーションでシングル サインオンを使用できます。

## <a name="key-concepts-introduced-in-the-solution"></a>ソリューションで導入された主要な概念

### <a name="workplace-join"></a>ワークプ レース ジョイン
ワークプ レース ジョインを使用すると、インフォメーション ワーカーは個人用のデバイスを会社のリソースとサービスにアクセスする、会社の職場のコンピューターを参加できます。 個人用のデバイスを職場に参加するときに既知のデバイスなり提供シームレスな 2 要素認証とシングル サインオン職場のリソースとアプリケーションにします。 デバイスがワークプ レース ジョインによって参加しているときに、アプリケーションに対するセキュリティ トークンの発行を承認するために条件付きアクセスをドライブに、デバイスの属性をディレクトリから取得できます。 Windows 8.1 と iOS 6.0 以降、および Android 4.0 以降のデバイスをワークプ レース ジョインを使用して参加することができます。

### <a name="BKMK_DRS"></a>Azure Active Directory Device Registration サービス
ワークプ レース ジョイン、Azure Active Directory Device Registration サービスによってが可能になります。 デバイスをワークプ レース ジョインによって参加、サービスは Azure Active Directory にデバイス オブジェクトをプロビジョニングし、デバイス ID を表すために使用する、ローカル デバイス上のキーを設定します。 このデバイス ID は、クラウドとオンプレミスでホストされているアプリケーションのアクセス制御規則と共に使用できます。

詳細については、Azure Active Directory Device registration サービスを有効にすると、次を参照してください。[Azure Active Directory デバイス登録サービスの概要](https://msdn.microsoft.com/6a14cb1f-a058-4453-8ede-d9f4a66a7073.aspx)します。

### <a name="workplace-join-as-a-seamless-second-factor-authentication"></a>ワークプ レース ジョインとしてシームレスな 2 要素認証
企業は、情報へのアクセス ガバナンスとコンシューマーの企業リソースにデバイスのアクセス権を付与しながら、コンプライアンスに関連するリスクを管理できます。 デバイスでワークプ レース ジョインは、管理者に、次の機能を提供します。

-   既知のデバイスを識別する、デバイス認証を使用します。 管理者は、この情報を使用して、ドライブのリソースへの条件付きアクセスとアクセスを制御します。

-   信頼されたデバイスから会社のリソースにアクセスするユーザーのよりシームレスなサインイン エクスペリエンスを提供します。

### <a name="single-sign-on"></a>シングル サイン オン
シングル サインオン (SSO) このシナリオのコンテキストでは、既知のデバイスから企業リソースにアクセスするを入力する、エンド ユーザーがあるパスワード プロンプトの表示数を削減する機能です。 この機能は、ユーザーは企業アプリケーションにアクセスし、リソースをこのデバイスからの SSO 有効期間中に 1 つだけの時間を求められますことを意味します。 デバイスは、ワークプ レース ジョインを使用している場合、このデバイスを使用して登録されているユーザーは既定では 7 日間の永続的な SSO を取得します。 このユーザーは、シームレスなサインイン エクスペリエンス、同じセッションまたは新しいセッションを持っています。

## <a name="solution-overview"></a>ソリューションの概要
このソリューションの一部として、サポートされているデバイスでワークプ レース ジョインを使用して、会社のリソースをシングル サインオン エクスペリエンスと方法を説明します。

> [!NOTE]
> Windows 8.1、iOS 6.0 以降、および Android 4.0 以降のデバイスをサポートするには、Azure Active Directory Device Registration をデバイス オブジェクトの書き戻しと一緒に構成を参照してくださいする必要があります[Azure Active Directory Device Registration Service を使用して内部設置型条件付きアクセスのステップ バイ ステップ ガイド](https://msdn.microsoft.com/library/azure/dn788908.aspx)

このソリューション ガイドでは、次のチュートリアルの手順を実行します。

1.  [Windows デバイスのチュートリアル: 職場への参加](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)

2.  [チュートリアル: iOS デバイスでワークプ レースに参加します。](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

3.  [チュートリアル: 職場へ Android デバイスの参加](../../ad-fs/operations/walkthrough--workplace-join-to-an-android-device.md)

## <a name="see-also"></a>参照してください。
[デバイス登録サービスによるフェデレーション サーバーを構成します。](../deployment/configure-a-federation-server-with-device-registration-service.md)



