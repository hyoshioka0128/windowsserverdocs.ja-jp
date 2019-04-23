---
author: shortpatti
ms.author: pashort
ms.date: 10/02/2018
ms.prod: windows-server-threshold
ms:topic: include
ms.openlocfilehash: d1bfc74c4daa751e3081b26c87dd0d2c88f5f095
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879853"
---
スタンバイ アダプターのオプションは、**なし (すべてのアダプター アクティブ)** またはスタンバイ アダプターとして機能する NIC チーム内の特定のネットワーク アダプターのどれを選択します。 スタンバイ アダプターと NIC を構成するときに他のすべての選択されていないチーム メンバーはアクティブとのネットワーク トラフィックに送信またはアクティブな NIC が失敗するまでに、アダプターで処理します。 アクティブな NIC を失敗すると、スタンバイの NIC がアクティブになり、プロセスのネットワーク トラフィック。 すべてのチーム メンバーは、サービスに復元を取得、スタンバイのチーム メンバーは、スタンバイ状態に戻ります。  