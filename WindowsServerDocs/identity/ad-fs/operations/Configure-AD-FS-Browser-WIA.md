---
title: AD FS で Windows 統合認証 (WIA) を使用するブラウザーを構成します。
description: このドキュメントは、AD FS で WIA を使用するブラウザーを構成する方法を説明します
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f71680bb721635bd37197dca9d3ae4726099525f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845483"
---
# <a name="configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>AD FS で Windows 統合認証 (WIA) を使用するブラウザーを構成します。

既定では、Windows 統合認証 (WIA) が Active Directory フェデレーション サービス (AD FS) で Windows Server 2012 R2 を使用するアプリケーションに組織の内部ネットワーク (イントラネット) 内で発生する認証要求で有効にします。その認証のためのブラウザーです。

AD FS 2016 では、WIA を行う Windows Phone のない、また、(正しく)、キャッチも中に、Edge ブラウザーのできる強化された既定の設定があります。

    =~Windows\s*NT.*Edge

多くの場合は更新される場合でも、エッジの一般的なシナリオをサポートするために個々 のユーザー エージェント文字列を構成する必要が不要になったの上を意味します。

その他のブラウザーでは、AD FS プロパティを構成する**WiaSupportedUserAgents**を使用しているブラウザーに基づいて、必要な値を追加します。  以下の手順を使用することができます。



### <a name="view-wiasupporteduseragent-settings"></a>WIASupportedUserAgent 設定を表示します。
**WIASupportedUserAgents** WIA をサポートするユーザー エージェントを定義します。 AD FS は、ブラウザーまたはブラウザー コントロールでのログインを実行するときに、ユーザー エージェント文字列を分析します。

次の PowerShell の例を使用して、現在の設定を表示することができます。

```powershell
    $strings = Get-AdfsProperties | select -ExpandProperty WiaSupportedUserAgents
```

![WIA サポート](../operations/media/Configure-AD-FS-Browser-WIA/wiasupport.png)

### <a name="change-wiasupporteduseragent-settings"></a>WIASupportedUserAgent 設定の変更
新しい AD FS のインストールでは既定では、作成されたユーザー エージェント文字列の一致のセットがあります。 ただし、これらがあります期限切れのブラウザーおよびデバイスへの変更に基づきます。 特に、Windows デバイスでは、トークンにわずかな違いを類似のユーザー エージェント文字列があります。 次の Windows PowerShell の例は、シームレスな WIA をサポートする今日の市場にあるデバイスの現在のセットの最善のガイダンスを提供します。

```powershell
    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")
```

上記のコマンドは AD FS は、WIA の次のユース ケースをのみ説明を確認します。

ユーザー エージェント|使用事例|
-----|-----|
MSIE 6.0|IE 6.0|
MSIE 7.0; Windows NT|IE 7、IE イントラネット ゾーンでします。 デスクトップ オペレーティング システムでは、"Windows NT"フラグメントが送信されます。|
MSIE 8.0|IE 8.0 (デバイスがありませんこのを送信するより具体的にするため必要があります)|
MSIE 9.0|IE の 9.0 (デバイスがありません送信、詳細を確認する必要がありません)|
MSIE 10.0; Windows NT 6|Windows XP およびデスクトップ オペレーティング システムの新しいバージョンの IE 10.0</br></br>送信するため、(使用してモバイル設定を優先) Windows Phone 8.0 デバイスは除外されます。</br></br>ユーザー エージェント:Mozilla/5.0 (互換性があります。MSIE 10.0 です。Windows Phone 8.0。Trident/6.0。発行元の IEMobile/10.0 です。ARM;タッチです。NOKIA;Lumia 920)|
Windows NT 6.3;Trident または 7.0</br></br>Windows NT 6.3;Win64;x64。Trident または 7.0</br></br>Windows NT 6.3; WOW64; Trident/7.0| Windows 8.1 デスクトップ オペレーティング システム、さまざまなプラットフォーム|
Windows NT 6.2;Trident または 7.0</br></br>Windows NT 6.2;Win64;x64。Trident または 7.0</br></br>Windows NT 6.2; WOW64; Trident/7.0|Windows 8 デスクトップ オペレーティング システム、さまざまなプラットフォーム|
Windows NT 6.1;Trident または 7.0</br></br>Windows NT 6.1;Win64;x64。Trident または 7.0</br></br>Windows NT 6.1;これは、WOW64Trident または 7.0|Windows 7 デスクトップ オペレーティング システム、さまざまなプラットフォーム|
MSIPC を右クリックし| Microsoft Information Protection とクライアントの制御|
Windows Rights Management クライアント|Windows Rights Management クライアント|
