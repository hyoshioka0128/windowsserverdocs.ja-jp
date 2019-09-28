---
title: Verbose コマンド
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fcf30ae7-818f-4e7e-a083-a1812682032b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c7ecc2bb3578b578060694c95833fd32674db10
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369913"
---
# <a name="the-verbose-command"></a>Verbose コマンド



指定したコマンドの詳細な出力が表示されます。 使用することができます **/verbose** を実行するその他の WDSUTIL コマンドを使用します。 指定する必要があります **/verbose** と **]、[進行状況の** 直後後 **WDSUTIL**します。

## <a name="syntax"></a>構文

```
WDSUTIL /verbose <commands>
```

## <a name="examples"></a>使用例

自動追加データベースから承認済みのコンピュータを削除し、詳細な出力を表示する、次のように入力します。
```
WDSUTIL /Verbose /progress /Delete-AutoAddDevices /Server:MyWDSServer /DeviceType:ApprovedDevices
```