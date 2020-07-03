---
title: verbose
description: 詳細については、指定されたコマンドの詳細な出力を表示するリファレンス記事を参照してください。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fcf30ae7-818f-4e7e-a083-a1812682032b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 079e441ba4a932e23493e7e37fbe36cab4c4971f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935242"
---
# <a name="verbose"></a>verbose

指定したコマンドの詳細な出力が表示されます。 使用することができます **/verbose** を実行するその他の WDSUTIL コマンドを使用します。 指定する必要があります **/verbose** と **]、[進行状況の** 直後後 **WDSUTIL**します。

## <a name="syntax"></a>構文

```
WDSUTIL /verbose <commands>
```

## <a name="examples"></a>例

自動追加データベースから承認済みのコンピュータを削除し、詳細な出力を表示する、次のように入力します。
```
WDSUTIL /Verbose /progress /Delete-AutoAddDevices /Server:MyWDSServer /DeviceType:ApprovedDevices
```