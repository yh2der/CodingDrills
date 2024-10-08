# Built-In Sort
std::sort 的實現主要基於 Introsort，這是一種混合排序算法，它結合了 快速排序（Quicksort）、堆排序（Heapsort）和 插入排序（Insertion Sort）的特性。這樣的設計目的是在大多數情況下獲得最佳的性能，並在特定情況下避免最壞情況的性能瓶頸。

## Introsort 的原理
- 快速排序（Quicksort）:
    - 基本思想: 通過選擇一個「基準」元素，將數據分為兩個子集合，左邊的子集合元素都比基準小，右邊的子集合元素都比基準大。然後對這兩個子集合分別進行排序。
    - 優點: 平均情況下性能很好，時間複雜度為 O(n log n)。
    - 最壞情況: 當數據幾乎已經排序時，快速排序的時間複雜度會降到 O(n^2)。

- 堆排序（Heapsort）:
    - 基本思想: 將數據轉換為最大堆或最小堆，然後從堆中逐個提取最大或最小元素，構建排序後的數據。
    - 優點: 可以保證 O(n log n) 的最壞情況性能，不像快速排序那樣有最壞情況的性能問題。
    - 缺點: 在實際應用中通常比快速排序慢一些，因為其常數因子較大。

- 插入排序（Insertion Sort）:
    - 基本思想: 通過將每個元素插入到已經排序的部分中，逐步建立排序。
    - 優點: 對於小型數據集或部分已經排序的數據表現良好，時間複雜度為 O(n^2)。
    - 缺點: 對於大型數據集效率較低。

## Introsort 的工作流程
- 使用快速排序進行排序：當數據集較大時，std::sort 使用快速排序來進行排序，這樣可以獲得 O(n log n) 的平均性能。

- 切換到堆排序：當遞歸深度超過某個預定的限制時，std::sort 會切換到堆排序。這是為了避免快速排序在最壞情況下的 O(n^2) 複雜度。

- 使用插入排序：當處理非常小的數據集時，std::sort 會使用插入排序，這樣能夠提高小數據集的排序效率。