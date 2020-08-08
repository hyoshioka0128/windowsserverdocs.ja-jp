---
title: Vm とコンテナーのホストコンピューティングネットワーク (HCN) サービス API
description: ホストコンピューティングネットワーク (HCN) サービス API は、仮想ネットワーク、仮想ネットワークエンドポイント、および関連付けられているポリシーを管理するためのプラットフォームレベルのアクセスを提供する公開された Win32 API です。 これにより、Windows ホストで実行されている仮想マシン (Vm) とコンテナーの接続性とセキュリティが提供されます。
ms.author: jmesser
author: jmesser81
ms.date: 11/05/2018
ms.openlocfilehash: 8e83af4ea54d2fcc75ff8ff054f4ad253a5422ea
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955661"
---
# <a name="host-compute-network-hcn-service-api-for-vms-and-containers"></a>Vm とコンテナーのホストコンピューティングネットワーク (HCN) サービス API

>適用対象: Windows Server (半期チャネル)、Windows Server 2019

ホストコンピューティングネットワーク (HCN) サービス API は、仮想ネットワーク、仮想ネットワークエンドポイント、および関連付けられているポリシーを管理するためのプラットフォームレベルのアクセスを提供する公開された Win32 API です。 これにより、Windows ホストで実行されている仮想マシン (Vm) とコンテナーの接続性とセキュリティが提供されます。

開発者は HCN サービス API を使用して、アプリケーションワークフロー内の Vm とコンテナーのネットワークを管理します。 HCN API は、開発者に最適なエクスペリエンスを提供するように設計されています。 エンドユーザーは、これらの Api を直接操作することはありません。

## <a name="features-of-the-hcn-service-api"></a>HCN サービス API の機能
-    OnCore/VM 上のホストネットワークサービス (HNS) によってホストされる C API として実装されます。

-    ネットワーク、エンドポイント、名前空間、ポリシーなどの HCN オブジェクトを作成、変更、削除、および列挙する機能を提供します。 操作は、オブジェクト (ネットワークハンドルなど) へのハンドルに対して実行され、内部的には RPC コンテキストハンドルを使用してこれらのハンドルを実装します。

-    スキーマベース。 API のほとんどの関数は、JSON ドキュメントとして関数呼び出しの引数を含む文字列として、入力パラメーターと出力パラメーターを定義します。 JSON ドキュメントは、厳密に型指定されたバージョン管理されたスキーマに基づいています。これらのスキーマは、パブリックドキュメントに含まれています。

-    サービス全体のイベント (ネットワークの作成や削除など) の通知にクライアントが登録できるようにするために、サブスクリプション/コールバック API が用意されています。

-    HCN API はデスクトップブリッジで動作します (別名、 Centennial) システムサービスで実行されているアプリ。 API は、呼び出し元からユーザートークンを取得して ACL をチェックします。

>[!TIP]
>HCN サービス API は、バックグラウンドタスクとフォアグラウンド以外のウィンドウでサポートされています。

## <a name="terminology-host-vs-compute"></a>用語: ホストとコンピューティング
ホストコンピューティングサービスを使用すると、呼び出し元は、1台の物理コンピューター上に仮想マシンとコンテナーの両方を作成して管理することができます。 業界の用語に従うために名前が付けられています。

- **ホスト**は、仮想化業界で広く使用されており、仮想化されたリソースを提供するオペレーティングシステムを指します。

- **Compute**は、仮想マシンだけではない仮想化方法を参照するために使用されます。 ホストコンピューティングネットワークサービスを使用すると、呼び出し元は、1台の物理コンピューター上の仮想マシンとコンテナーの両方のネットワークを作成および管理できます。

## <a name="schema-based-configuration-documents"></a>スキーマベースの構成ドキュメント
明確に定義されたスキーマに基づく構成ドキュメントは、仮想化領域に確立された業界標準です。 Docker や Kubernetes などのほとんどの仮想化ソリューションでは、構成ドキュメントに基づく Api が提供されます。 Microsoft に参加することで、いくつかの業界イニシアチブが、 [Openapi](https://www.openapis.org/)などのスキーマを定義して検証するためのエコシステムを推進しています。  これらのイニシアチブは、 [Open Container イニシアチブ (OCI)](https://www.opencontainers.org/)など、コンテナーに使用されるスキーマの特定のスキーマ定義の標準化を推進します。

構成ドキュメントの作成に使用される言語は[JSON](https://tools.ietf.org/html/rfc8259)で、次のものと組み合わせて使用します。
-    ドキュメントのオブジェクトモデルを定義するスキーマ定義
-    JSON ドキュメントがスキーマに準拠しているかどうかの検証
-    Api の呼び出し元によって使用されるプログラミング言語における、これらのスキーマのネイティブ表現との間での JSON ドキュメントの自動変換

頻繁に使用されるスキーマ定義は[Openapi](https://www.openapis.org/)と[JSON スキーマ](http://json-schema.org/)で、ドキュメント内のプロパティの詳細な定義を指定できます。次に例を示します。
-    プロパティの有効な値のセット (パーセントを表すプロパティの場合は0-100 など)。
-    列挙型の定義。これは、プロパティに対して有効な文字列のセットとして表されます。
-    文字列の予期される書式の正規表現。

HCN Api のドキュメントの一部として、microsoft は、JSON ドキュメントのスキーマを OpenAPI 仕様として公開することを計画しています。 この仕様に基づき、スキーマの言語固有の表現によって、クライアントで使用されるプログラミング言語でスキーマオブジェクトをタイプセーフに使用できるようになります。

### <a name="example"></a>例

次に、VM の構成ドキュメントに含まれる SCSI コントローラーを表すオブジェクトのワークフローの例を示します。

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
>[NewIn ("2.0") 注釈は、スキーマ定義のバージョン管理のサポートの一部です。

この内部定義から、スキーマの OpenAPI 仕様を生成します。

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

[Swagger](https://swagger.io/)などのツールを使用すると、クライアントによって使用されるスキーマプログラミング言語の言語固有の表現を生成できます。 Swagger は、C#、ゴー、Javascript、Python などのさまざまな言語をサポートしています。

- 最上位の IPAM & サブネットオブジェクト用に[生成された C# コードの例](example-c-sharp.md)。

- 最上位の IPAM & サブネットオブジェクトの[生成されたジャンプコードの例](example-go.md)。 ゴーは、ホストコンピューティングネットワークサービス Api の2つのコンシューマーである Docker と Kubernetes によって使用されます。 外出先には、JSON ドキュメントとの間での入力型のマーシャリングのサポートが組み込まれています。

コードの生成と検証に加えて、ツールを使用して、JSON ドキュメント (つまり[Visual Studio Code](https://code.visualstudio.com/Docs/languages/json)) の操作を簡略化することができます。

### <a name="top-level-objects-defined-in-the-hcnschemasmars-file"></a>HCN で定義されているトップレベルのオブジェクト。スキーマの mars ファイル
前述のように、HCN Api によって使用されるドキュメントのドキュメントスキーマは、onecore/vm/dv/net/hns/schema/mars/Schema の下にある一連の mars ファイルで検索できます。

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

- [一般的な HCN シナリオ](hcn-scenarios.md)の詳細については、こちらを参照してください。

- [HCN の RPC コンテキストハンドル](hcn-declaration-handles.md)の詳細については、こちらを参照してください。

- [Hcn JSON ドキュメントスキーマ](hcn-json-document-schemas.md)の詳細については、こちらを参照してください。
