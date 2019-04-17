---
title: "Active Directory フェデレーション サービスと証明書のキーの指定] プロパティについて"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: a5307da5-02ff-4c31-80f0-47cb17a87272
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: db58fcce054f34c4b0a3f6725456badae9fd0468
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-and-certificate-keyspec-property-information"></a>AD FS と証明書の KeySpec プロパティについて
キーの仕様 ("KeySpec") は、証明書とキーに関連付けられているプロパティです。 これは、署名、暗号化、またはその両方の証明書に関連付けられている秘密キーを使用できるかどうかを指定します。   

KeySpec 値が正しくない AD FS と Web アプリケーション プロキシがエラーを引き起こすなど。


- (ただし、36888 と 36874 SChannel イベント ログに記録される可能性があります) に記録されたなしの AD FS イベントと AD FS または Web アプリケーション プロキシに SSL/TLS 接続を確立するために失敗
- AD FS または WAP ログインの失敗は、ページに表示されるエラー メッセージなしでベースの認証] ページを形成します。

イベント ログでは、次を参照してください可能性があります。

    Log Name:      AD FS Tracing/Debug
    Source:        AD FS Tracing
    Date:          2/12/2015 9:03:08 AM
    Event ID:      67
    Task Category: None
    Level:         Error
    Keywords:      ADFSProtocol
    User:          S-1-5-21-3723329422-3858836549-556620232-1580884
    Computer:      ADFS1.contoso.com
    Description:
    Ignore corrupted SSO cookie.

## <a name="what-causes-the-problem"></a>問題を原因します。
KeySpec プロパティでは、生成された場合または取得して Microsoft CryptoAPI (CAPI) から Microsoft レガシ暗号化記憶域プロバイダー (CSP)、キーを使用する方法を識別します。

KeySpec 値**1**、または**AT_KEYEXCHANGE**、署名と暗号化に使用できます。  値**2**、または**AT_SIGNATURE**の署名にのみ使用します。

最も一般的な KeySpec 誤構成は、証明書をトークン署名証明書以外の値を 2 を使用しています。  

キーは Cryptography Next Generation (CNG) プロバイダーを使用して生成された証明書は、キーの仕様の概念がないと KeySpec 値は 0 に常になります。

有効な KeySpec 値以下を確認する方法を参照してください。 

### <a name="example"></a>使用例
従来の CSP の例は、Microsoft Enhanced Cryptographic Provider です。 

か、Microsoft RSA CSP キー blob 形式に、アルゴリズム識別子が含まれている**CALG_RSA_KEYX**または**CALG_RSA_SIGN**をそれぞれのいずれかのサービス要求に * * AT_KEYEXCHANGE * * または**AT_SIGNATURE**キー。
  
次のようにマップ KeySpec 値に RSA キーのアルゴリズム識別子

| プロバイダーがサポートされているアルゴリズム| Capi ストアの呼び出しの値をキーの仕様 |
| --- | --- |
|署名と暗号化解除に使用できる CALG_RSA_KEYX: RSA キー| AT_KEYEXCHANGE (または KeySpec = 1)|
CALG_RSA_SIGN: RSA 署名キーのみ |AT_SIGNATURE (または KeySpec = 2)|

## <a name="keyspec-values-and-associated-meanings"></a>KeySpec 値と関連付けられている意味
次に、さまざまな KeySpec 値の意味を示します。

|Keyspec 値|手段|推奨される AD FS の使用|
| --- | --- | --- |
|0|証明書が CNG cert です。|SSL 証明書のみ|
|1|レガシ CAPI (非 CNG) 証明書の署名と暗号化解除キーを使用できます。|    トークン署名、トークンの暗号化の解除、サービス通信証明書を SSL|
|2|レガシ CAPI (非 CNG) 証明書の署名にのみ、キーを使用できます。|推奨されません。|

## <a name="how-to-check-the-keyspec-value-for-your-certificates--keys"></a>証明書の KeySpec 値を確認する方法]、[キー
使用できる証明書の値を表示する、**certutil**コマンド ライン ツールです。  

例を次に示します: **certutil – v – ストア my**します。  これが、画面に証明書情報をダンプされます。

![証明書の Keyspec](media/AD-FS-and-KeySpec-Property/keyspec1.png)

[次の 2 つの CERT_KEY_PROV_INFO_PROP_ID ファイルの場所。


1. **プロバイダーの種類:**これはレガシ暗号化ストレージ プロバイダー (CSP) を使用する証明書またはキー記憶域プロバイダーのベースに新しい証明書 Next Generation (CNG) API のかどうかを示します。  0 以外の値では、従来のプロバイダーを示します。
2.  **KeySpec:** AD FS の証明書の有効な KeySpec 値を次に示します。

    レガシ CSP プロバイダー (プロバイダーの種類を 0 に等しくない):
    
    |AD FS 証明書の目的|有効な KeySpec 値|
    | --- | --- |
    |サービスの通信|1|
    |トークン暗号化解除|1|
    |トークン署名|1 と 2|
    |SSL|1|

    CNG プロバイダー (プロバイダーの種類 = 0)。
    |AD FS 証明書の目的|有効な KeySpec 値|
    | --- | --- |   
    |SSL|0|

## <a name="how-to-change-the-keyspec-for-your-certificate-to-a-supported-value"></a>サポートされている値に証明書の keyspec を変更する方法
KeySpec 値を変更する場合は再生成されたり、再度証明書機関によって発行された証明書は必要ありません。  次の手順を使用して、証明書ストアに、完全な証明書と秘密キーを PFX ファイルからを再インポートすることによって、KeySpec を変更できます。


1. 最初に、確認しができるように、構成し直す必要に応じて再インポートした後に、既存の証明書の秘密キーのアクセス許可を記録します。
2. PFX ファイルに秘密キーを含む証明書をエクスポートします。
3. AD FS と WAP サーバーごとに次の手順を実行します。
    1. 証明書を削除 (AD FS から/WAP サーバー)
    2. 管理者特権の PowerShell コマンド プロンプトを開き、次のコマンドレットの構文を使用して、(これは、すべての AD FS 証明書の目的の動作) AT_KEYEXCHANGE 値を指定する各 AD FS と WAP サーバー上の PFX ファイルをインポートします。
        1. C:\ > certutil – importpfx certfile.pfx AT_KEYEXCHANGE
        2. PFX のパスワードを入力してください。
    3. 上記の完了後、次を操作します。
        1. 秘密キーのアクセス許可を確認します。
        2. Adfs または wap サービスを再起動します。





