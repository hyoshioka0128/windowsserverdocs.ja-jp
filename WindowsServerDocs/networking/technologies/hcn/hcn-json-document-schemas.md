---
title: ホストコンピューティングネットワーク (HCN) JSON ドキュメントスキーマ
description: ''
ms.author: jmesser
author: jmesser81
ms.date: 11/05/2018
ms.openlocfilehash: b8676fbab1776144cbbe68604f56d1230a04a145
ms.sourcegitcommit: 213989f29cc0c30a39a78573bd4396128a59e729
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70031539"
---
# <a name="hcn-json-document-schemas"></a>HCN JSON ドキュメントのスキーマ

>適用対象:Windows Server (半期チャネル)、Windows Server 2019

## <a name="hcn-schema"></a>HCN スキーマ

```json
// Network
{
    "Id" : <string>,
    "Owner" : <string>,
    "SchemaVersion" : {
        "Major" : <uint32>,
        "Minor" : <uint32>
    },
    "Flags" : <enum bit mask>, 
         // AsString; Values: 
         // "None" (0),
         // "EnableDnsProxy" (1),
         // "EnableDhcpServer" (2),
         // "IsolateVSwitch" (8)
    "Type"  : <enum>, 
         // AsString; Values: 
         // "NAT" (0), 
         // "ICS" (1), 
         // "Transparent" (2)
    "Ipams" : [ {
         "Type" : <enum>, 
             // AsString; Values: 
             // "Static" (0), 
             // "Dhcp" (1)
         "Subnets" : [ {
                "IpAddressPrefix" : <ip prefix in CIDR>,
                "Policies" : [ {
                        "Type" : <enum>, 
                            // AsString; Values: 
                            // "VLAN" (0)
                        "Data" : <any>
                 } ],
                "Routes" : [ {
                       "NextHop" : <ip address of the next hop gateway>,
                       "DestinationPrefix" : <ip prefix in cidr>,
                       "Metric" : <route metric in uint8>,
                 } ],
          } ],
     } ],
    "Policies" : [{
         "Type" : <enum>, 
              // AsString; Values: 
              // "NetAdapterName" (1), 
              // "InterfaceConstraint" (2)
         "Data" : <any>
    }],
    "Dns" : {
        "Suffix" : <local connection specific suffix>,
        "Search" : [<list of additional suffixes>],
        "ServerList" : [<string>],
        "Options" : [<string>],
    },
    "MacPool" : {
        "Ranges" : [ {
              "StartMacAddress" : <string>,
              "EndMacAddress" : <string>
         } ],
    },
}
```

## <a name="hcn-endpoint-schema"></a>HCN エンドポイントスキーマ

```json
// Endpoint 
{
    "Id" : <string>,
    "Owner" : <string>,
    "SchemaVersion" : {
        "Major" : <uint32>,
        "Minor" : <uint32>
    },
    "Flags" : <enum bit mask>, 
         // AsString; Values: 
         // "None" (0),
         // "DisableInterComputeCommunication" (2)
    "HostComputeNetwork" : <string>,
    "MacAddress" : <string>,
    "Policies" : [ {
         "Type" : <enum>, 
              // AsString; Values: 
              // "PortMapping" (0), 
              // "ACL" (1)
         "Data" : <any>
    } ],
    "Dns" : {
        "Suffix" : <local connection specific suffix>,
        "Search" : [<list of additional suffixes>],
        "ServerList" : [<string>],
        "Options" : [<string>],
    },
    "IPConfigurations" : [ {
        "IPAddress" : <ip address>,
        "PrefixLength" : <prefix length uint16>,
    } ],
    "Routes" : [ {
        "NextHop" : <ip address of the next hop gateway>,
        "DestinationPrefix" : <ip prefix in cidr>,
        "Metric" : <route metric in uint8>,

    } ],
}
```

## <a name="hcn-policy-schema"></a>HCN ポリシースキーマ

```json
// VlanPolicy
{
    "Type" : "VLAN",
    "IsolationId" : <uint32>,
}

// PortMappingPolicy
{
    "Type" : "PortMapping",
    "Protocol" : <enum>,
         // AsString; Values: 
         // "Unknown" (0),
         // "ICMPv4" (1),
         // "IGMP" (2),
         // "TCP" (6),
         // "UDP" (17),
         // "ICMPv6" (58)
    "InternalPort" : <uint16>,
    "ExternalPort" : <uint16>,
}
```

## <a name="hcn-load-balancer-schema"></a>HCN ロードバランサースキーマ

```json
// Host Compute LoadBalancer
{
    "Id" : <string>,
    "Owner" : <string>,
    "SchemaVersion" : {
        "Major" : <uint32>,
        "Minor" : <uint32>
    },
    "Flags" : <enum bit mask>, 
         // AsString; Values: 
         // "None" (0),
         // "EnableDirectServerReturn" (1)
         // "EnableInternalLoadBalancer" (2)
    "HostComputeEndpoints" : [<Host compute Endpoint id>],
    "VirtualIPs" : [<Virtual IpAddress>],
    "PortMappings" : [ {
        "Type" : "PortMapping",
        "Protocol" : <enum>,
             // AsString; Values: 
             // "Unknown" (0),
             // "ICMPv4" (1),
             // "IGMP" (2),
             // "TCP" (6),
             // "UDP" (17),
             // "ICMPv6" (58)
        "InternalPort" : <uint16>,
        "ExternalPort" : <uint16>,
    } ],
    "Policies" : [ {
         "Type" : <enum>, 
              // AsString; Values: 
              // "SourceVirtualIp" (0), 
         "Data" : <any>
    } ],
}
```

## <a name="hcn-namespace-schema"></a>HCN 名前空間スキーマ

```json
// Namespace
{
    "Id" : <string>,
    "Owner" : <string>,
    "SchemaVersion" : {
        "Major" : <uint32>,
        "Minor" : <uint32>
    },
    "NamespaceId" : <uint32>,
    "NamespaceGuid" : <guid>,
    "Type"  : <enum>,
              // AsString; Values: 
              // "Host" (0), 
              // "HostDefault" (1), 
              // "Guest" (2), 
              // "GuestDefault" (3)
    "Resources" : [ {
          "Type"  : <enum>,
              // AsString; Values: 
              // "Container" (0), 
              // "Endpoint" (1)
          "Data"  : <any>
    } ],
}
```

## <a name="hcn-notification-schema"></a>HCN 通知スキーマ

```json
// Notification
{
    "ID" : Guid,
    "Flags" : <uint32>,
};
```

## <a name="result-error-schema"></a>結果のエラースキーマ

```json
// ErrorSchema
{
    "ErrorCode" : <uint32>,
    "Error" : <string>,
    "Success" : <bool>,
}
```

