---
layout: post
title: "ArrayBuffer usage"
date: 2018-01-23 07:35:30 +0800
---
- Int8Array 类型化数组的创建

- ArrayBuffer 的创建方式：
  1. 方式一：
    ```
    var buffer = new ArrayBuffer(10); // 开辟 8 个字节的空间
    var tarr = new Int16Array(buffer);  // 创建有符号16位类型化数组，每个数占用两个字节
    * 因为 Int16 每个数字占用两个字节，所以要求 ArrayBuffer 开辟的空间必须是 2 的倍数
    ```

  2. 方式二：
    ```
    var tarr = be Int16Array(10); // 表示创建了一个包含 10 个元素的类型化数组
    console.log(tarr.length, tarr.betyLength)
    ```

  3. 方式三：
    ```
    var tarr = new Int16Array(buffer, 2); // 跳过前面两个字节
    console.log(tarr.length); // 4
    var tarr = new Int16Array(buffer, 2, 2); // 挑个前两个字节，数组长度为 2
    console.log(tarr.length)
    ```

  4. 方式四：
    ```
    var tarr = new Int16Array([12, 3, 5]); // 创建了长度为 3 的类型化数组，此时会创建对应 buffer
    console.log(tarrr.buffer.byteLength);
    console.log(tarr.length, tarr.byteLength);
    ```

  5. 方式五：
    ```
    var tarr = new Int16Array([12, 3, 5]);
    var tarr = new Int8Array(tarr); // 此时数组只是继承了 tarr 数组的数
    var console.log(tarr.length, tarr.byteLength);
    ```

- subarray
  ```
  var tarr = new Int16Array([1, 2, 3, 4, 5, 6]);
  var tarr2 = tarr.subarray(1, 3); // star, end
  console.log(tarr2);
  console.log(tarr.buffer === tarr2.buffer) // 并没有创建新的 buffer，数据底层相同
  ```
- set
  ```
   var arr = new Int8Array([1, 2, 3, 4, 5]);
   var arr2 = new Int16Array(5);
   arr2.set(arr); //拷贝了 arr 的数据，创建了新的 buffer
   console.log(arr2);

   arr2 的长度不能小于 arr 的长度，多出空间用 0 填充， set 可以设置开始填充的位置
   var arr2 = new Int8Array(8);
   arr2.set(arr, 3); 从第三个位置开始拷贝 arr。前面的数字用 0 填充
  ```
