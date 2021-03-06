---
title: '&lt;memory_resource&gt;'
ms.date: 04/04/2019
f1_keywords:
- <memory_resource>
helpviewer_keywords:
- memory_resource header
ms.openlocfilehash: de88feb691d0ec1bc9bf9b9dc2bc40cbc31a1cfe
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88831048"
---
# <a name="ltmemory_resourcegt"></a>&lt;memory_resource&gt;

コンテナークラステンプレート memory_resource とそのサポートテンプレートを定義します。

## <a name="syntax"></a>構文

```cpp
#include <memory_resource>
```

## <a name="members"></a>メンバー

### <a name="operators"></a>演算子

|名前|説明|
|-|-|
|[operator! =](../standard-library/memory-resource-operators.md#op_neq)|演算子の左側の memory_resource オブジェクトが右側の memory_resource オブジェクトと等しくないかどうかを調べます。|
|[operator = =](../standard-library/memory-resource-operators.md#op_eq_eq)|演算子の左側の memory_resource オブジェクトが右側の memory_resource オブジェクトと等しいかどうかを調べます。|

### <a name="specialized-template-functions"></a>特殊テンプレート関数

|名前|説明|
|-|-|
|[polymorphic_allocator](../standard-library/memory-resource-functions.md#poly_alloc)||

### <a name="functions"></a>Functions

|名前|説明|
|-|-|
|[get_default_resource](../standard-library/memory-resource-functions.md#get_default)||
|[new_delete_resource](../standard-library/memory-resource-functions.md#new_delete)||
|[null_memory_resource](../standard-library/memory-resource-functions.md#null_memory)||
|[set_default_resource](../standard-library/memory-resource-functions.md#set_default)||

### <a name="classes-and-structs"></a>クラスと構造体

|名前|説明|
|-|-|
|[memory_resource クラス](../standard-library/memory-resource-class.md)||
|[monotonic_buffer_resource クラス](../standard-library/monotonic-buffer-resource-class.md)||
|[pool_options 構造体](../standard-library/pool-options-structure.md)||
|[synchronized_pool_resource クラス](../standard-library/synchronized-pool-resource-class.md)||
|[unsynchronized_pool_resource クラス](../standard-library/unsynchronized-pool-resource-class.md)||

## <a name="see-also"></a>関連項目

[ヘッダーファイルのリファレンス](../standard-library/cpp-standard-library-header-files.md)\
[C++ 標準ライブラリのスレッドセーフ](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[C++ 標準ライブラリリファレンス](../standard-library/cpp-standard-library-reference.md)
