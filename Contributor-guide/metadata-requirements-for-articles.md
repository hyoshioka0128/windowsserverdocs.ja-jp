---
title: Windows Server 関連の記事に必要なメタデータタグを追加する
description: Windows Server 関連の記事の上部にメタデータタグとして追加する必要がある情報の一覧。 必要なタグは、レポートとチームの両方の要件に基づいて変更される可能性があります。
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: f0af6b48cd3fd28ae0a15752cb21bfe9a4abf14f
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865091"
---
# <a name="add-the-required-metadata-tags-to-your-windows-server-related-article"></a>Windows Server 関連の記事に必要なメタデータタグを追加する

各記事の上部には、追跡と SEO の目的で特定のメタデータが含まれている必要があります。 必要なタグは、レポートの要件に基づいて変更される可能性があります。 ただし、フィールドを追加または削除する必要がある場合は通知されます。

次のようになります。上部と下部にある3つのハイフン (---) を含みます。

```markdown

---
title: The title of the article should go here. This is used in SEO and search results.

description: A description for the article should go here. This is used in search results, to provide users with information about whether the article has the information they're looking for.

ms.prod: Use this specific text, windows-server-threshold

ms.reviewer: The Microsoft alias for the primary PM for the feature/functionality

author: Your GitHub alias

ms.author: Your Microsoft alias

manager: Your manager's Microsoft alias

ms.topic: Type of article, including article, landing-page, get-started-article, or reference

ms.date: Date of change (MM/DD/YYYY)

---

```

## <a name="example"></a>例

```markdown

---
title: What is Windows Admin Center?
description: Learn about the Windows Admin Center, a locally-deployed, browser-based management tool set that lets you manage your Windows Servers with no Azure or cloud dependency.
ms.prod: windows-server-threshold
ms.reviewer: alainch
author: danielle-github
ms.author: danielle
manager: alainch
ms.topic: article
ms.date: 07/06/2019
---

```