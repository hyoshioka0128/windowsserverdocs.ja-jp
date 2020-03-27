---
title: Windows 管理センター v1909 でのクラスター接続の種類の変更
description: Windows 管理センター v1909 でのクラスター接続の種類の変更
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 10/01/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 5324f782ea3c02ed24968d4b3ef58ab8b6ac9d32
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319352"
---
# <a name="cluster-connection-type-changes-in-windows-admin-center-v1909"></a>Windows 管理センター v1909 でのクラスター接続の種類の変更

>適用対象: Windows Admin Center、Windows Admin Center Preview

> [!IMPORTANT]
> このドキュメントでは、windows 管理センターの拡張機能の開発者が、フェールオーバークラスターとハイパー集約型クラスター (HCI) ソリューション用の Windows 管理センターツールを開発する際に必要な変更について説明します。 これは、Windows 管理センター v1909 Preview リリースおよび将来の GA リリースと互換性を持たせるために、拡張機能に必要な必須の変更です。

Windows 管理センター v1909 では、2つの異なるクラスター接続の種類 (フェールオーバークラスターとハイパー収束クラスター接続) を1つのクラスター接続の種類に統合しました。 クラスターを追加する接続の種類を決定するために、クラスターの構成を事前に特定する必要がなくなりました。また、クラスターを異なる種類の接続として2回追加して、異なるツールセットにアクセスできるようにします。 クラスターを "Windows Server クラスター" として追加できるようになりました。適切なツールは、主に記憶域スペースダイレクトが有効になっているかどうかに基づいて読み込まれます。

これには接続の種類の定義を変更する必要があり、クラスター関連ツールがどのような場合に読み込むかを決定するために、クラスター用のツールを提供する拡張機能 (HCI クラスターまたは非 HCI クラスターのどちらかまたは両方) が実装の変更を必要とします。以下に。

## <a name="manifestjson---solutionsids-and-connectiontypes"></a>manifest-solutionsIds および connectionTypes

以前は、フェールオーバークラスターまたは HCI クラスターの接続の種類に対してツールを表示するには、```manifest.json``` ファイルで次の定義のいずれかを使用しました。

フェールオーバークラスターの場合:
``` json
    {
        "entryPointType": "tool",
        "name": "MyToolName",
        "urlName": "MyToolUrl",
        "displayName": "MyToolDisplayName",
        "description": "MyToolDescription",
        "icon": "MyToolIcon",
        "path": "MyToolPath",
        "iframeId": "MyToolIframeId",
        "requirements": [
        {
            "solutionIds": [
                "msft.sme.failover-cluster!failover-cluster"
            ],
            "connectionTypes": [
                "msft.sme.connection-type.cluster"
            ]
        }
        ]
    }
```

HCI クラスターでは、上の強調表示されたセクションが次のように置き換えられています。
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!SDDC"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.hyper-converged-cluster"
        ]
    }
    ]
```

Windows 管理センター1909以降では、2つの solutionIds と connectionTypes が次のように置き換えられています。
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!cluster"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.cluster"
        ]
    }
    ]
```

これは、現時点でサポートされている唯一のクラスター関連の solutionIds および connectionTypes 型です。 ツールが、この solutionIds および connectionTypes 型でのみ定義されている場合、HCI クラスターであるかどうかに関係なく、任意のフェールオーバークラスター接続に対して読み込まれます。 HCI クラスターまたは非 HCI クラスターに対してのみ使用できるようにツールを制限する場合は、次のセクションで説明する新しいインベントリプロパティを追加で使用する必要があります。

## <a name="manifestjson--inventory-properties"></a>manifest-inventory プロパティ
サーバーまたはクラスターに接続すると、Windows 管理センターは一連のインベントリプロパティに対してクエリを実行します。このプロパティを使用して、ツールをいつ使用できるかを判断するための条件を作成できます (詳細については、「[ツールの表示を制御](dynamic-tool-display.md)するドキュメント」の「インベントリのプロパティ」セクションを参照してください)。 Windows 管理センター v1909 では、この一覧に2つの新しいプロパティが追加されました。このプロパティを使用して、クラスターがハイパー集約クラスターであるかどうかを判断できます。 

### <a name="iss2denabled"></a>isS2dEnabled
技術的には、ハイパー収束クラスターは、記憶域スペースダイレクト (S2D) が有効になっているフェールオーバークラスターとして定義されます。 ツールをハイパー集約クラスターでのみ使用できるようにする場合は (S2D が有効になっている場合)、次のインベントリ条件を追加します。
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!cluster"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.cluster"
        ],
        "conditions": [
        {
            "inventory": {
                "isS2dEnabled": {
                    "type": "boolean",
                    "operator": "is"
                }
            }
        }
        ]
    }
    ]
```
> [!TIP] 
> S2D が有効になっていない場合にのみツールを使用できるようにするには、"operator" 値を "not" に変更します。

### <a name="isbritannicaenabled"></a>isBritannicaEnabled
さらに、SDDC 管理クラスターリソースに依存していて、SDDC オブジェクトモデルを使用している場合は、次の条件を確認することができます。
``` json
    "conditions": [
        {
            "inventory": {
                "isS2dEnabled": {
                    "type": "boolean",
                    "operator": "is"
                },
                "isBritannicaEnabled": {
                    "type": "boolean",
                    "operator": "is"
                }
            }
        }
    ]
```

## <a name="backward-compatibility-to-support-previous-versions-of-windows-admin-center"></a>以前のバージョンの Windows 管理センターをサポートするための旧バージョンとの互換性
拡張機能が v1904 GA リリースなどの古いバージョンの Windows 管理センターで引き続き動作するようにするには、以前の solutionIds と connectionTypes の定義を新しい定義と共に使用できます。 Windows 管理センターのすべてのバージョンの HCI クラスターに対してのみツールを表示するには、次の例を参照してください。
``` json
    "requirements": [
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!SDDC"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.hyper-converged-cluster"
        ]
    },
    {
        "solutionIds": [
            "msft.sme.software-defined-data-center!SDDC",
            "msft.sme.software-defined-data-center!cluster"
        ],
        "connectionTypes": [
            "msft.sme.connection-type.hyper-converged-cluster",
            "msft.sme.connection-type.cluster"
        ],
        "conditions": [
            {
                "inventory": {
                    "isS2dEnabled": {
                        "type": "boolean",
                        "operator": "is"
                    }
                }
            }
        ]
    }
    ]
```

## <a name="known-issue-appcontextserviceactiveconnectionishyperconvergedclusterisfailovercluster-is-not-set-properly-in-windows-admin-center-v1909"></a>既知の問題: isHyperConvergedCluster/isFailoverCluster が Windows 管理センター v1909 で適切に設定されていない activeConnection
最近の変更の回帰は、```AppContextService.activeConnection.isHyperConvergedCluster/isFailoverCluster``` のプロパティが Windows 管理センター v1909 で適切に設定されておらず、常に false になることです。 これは、次のリリースの v1910 で修正される予定ですが、2020の次の GA リリースでは非推奨となり、使用できなくなります。 今後、これを次のコードに置き換えて、```this.connectHCI```を使用することができます。
```
    import { ClusterInventoryCache } from '@msft-sme/core';

    constructor(
        ...
        private appContextService: AppContextService,
        ...
    ) {
        ...
        this.clusterInventoryCache = new ClusterInventoryCache(
            this.appContextService,
            <SharedCacheOptions>{ expiration: Constants.sharedCacheExpiration }
        );

         this.isBritannicEnabled().subscribe(result => this.connectHCI = result);
    }

    private isBritannicEnabled(): Observable<boolean> {
        return this.clusterInventoryCache.query(this.getClusterInventoryQueryParameters())
        .pipe(
            map(inventory => {
                return inventory.instance.isBritannicaEnabled;
        }));
    }

    private getClusterInventoryQueryParameters(): ClusterInventoryParams {
        const nodeName = this.appContextService.activeConnection.validNodeName;
        const endpoint = this.appContextService.authorizationManager.getJeaEndpoint(nodeName);
        const options = { powerShellEndpoint: endpoint };
        return {
            name: nodeName,
            requestOptions: options
        };
    }
```