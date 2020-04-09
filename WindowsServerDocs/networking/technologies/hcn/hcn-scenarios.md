---
title: ホストコンピューティングネットワーク (HCN) のシナリオ
ms.author: jmesser
author: jmesser81
ms.prod: windows-server
ms.date: 11/05/2018
ms.openlocfilehash: 2fdf0d13a0a362681a27106356fbe295532ed970
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859835"
---
# <a name="common-scenarios"></a>一般的なシナリオ

>適用対象: Windows Server (半期チャネル)、Windows Server 2019

## <a name="scenario-hcn"></a>シナリオ: HCN 


### <a name="create-an-hcn"></a>HCN を作成する

このサンプルでは、ホストコンピューティングネットワークサービス API を使用して、仮想 NIC を Virtual Machines またはコンテナーに接続するために使用できるホストコンピューティングネットワークをホスト上に作成する方法を示します。

```C++
using unique_hcn_network = wil::unique_any< 
    HCN_NETWORK, 
    decltype(&HcnCloseNetwork), 
    HcnCloseNetwork>; 


/// Creates a simple HCN Network, waiting synchronously to finish the task
void CreateHcnNetwork() 
{

    unique_hcn_network hcnnetwork;
    wil::unique_cotaskmem_string result;
    std::wstring settings = LR"( 
    { 
        "SchemaVersion": { 
            "Major": 2, 
            "Minor": 0 
        }, 
        "Owner" : "WDAGNetwork", 
        "Flags" : 0,
        "Type"  : 0,
        "Ipams" : [
            {
                "Type" : 0,
                "Subnets" : [
                    {
                        "IpAddressPrefix" : "192.168.1.0/24",
                        "Policies" : [
                            {
                                "Type" : "VLAN",
                                "IsolationId" : 100,
                            }
                        ],
                        "Routes" : [
                            {
                                "NextHop" : "192.168.1.1",
                                "DestinationPrefix" : "0.0.0.0/0",
                            }
                        ]

                    }
                ],
            },
        ],
        "MacPool":  {
            "Ranges" : [
                {
                    "EndMacAddress":  "00-15-5D-52-CF-FF",
                    "StartMacAddress":  "00-15-5D-52-C0-00"
                }
            ],
        },
        "Dns" : {
            "Suffix" : "net.home",
            "ServerList" : ["10.0.0.10"],
        }
    }
    })";    
    
    GUID networkGuid;  
    HRESULT result = CoCreateGuid(&networkGuid);

    result = HcnCreateNetwork(
        networkGuid,              // Unique ID 
        settings.c_str(),      // Compute system settings document 
        &hcnnetwork,
        &result 
        );
    if (FAILED(result)) 
    { 
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //    "ErrorCode" : <uint32>,
        //    "Error" : <string>,
        //    "Success" : <bool>,
       //   }

        // Failed to create network
        THROW_HR(result); 
    }  

    // Close the Handle
    result = HcnCloseNetwork(hcnnetwork.get());

    if (FAILED(result)) 
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }
        
}
```

### <a name="delete-an-hcn"></a>HCN の削除

このサンプルでは、ホストコンピューティングネットワークサービス API を使用して、ホストコンピューティングネットワークを開い & 削除する方法を示します。 

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID networkGuid; // Initialize it to appropriate network guid value 
    HRESULT hr = HcnDeleteNetwork(networkGuid, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
```


### <a name="enumerate-all-networks"></a>すべてのネットワークを列挙する

このサンプルでは、ホストコンピューティングネットワークサービス API を使用して、すべてのホストコンピューティングネットワークを列挙する方法を示します。

```C++
     wil::unique_cotaskmem_string resultNetworks;
     wil::unique_cotaskmem_string errorRecord;

     // Filter to select Networks based on properties
     std::wstring filter [] = LR"(
     { 
         "Name"  : "WDAG",
     })";
     HRESULT result = HcnEnumerateNetworks(filter.c_str(), &resultNetworks, &errorRecord);
     if (FAILED(result))
     {
         // UnMarshal  the result Json

         THROW_HR(result);
     }
```


### <a name="query-network-properties"></a>ネットワークのプロパティを照会する

このサンプルでは、ホストコンピューティングネットワークサービス API を使用してネットワークのプロパティを照会する方法を示します。

```C++
    unique_hcn_network hcnnetwork;
    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    { 
        // Future
    })";
    GUID networkGuid; // Initialize it to appropriate network guid value
    HRESULT hr = HcnOpenNetwork(networkGuid, &hcnnetwork, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    hr = HcnQueryNetworkProperties(hcnnetwork.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


## <a name="scenario-hcn-endpoint"></a>シナリオ: HCN エンドポイント

### <a name="create-an-hcn-endpoint"></a>HCN エンドポイントを作成する

このサンプルでは、ホストコンピューティングネットワークサービス API を使用してホストコンピューティングネットワークエンドポイントを作成し、仮想マシンまたはコンテナーにホットアドする方法を示します。

```C++
using unique_hcn_endpoint = wil::unique_any< 
    HCN_ENDPOINT, 
    decltype(&HcnCloseEndpoint), 
    HcnCloseEndpoint>; 

void CreateAndHotAddEndpoint() 
{
    unique_hcn_endpoint hcnendpoint;
    unique_hcn_network hcnnetwork;

    wil::unique_cotaskmem_string errorRecord;


    std::wstring settings[] = LR"( 
    { 
        "SchemaVersion": { 
            "Major": 2, 
            "Minor": 0 
        }, 
        "Owner" : "Sample", 
                   "Flags" : 0,
        "HostComputeNetwork" : "87fdcf16-d210-426e-959d-2a1d4f41d6d3",
        "DNS" : {
            "Suffix" : "net.home",
            "ServerList" : "10.0.0.10",
        }
    })";
    GUID endpointGuid;  
    HRESULT result = CoCreateGuid(&endpointGuid);

    result = HcnOpenNetwork(
        networkGuid,              // Unique ID 
        &hcnnetwork,
        &errorRecord
        );
    if (FAILED(result)) 
    { 
        // Failed to find network
        THROW_HR(result); 
    }                

    result = HcnCreateEndpoint(
        hcnnetwork.get(),
        endpointGuid,              // Unique ID 
        settings.c_str(),      // Compute system settings document 
        &hcnendpoint,
        &errorRecord
        );

    if (FAILED(result)) 
    { 
        // Failed to create endpoint
        THROW_HR(result); 
    }

    // Can use the sample from HCS API Spec on how to attach this endpoint 
    // to the VM using AddNetworkAdapterToVm   

    result = HcnCloseEndpoint(hcnendpoint.get());

    if (FAILED(result))
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }
             
}
```


### <a name="delete-an-endpoint"></a>エンドポイントの削除

このサンプルでは、ホストコンピューティングネットワークサービス API を使用してホストコンピューティングネットワークエンドポイントを削除する方法を示します。

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value
    HRESULT hr = HcnDeleteEndpoint(endpointGuid, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


### <a name="modify-and-endpoint"></a>変更とエンドポイント

このサンプルでは、ホストコンピューティングネットワークサービス API を使用してホストコンピューティングネットワークエンドポイントを変更する方法を示します。

```C++
    unique_hcn_endpoint hcnendpoint;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value
    
    HRESULT hr = HcnOpenEndpoint(endpointGuid, &hcnendpoint, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    std::wstring  ModifySettingAddPortJson = LR"(
    {
        "ResourceType" : 0,
        "RequestType" : 0,
        "Settings" : {
            "PortName" : "acbd341a-ec08-44c0-9d5e-61af0ee86902"
            "VirtualNicName" : "641313e1-7ae8-4ddb-94e5-3215f3a0b218--87fdcf16-d210-426e-959d-2a1d4f41d6d1"
            "VirtualMachineId" : "641313e1-7ae8-4ddb-94e5-3215f3a0b218"
        }
    }
    )";


    hr = HcnModifyEndpoint(hcnendpoint.get(), ModifySettingAddPortJson.c_str(), &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


### <a name="enumerate-all-enpoints"></a>すべての enpoints を列挙する

このサンプルでは、ホストコンピューティングネットワークサービス API を使用して、すべてのホストコンピューティングネットワークエンドポイントを列挙する方法を示します。

```C++
    wil::unique_cotaskmem_string errorRecord;

    wil::unique_cotaskmem_string resultEndpoints;
    wil::unique_cotaskmem_string errorRecord;

    // Filter to select Endpoint based on properties
    std::wstring filter [] = LR"(
    { 
        "Name"  : "sampleNetwork",
    })";
    result = HcnEnumerateEndpoints(filter.c_str(), &resultEndpoints, &errorRecord);
    if (FAILED(result))
    {
        THROW_HR(result);
    }
```


### <a name="query-endpoint-properties"></a>クエリエンドポイントのプロパティ

このサンプルでは、ホストコンピューティングネットワークサービス API を使用して、ホストコンピューティングネットワークエンドポイントのすべてのプロパティを照会する方法を示します。

```C++
    unique_hcn_endpoint hcnendpoint;
    wil::unique_cotaskmem_string errorRecord;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value

    HRESULT hr = HcnOpenEndpoint(endpointGuid, &hcnendpoint, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }



    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    { 
        // Future
    })";

    hr = HcnQueryEndpointProperties(hcnendpoint.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the errorRecord Json
        THROW_HR(hr);
    }
```


## <a name="scenario-hcn-namespace"></a>シナリオ: HCN 名前空間

### <a name="create-an-hcn-namespace"></a>HCN 名前空間を作成する

このサンプルでは、ホストコンピューティングネットワークサービス API を使用して、エンドポイントとコンテナーを接続するために使用できるホストコンピューティングネットワーク名前空間をホストに作成する方法を示します。

```C++
using unique_hcn_namespace = wil::unique_any< 
    HCN_NAMESPACE, 
    decltype(&HcnCloseNamespace), 
    HcnCloseNamespace>; 

/// Creates a simple HCN Network, waiting synchronously to finish the task
void CreateHcnNamespace() 
{

    unique_hcn_namespace handle;
    wil::unique_cotaskmem_string errorRecord;
    std::wstring settings = LR"( 
    { 
        "SchemaVersion": { 
            "Major": 2, 
            "Minor": 0 
        }, 
        "Owner" : "Sample", 
        "Flags" : 0,
        "Type" : 0,
    })";    
   
    GUID namespaceGuid;  
    HRESULT result = CoCreateGuid(&namespaceGuid);

    result = HcnCreateNamespace(
        namespaceGuid,              // Unique ID 
        settings.c_str(),      // Compute system settings document 
        &handle,
        &errorRecord
        );
    if (FAILED(result)) 
    { 
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //    "ErrorCode" : <uint32>,
        //    "Error" : <string>,
        //    "Success" : <bool>,
       //   }

        // Failed to create network
        THROW_HR(result); 
    } 

    result = HcnCloseNamespace(handle.get());

    if (FAILED(result))
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }
         
}
```


### <a name="delete-an-hcn-namespace"></a>HCN 名前空間の削除

このサンプルでは、ホストコンピューティングネットワークサービス API を使用してホストコンピューティングネットワークの名前空間を削除する方法を示します。

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnDeleteNamespace(namespaceGuid, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }

```


### <a name="modify-an-hcn-namespace"></a>HCN 名前空間を変更する

このサンプルでは、ホストコンピューティングネットワークサービス API を使用してホストコンピューティングネットワークの名前空間を変更する方法を示します。

```C++
    unique_hcn_namespace handle;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnOpenNamespace(namespaceGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

    wil::unique_cotaskmem_string errorRecord;
    static std::wstring  ModifySettingAddEndpointJson = LR"(
    {
        "ResourceType" : 1,
        "ResourceType" : 0,
        "Settings" : {
            "EndpointId" : "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        }
    }
    )";

    
    hr = HcnModifyNamespace(handle.get(), ModifySettingAddEndpointJson.c_str(), &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
    hr = HcnCloseNamespace(handle.get());

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
    
```


### <a name="enumerate-all-namespaces"></a>すべての名前空間の列挙

このサンプルでは、ホストコンピューティングネットワークサービス API を使用して、すべてのホストコンピューティングネットワーク名前空間を列挙する方法を示します。

```C++
    wil::unique_cotaskmem_string resultNamespaces;
    wil::unique_cotaskmem_string errorRecord;

    std::wstring filter [] = LR"(
    { 
            // Future       
    })";
    HRESULT hr = HcnEnumerateNamespace(filter.c_str(), &resultNamespaces, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

```


### <a name="query-namespace-properties"></a>クエリの名前空間のプロパティ

このサンプルでは、ホストコンピューティングネットワークサービス API を使用してホストコンピューティングネットワークの名前空間プロパティを照会する方法を示します。

```C++
    unique_hcn_namespace handle;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnOpenNamespace(namespaceGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    { 
        // Future
    })";

    HRESULT hr = HcnQueryNamespaceProperties(handle.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

```


## <a name="scenario-hcn-load-balancer"></a>シナリオ: HCN ロードバランサー

### <a name="create-an-hcn-load-balancer"></a>HCN ロードバランサーを作成する

このサンプルでは、ホストコンピューティングネットワークサービス API を使用して、コンピューティング間でエンドポイントを負荷分散するために使用できるホストコンピューティングネットワーク Load Balancer をホスト上に作成する方法を示します。

```C++
using unique_hcn_loadbalancer = wil::unique_any< 
    HCN_LOADBALANCER, 
    decltype(&HcnCloseLoadBalancer), 
    HcnCloseLoadBalancer>; 

/// Creates a simple HCN LoadBalancer, waiting synchronously to finish the task
void CreateHcnLoadBalancer() 
{

    unique_hcn_loadbalancer handle;
    wil::unique_cotaskmem_string errorRecord;
    std::wstring settings = LR"( 
     { 
        "SchemaVersion": { 
            "Major": 2, 
            "Minor": 0 
        }, 
        "Owner" : "Sample", 
        "HostComputeEndpoints" : [
            "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        ],
        "VirtualIPs" : [ "10.0.0.10" ],
        "PortMappings" : [
            {
                "Protocol" : 0,
                "InternalPort" : 8080,
                "ExternalPort" : 80,
            }
        ],
        "EnableDirectServerReturn" : true,
        "InternalLoadBalancer" : false,
    }
     )";    
   
    GUID lbGuid;  
    HRESULT result = CoCreateGuid(&lbGuid);


    HRESULT hr = HcnCreateLoadBalancer(
        lbGuid,              // Unique ID 
        settings.c_str(),      // LoadBalancer settings document 
        &handle,
        &errorRecord
        );
    if (FAILED(hr)) 
    { 
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //    "ErrorCode" : <uint32>,
        //    "Error" : <string>,
        //    "Success" : <bool>,
       //   }

        // Failed to create network
        THROW_HR(hr); 
    }

    hr = HcnCloseLoadBalancer(handle.get());

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
          
}
```


### <a name="delete-an-hcn-load-balancer"></a>HCN ロードバランサーの削除

このサンプルでは、ホストコンピューティングネットワークサービス API を使用してホストコンピューティングネットワーク LoadBalancer を削除する方法を示します。

```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value
    HRESULT hr = HcnDeleteLoadBalancer(lbGuid , &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
```


### <a name="modify-an-hcn-load-balancer"></a>HCN ロードバランサーを変更する

このサンプルでは、ホストコンピューティングネットワークサービス API を使用してホストコンピューティングネットワークの名前空間を変更する方法を示します。

```C++
    unique_hcn_loadbalancer handle;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value

    HRESULT hr = HcnOpenLoadBalancer(lbGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }

    wil::unique_cotaskmem_string errorRecord;
    static std::wstring  ModifySettingAddEndpointJson = LR"(
    {
        "ResourceType" : 1,
        "ResourceType" : 0,
        "Settings" : {
            "EndpointId" : "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        }
    }
    )";

    
    hr = HcnModifyLoadBalancer(handle.get(), ModifySettingAddEndpointJson.c_str(), &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
    hr = HcnCloseLoadBalancer(handle.get());

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


### <a name="enumerate-all-load-balancers"></a>すべてのロードバランサーを列挙する

このサンプルでは、ホストコンピューティングネットワークサービス API を使用して、すべてのホストコンピューティングネットワーク Load Balancer を列挙する方法を示します。

```C++
    wil::unique_cotaskmem_string resultLoadBalancers;
    wil::unique_cotaskmem_string errorRecord;

    std::wstring filter [] = LR"(
    { 
         // Future

    })";
    HRESULT result = HcnEnumerateLoadBalancers(filter.c_str(), & resultLoadbalancers, &errorRecord);
    if (FAILED(result))
    {
            // UnMarshal  the result Json

            THROW_HR(result);
    }
```


### <a name="query-load-balancer-properties"></a>ロードバランサーのプロパティのクエリ

このサンプルでは、ホストコンピューティングネットワークサービス API を使用してホストコンピューティングネットワーク LoadBalancer のプロパティを照会する方法を示します。

```C++
    unique_hcn_loadbalancer handle;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value

    HRESULT hr = HcnOpenLoadBalancer(lbGuid, &handle, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }


    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    { 
        "ID"  : "",
        "Type" : 0,
    })";

    hr = HcnQueryNProperties(handle.get(), query.c_str(), &properties, &errorRecord);

    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```


## <a name="scenario-hcn-notifications"></a>シナリオ: HCN 通知

### <a name="register-and-unregister-service-wide-notifications"></a>サービス全体の通知の登録と登録解除

このサンプルでは、ホストコンピューティングネットワークサービス API を使用して、サービス全体の通知の登録と登録解除を行う方法を示します。 これにより、新しいネットワーク作成イベントなどのサービス全体の操作が発生したときに、呼び出し元は (登録時に指定されたコールバック関数を使用して) 通知を受け取ることができます。

```C++
using unique_hcn_callback = wil::unique_any< 
    HCN_CALLBACK, 
    decltype(&HcnUnregisterServiceCallback), 
    HcnUnregisterServiceCallback>; 

// Callback handle returned by registration api. Kept at 
// global or module scope as it will automatically be
// unregistered when it goes out of scope.
unique_hcn_callback g_Callback;

// Event notification callback function.
void
CALLBACK
ServiceCallback(
    DWORD   NotificationType,
    void*   Context,
    HRESULT NotificationStatus,
    PCWSTR  NotificationData)
{
    // Optional client context
    UNREFERENCED_PARAMETER(context);
    // Reserved for future use
    UNREFERENCED_PARAMETER(NotificationStatus);

    switch (NotificationType)
    {
        case HcnNotificationNetworkCreate:
            // TODO: UnMarshal the NotificationData
            //
            // // Notification
            // {
            //     "ID" : Guid,
            //     "Flags" : <uint32>,
            // };
            break;

        case HcnNotificationNetworkDelete:
            // TODO: UnMarshal the NotificationData
            break;

        Default:
            // TODO: handle other events.
            break;
    }
}

/// Register for service-wide notifications
void RegisterForServiceNotifications() 
{
    THROW_IF_FAILED(HcnRegisterServiceCallback(
        ServiceCallback,
        nullptr,
        &g_Callback));        
}

/// Unregister from service-wide notifications
void UnregisterForServiceNotifications()
{
    // As this is a unique_hcn_callback, this will cause HcnUnregisterServiceCallback to be invoked
    g_Callback.reset();

}
```

## <a name="next-steps"></a>次のステップ:

- [HCN の RPC コンテキストハンドル](hcn-declaration-handles.md)の詳細については、こちらを参照してください。

- [Hcn JSON ドキュメントスキーマ](hcn-json-document-schemas.md)の詳細については、こちらを参照してください。