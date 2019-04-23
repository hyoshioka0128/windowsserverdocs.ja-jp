---
title: Vm とコンテナーのネットワークの計算 (HCN) サービスの API をホストします。
description: ホスト ネットワークの計算 (HCN) サービスの API は、仮想ネットワーク、仮想ネットワークのエンドポイント、および関連付けられているポリシーを管理するためのプラットフォーム レベルのアクセスを提供するパブリックに公開された Win32 API です。 まとめてこれにより接続とセキュリティの仮想マシン (Vm) と Windows ホスト上で実行されているコンテナー。
ms.author: jmesser
author: jmesser81
ms.date: 11/05/2018
ms.openlocfilehash: 50af0dab69633aa6e07ded68e9246aa0315377f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844983"
---
# <a name="host-compute-network-hcn-service-api-for-vms-and-containers"></a>Vm とコンテナーのネットワークの計算 (HCN) サービスの API をホストします。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

ホスト ネットワークの計算 (HCN) サービスの API は、仮想ネットワーク、仮想ネットワークのエンドポイント、および関連付けられているポリシーを管理するためのプラットフォーム レベルのアクセスを提供するパブリックに公開された Win32 API です。 まとめてこれにより接続とセキュリティの仮想マシン (Vm) と Windows ホスト上で実行されているコンテナー。 

開発者は、Vm のネットワークと、アプリケーションのワークフロー内のコンテナーを管理するのに HCN サービス API を使用します。 HCN API は、開発者にとって最適なエクスペリエンスを提供する設計されています。 エンドユーザーはこれらの Api と直接対話しません。  

## <a name="features-of-the-hcn-service-api"></a>HCN Service の API の機能
-   OnCore/VM で Host Network Service (HNS) によってホストされている C API として実装されます。

-   作成、変更、削除、および HCN オブジェクトなど、ネットワーク、エンドポイント、名前空間、およびポリシーを列挙する機能を提供します。 オブジェクト (ネットワーク ハンドルなど) へのハンドルで操作を実行し、これらのハンドルは RPC のコンテキスト ハンドルを使用して実装されている内部的にします。

-   スキーマに基づいています。 API のほとんどの関数は、入力を定義し、JSON ドキュメントとして関数呼び出しの引数を含む文字列としてパラメーターを出力します。 JSON ドキュメントは、厳密に型指定されたとバージョン管理されたスキーマに基づくが、これらのスキーマは、パブリックのドキュメントの一部です。 

-   クライアントのネットワークの作成と削除などのサービス全体のイベント通知に登録するには、サブスクリプションやコールバック API が提供されます。

-   HCN API の動作では、デスクトップ ブリッジ (別名。 Centennial) のシステム サービスで実行されているアプリ。 API は、呼び出し元からユーザー トークンを取得することによって、ACL を確認します。

>[!TIP]
>HCN サービス API は、バック グラウンド タスクとフォア グラウンドで非 windows でサポートされます。 

## <a name="terminology-host-vs-compute"></a>用語:Vs をホストします。計算
ホストのコンピューティング サービスでは、作成して仮想マシンと 1 台の物理コンピューター上のコンテナーの両方を管理する呼び出し元を許可します。 業界用語に従うという名前です。 

- **ホスト**仮想化されたリソースを提供するオペレーティング システムを参照する仮想化の業界で広く使用されています。

- **コンピューティング**だけの仮想マシンよりも広範にある仮想化メソッドを参照するために使用します。 ネットワーク コンピューティング サービスをホストには、呼び出し元を作成し、仮想マシンと 1 台の物理コンピューター上のコンテナーの両方のネットワークの管理ができます。

## <a name="schema-based-configuration-documents"></a>スキーマ ベースの構成のドキュメント
適切に定義されたスキーマに基づいて構成ドキュメントは、仮想化の分野で確立された業界標準です。 Docker と Kubernetes などのほとんどの仮想化ソリューションでは、Api の構成ドキュメントに基づくを提供します。 Microsoft の参加のいくつかの業界イニシアティブ ドライブを定義して、これらのスキーマの検証をなどのエコシステム[OpenAPI](https://www.openapis.org/)します。  このような取り組みなどのコンテナーでは、使用されるスキーマの特定のスキーマの定義の標準化をドライブも[Open Container Initiative (OCI)](https://www.opencontainers.org/)します。

構成ドキュメントを作成するために使用される言語は[JSON](https://tools.ietf.org/html/rfc8259)と組み合わせて使用します。
-   ドキュメント オブジェクト モデルを定義するスキーマの定義
-   JSON ドキュメントがスキーマに準拠しているかどうかの検証
-   自動化して、Api の呼び出し元が使用されているプログラミング言語でこれらのスキーマのネイティブ形式から JSON ドキュメントの変換 

頻繁に使用されるスキーマの定義は[OpenAPI](https://www.openapis.org/)と[JSON スキーマ](http://json-schema.org/)、たとえば、文書内のプロパティの定義の詳細を指定することができます。
-   0 ~ 100 パーセントを表すプロパティなどのプロパティの値の有効なセット。
-   一連のプロパティの有効な文字列として表される列挙体の定義。
-   文字列の書式の正規表現。 

HCN Api を文書化の一環として、OpenAPI 仕様として、JSON ドキュメントのスキーマを公開する予定です。 スキーマの言語固有の表現はこの仕様に基づき、クライアントで使用するプログラミング言語のスキーマ オブジェクトのタイプ セーフの使用許可できます。 

### <a name="example"></a>例 

次は、VM の構成ドキュメントに SCSI コント ローラーを表すオブジェクトをこのワークフローの例です。 

Windows のソース コードで .mars ファイルを使用してスキーマを定義します onecore/vm/dv/net/hns/schema/mars/Schema/HCN.Schema.Network.mars。

```
enum IpamType
{
    [NewIn("2.0")] Static,
    [NewIn("2.0")] Dhcp,
};

class Ipam
{
    // Type : dhcp
    [NewIn("2.0"),OmitEmpty] IpamType   Type;
    [NewIn("2.0"),OmitEmpty] Subnet     Subnets[];
};

class Subnet : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] string         IpAddressPrefix;
    [NewIn("2.0"),OmitEmpty] SubnetPolicy   Policies[];
    [NewIn("2.0"),OmitEmpty] Route          Routes[];
};


enum SubnetPolicyType
{
    [NewIn("2.0")] VLAN
};

class SubnetPolicy
{
    [NewIn("2.0"),OmitEmpty] SubnetPolicyType                 Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Common.PolicySettings Data;
};

class PolicySettings
{
    [NewIn("2.0"),OmitEmpty]  string      Name;
};

class VlanPolicy : HCN.Schema.Common.PolicySettings 
{
    [NewIn("2.0")] uint32 IsolationId;
};

class Route 
{
    [NewIn("2.0"),OmitEmpty] string NextHop;
    [NewIn("2.0"),OmitEmpty] string DestinationPrefix;
    [NewIn("2.0"),OmitEmpty] uint16 Metric;
};

```

>[!TIP]
>[NewIn("2.0") 注釈はスキーマ定義のバージョン管理サポートの一部です。

この内部の定義からは、スキーマの OpenAPI 仕様を生成します。

```
{ 
    "swagger" : "2.0", 
    "info" : { 
       "version" : "2.1", 
       "title" : "HCN API" 
    },
    "definitions": {        
        "Ipam": {
            "type": "object",
            "properties": {
                "Type": {
                    "type": "string",
                    "enum": [
                        "Static",
                        "Dhcp"
                    ],
                    "description": " Type : dhcp"
                },
                "Subnets": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/Subnet"
                    }
                }
            }
        },
        "Subnet": {
            "type": "object",
            "properties": {
                "ID": {
                    "type": "string",
                    "pattern": "^[0-9A-Fa-f]{8}-([0-9A-Fa-f]{4}-){3}[0-9A-Fa-f]{12}$"
                },                
                "IpAddressPrefix": {
                    "type": "string"
                },
                "Policies": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/SubnetPolicy"
                    }
                },
                "Routes": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/Route"
                    }
                }
            }
        },
        "SubnetPolicy": {
            "type": "object",
            "properties": {
                "Type": {
                    "type": "string",
                    "enum": [
                        "VLAN",
                        "VSID"
                    ]
                },
                "Data": {
                    "$ref": "#/definitions/PolicySettings"
                }
            }
        },
        "PolicySettings": {
            "type": "object",
            "properties": {
                "Name": {
                    "type": "string"
                }
            }
        },                      
        "VlanPolicy": {
            "type": "object",
            "properties": {
                "Name": {
                    "type": "string"
                },
                "IsolationId": {
                    "type": "integer",
                    "format": "uint32"
                }
            }
        },
        "Route": {
            "type": "object",
            "properties": {
                "NextHop": {
                    "type": "string"
                },
                "DestinationPrefix": {
                    "type": "string"
                },
                "Metric": {
                    "type": "integer",
                    "format": "uint16"
                }
            }
        }        
    }
} 
```

などのツールを使用して[Swagger](https://swagger.io/)、言語固有の表現のプログラミング言語のクライアントで使用されるスキーマを生成します。 Swagger などのさまざまな言語をサポートC#、Go、Javascript、および Python)。

- [例で生成されたC#コード](example-c-sharp.md)最上位レベルの IPAM とサブネットのオブジェクトします。

- [生成された、Go コードの例](example-go.md)最上位レベルの IPAM とサブネットのオブジェクトします。 Go は、Docker と Kubernetes は 2 つのホスト ネットワーク サービスのコンピューティング Api のコンシューマーによって使用されます。 Go Go 型と JSON ドキュメントの間のマーシャ リングの組み込みサポートしています。

コードの生成と検証、だけでなく、JSON ドキュメントを簡単にできるようにするツールを使用することができます: つまり、 [Visual Studio Code](https://code.visualstudio.com/Docs/languages/json)します。

### <a name="top-level-objects-defined-in-the-hcnschemasmars-file"></a>最上位レベルのオブジェクトが、HCN で定義されています。Schemas.mars ファイル
前述のように、一連の下にある .mars ファイルの HCN Api で使用されるドキュメントのドキュメント スキーマを見つけることができます: onecore/vm/dv/net/hns/スキーマ/mars/スキーマ

最上位レベルのオブジェクトは次のとおりです。
- [HostComputeNetwork](hcn-scenarios.md#scenario-hcn)
- [HostComputeEndpoint](hcn-scenarios.md#scenario-hcn-endpoint)
- [HostComputeNamespace](hcn-scenarios.md#scenario-hcn-namespace)
- [HostComputeLoadBalancer](hcn-scenarios.md#scenario-hcn-load-balancer)

```
class HostComputeNetwork : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.NetworkMode          Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.NetworkPolicy        Policies[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.MacPool              MacPool;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.DNS                  Dns;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Ipam                 Ipams[];
};

class HostComputeEndpoint : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] string                                     HostComputeNetwork;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Endpoint.EndpointPolicy Policies[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Endpoint.IpConfig       IpConfigurations[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.DNS                     Dns;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Route                   Routes[];
    [NewIn("2.0"),OmitEmpty] string                                     MacAddress;
};

class HostComputeNamespace : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] uint32                                    NamespaceId;
    [NewIn("2.0"),OmitEmpty] Guid                                      NamespaceGuid;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Namespace.NamespaceType        Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Namespace.NamespaceResource    Resources[];
};

class HostComputeLoadBalancer : HCN.Schema.Common.Base
{
    [NewIn("2.0"), OmitEmpty] string                                               HostComputeEndpoints[]; 
    [NewIn("2.0"), OmitEmpty] string                                               VirtualIPs[]; 
    [NewIn("2.0"), OmitEmpty] HCN.Schema.Network.Endpoint.Policy.PortMappingPolicy PortMappings[]; 
    [NewIn("2.0"), OmitEmpty] HCN.Schema.LoadBalancer.LoadBalancerPolicy           Policies[];
};
```

## <a name="next-steps"></a>次のステップ

- 詳細については、 [HCN の一般的なシナリオ](hcn-scenarios.md)します。

- 詳細については、 [RPC コンテキスト ハンドル HCN](hcn-declaration-handles.md)します。

- 詳細については、 [HCN JSON ドキュメントのスキーマ](hcn-json-document-schemas.md)します。