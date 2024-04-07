#redis #output #permanent 

redis 是一個key-value資料庫，key一般是string類型，value類型有多種樣式


| 基本類型  |                           |
|:--------- | ------------------------- |
| String    | hello world               |
| Hash      | {name:"Jack",age:17}      |
| List      | { a → b → c → c }         |
| Set       | { a, b, c }               |
| SortedSet | { a : 1 , b : 2 , c : 3 } |

| 特殊類型     |                     |
| -------- | ------------------- |
| GEO地理坐標  | { a: (120.4,30.5) } |
| BitMap   | 0100001110110       |
| HyperLog | 011010011001        |
