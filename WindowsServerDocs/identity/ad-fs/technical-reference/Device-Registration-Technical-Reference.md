---
ms.assetid: 69ec592a-5499-4249-8ba0-afa356a8ff75
title: デバイス登録のテクニカル リファレンス
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f2e373f45088105a7ac9ca5cb43fbebc6452ccb9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188578"
---
# <a name="device-registration-technical-reference"></a>デバイス登録のテクニカル リファレンス
デバイス登録サービス\(DRS\)は Windows Server 2012 R2 で Active Directory フェデレーション サービス役割に含まれている新しい Windows サービスです。  DRS は、AD FS ファーム内のすべてのフェデレーション サーバーにインストールし、構成する必要があります。  DRS の展開の詳細については、「 [デバイス登録サービスを使用してフェデレーション サーバーを構成する](https://technet.microsoft.com/library/dn486831.aspx)」を参照してください。  
  
## <a name="active-directory-objects-created-when-a-device-is-registered"></a>デバイスの登録時に作成される Active Directory オブジェクト  
次の Active Directory オブジェクトは、デバイス登録サービス の一部として作成されます。  
  
### <a name="device-registration-configuration"></a>デバイス登録構成  
デバイス登録構成は、Active Directory フォレストの構成名前付けコンテキストに格納されます \(たとえば、 **CN\=Device Registration Configuration, CN\=サービス、< configuration\-名前付け\-コンテキスト >** \)します。 このオブジェクトは、Active Directory フォレストにデバイス登録用のイニシャルが付けられたときに作成されます。  
  
デバイス登録構成には、次の要素が含まれます。  
  
-   **発行者キー**  
  
    登録済みデバイスに関連付けられた X.509 証明書を発行するために使用される、公開キーと秘密キーです。  秘密キーは DKM で保護されます。  
  
-   **デバイス登録サービスの構成**  
  
    デバイス登録サービスに関連するポリシーです。  
  
### <a name="registered-devices-container"></a>登録済みデバイス コンテナー  
デバイス オブジェクト コンテナーは、Active Directory フォレスト内のいずれかのドメイン下に作成されます。  このオブジェクト コンテナーには、Active Directory フォレストのすべてのデバイス オブジェクトが格納されます。  
  
既定では、コンテナーは AD FS と同じドメインに作成されます。  \(たとえば、 **CN\=RegisteredDevices, DC\=< 既定\-名前付け\-コンテキスト >** \)します。このオブジェクトは、Active Directory フォレストがデバイスの登録の initialed されるときに作成されます。  
  
### <a name="registered-devices"></a>登録済みデバイス  
デバイス オブジェクトは、Active Directory 内の新しい軽量オブジェクトです。  ユーザー、デバイス、および会社の関係を表すために使用されます。  デバイス オブジェクトは、AD FS によって署名された証明書を使用して、物理デバイスを Active Directory 内の論理デバイス オブジェクトに関連付けます。  
  
登録済みデバイスには、次の要素が含まれます。  
  
-   **表示名**  
  
    デバイスのフレンドリ名です。  Windows デバイスの場合、これはコンピューターのホスト名です。  
  
-   **デバイス Id**  
  
    デバイス登録サーバーによって生成される GUID です。  
  
-   **証明書の拇印**  
  
    登録済みデバイスに使用される X.509 証明書の証明書拇印です。  
  
-   **OS の種類**  
  
    デバイスのオペレーティング システムの種類です。  
  
-   **OS バージョン**  
  
    デバイスのオペレーティング システムのバージョンです。  
  
-   **有効になっています。**  
  
    デバイスが Active Directory で有効になっているかどうかを示すブール値です。  有効になっているデバイスだけがサービスにアクセスできます。  
  
-   **おおよその最終使用時刻**  
  
    リソースへのアクセスにデバイスが使用されたおおよその時間です。  レプリケーション トラフィックを制限するため、この値は 14 日に 1 回だけ更新されます。  
  
-   **登録済み所有者**  
  
    セキュリティ Id \(SID\)のこのデバイスをワークプ レースに参加しているユーザー。  
  
## <a name="ad-fsdrs-server-ssl-certificate-revocation-checking"></a>AD FS\/DRS サーバーの SSL 証明書失効の確認  
ワークプ レース ジョイン クライアントは、AD FS サーバーの SSL 証明書の有効性をチェックします。  AD FS サーバーの SSL 証明書が証明書失効リストを含むかどうか\(CRL\)エンドポイント、クライアントは、証明書の検証を指定されたエンドポイントに到達することである必要があります。  
  
テスト環境とテスト証明書機関を使用しているかどうかは\(CA\)されません、CA によって発行されたサーバー証明書に CRL のエンドポイントを含めることができますし、サーバーに SSL 証明書を発行します。  そうすると、ワークプ レース ジョイン クライアントが CRL のチェックをバイパスできるようになります。  
  
> [!CAUTION]  
> これを運用システムで行うことは、絶対にお勧めしません。  
  

