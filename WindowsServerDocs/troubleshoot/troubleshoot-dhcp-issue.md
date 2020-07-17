---
title: 動的ホスト構成プロトコル (DHCP) のトラブルシューティングガイド
description: この artilce には、DHCP の問題に関するトラブルシューティングガイドが導入されています。
ms.prod: windows-server
ms.service: na
manager: dcscontentpm
ms.technology: server-general
ms.date: 5/26/2020
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 4bded9f879061903b1e925632a3cb4c83dfaac08
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150320"
---
# <a name="troubleshooting-guide-for-dynamic-host-configuration-protocol-dhcp"></a>動的ホスト構成プロトコル (DHCP) のトラブルシューティングガイド

任意のデバイス (コンピューターや電話など) がネットワークで動作できるようにするには、そのデバイスに IP アドレスを割り当てる必要があります。 手動または自動で IP アドレスを割り当てることができます。 自動割り当ては、DHCP サービス (Microsoft またはサードパーティサーバー) によって処理されます。

この記事では、Microsoft IPv4 DHCP クライアントとサーバーの一般的なトラブルシューティング手順について説明します。

## <a name="more-information"></a>詳細情報

IPv4 アドレス割り当ての手順には、通常、次の3つの主要なコンポーネントが含まれます。

- IP アドレスを取得する必要がある DHCP クライアントデバイス

- 特定の設定に基づいてクライアントに IP アドレスを提供する DHCP サービス

- Dhcp リレーエージェント/IP ヘルパー。 DHCP ブロードキャスト要求を別のネットワークセグメントに送信します。

DHCP クライアントとサーバー間の通信は、次の2つのピア間の3種類の相互作用で構成されます。

- **ブロードキャストベースの DORA** (検出、オファー、要求、確認)。 このプロセスは次のステップで構成されます:
  
    - DHCP クライアントは、範囲内の使用可能なすべての DHCP サーバーに DHCP 検出ブロードキャスト要求を送信します。
  
    - Dhcp Offer のブロードキャスト応答が DHCP サーバーから受信され、使用可能な IP アドレスリースが提供されます。
  
    - DHCP クライアントのブロードキャスト要求では、提供された IP アドレスリースと DHCP ブロードキャストの受信確認が最後に要求されます。
  
    - DHCP クライアントとサーバーが別々の論理ネットワークセグメントに配置されている場合、DHCP リレーエージェントはフォワーダーに対して動作し、ピア間での DHCP ブロードキャストパケットの送受信を行います。

- **ユニキャスト Dhcp 更新要求**: dhcp クライアントから dhcp サーバーに直接送信され、ip アドレスリース時間の50% 後に ip アドレスの割り当てが更新されます。

- **Dhcp ブロードキャスト要求**の再バインド: クライアントの範囲内の任意の dhcp サーバーに対して行われます。 この値は、IP アドレスリース期間の87.5% 後に送信されます。これは、ダイレクトユニキャスト要求が機能しなかったことを示しているためです。 DORA プロセスと同様に、このプロセスには、DHCP リレーエージェント通信が含まれます。

Microsoft DHCP クライアントが有効な DHCP IPv4 アドレスを受信しない場合、クライアントは APIPA アドレスを使用するように構成されている可能性があります。 詳細については、次のサポート技術情報の記事を参照してください。  
[220874](https://support.microsoft.com/help/220874) DHCP サーバーなしで tcp/ip の自動アドレス指定を使用する方法

すべての通信は、UDP ポート67および68で行われます。 詳細については、次のサポート技術情報の記事を参照してください。  
[169289](https://support.microsoft.com/help/169289) DHCP (動的ホスト構成プロトコル) の基本。