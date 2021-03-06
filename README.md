# gosort

## Package sort
- Sortできるstructの条件  
→ 下記Intergaceを実装していること
```
type Interface interface {
    // Len is the number of elements in the collection.
    Len() int
    // Less reports whether the element with
    // index i should sort before the element with index j.
    Less(i, j int) bool
    // Swap swaps the elements with indexes i and j.
    Swap(i, j int)
}
```

- sort.Search(n int, f func(int) booli int
  - f()がtrue になる最初のindexを返却する
  - 一致を探すことも、ある数値以上の値を探すことも可能
  - 配列は、ソートしておく必要がある

- sort.Slice(slice interface{}, less func(i, j int) bool)
  - less関数で定義された順にソートされる(go1.8.1以上)
  - sort.Interfaceを実装していなくてもソートが可能となっている
  - stable sortを保証していない
    - sort.SliceStableを利用することで保証される

- sort.Sort(data sort.Interface) は渡されるデータによってソートの種別変える
  - ヒープソート
    - 条件: log(n+1)の整数値の2乗よりも深い場合
      - 右に1ビットずつシフト演算して0になるまでの回数の2乗が最大の深さ
      - この値が0となったときに、ヒープソートに切り替わる
    ```go
    // Switch to heapsort if depth of 2*ceil(lg(n+1)) is reached.
    ```
  - シェルソート
    - 条件: スライスが12より短い場合
    ```go
    // Use ShellSort for slices <= 12 elements
    ```
  - クイックソート
    - 条件: 上記条件に当てはまらない場合