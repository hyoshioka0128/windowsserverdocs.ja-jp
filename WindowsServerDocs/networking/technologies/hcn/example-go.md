---
title: 最上位レベル IPAM & サブネット オブジェクト生成の Go コードの例
description: ''
ms.author: jmesser
author: jmesser81
ms.date: 11/05/2018
ms.openlocfilehash: 428566411920e55d444890898d0f02a1e6cc81ca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870943"
---
# <a name="example-of-go-generated-code"></a>Go で生成されたコードの例 

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

```Go
/*
 * HCN API
 *
 * No description provided (generated by Swagger Codegen https://github.com/swagger-api/swagger-codegen)
 *
 * API version: 2.1
 * Generated by: Swagger Codegen (https://github.com/swagger-api/swagger-codegen.git)
 */

package swagger

type Ipam struct {

    //  Type : dhcp
    Type_ string `json:"Type,omitempty"`

    Subnets []Subnet `json:"Subnets,omitempty"`
}

/*
 * HCN API
 *
 * No description provided (generated by Swagger Codegen https://github.com/swagger-api/swagger-codegen)
 *
 * API version: 2.1
 * Generated by: Swagger Codegen (https://github.com/swagger-api/swagger-codegen.git)
 */

package swagger

type Subnet struct {

    ID string `json:"ID,omitempty"`

    IpAddressPrefix string `json:"IpAddressPrefix,omitempty"`

    Policies []SubnetPolicy `json:"Policies,omitempty"`

    Routes []Route `json:"Routes,omitempty"`
}

```