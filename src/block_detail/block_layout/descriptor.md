# descriptor

Block中的`descriptor`描述符，决定了Block有哪些额外的属性和具体定义。

[Block_private.h](https://opensource.apple.com/source/libclosure/libclosure-63/Block_private.h)

中的，3种`Block_descriptor`：`Block_descriptor_1`、`Block_descriptor_2`、`Block_descriptor_3`

```c
#define BLOCK_DESCRIPTOR_1 1
struct Block_descriptor_1 {
    uintptr_t reserved;
    uintptr_t size;
};

#define BLOCK_DESCRIPTOR_2 1
struct Block_descriptor_2 {
    // requires BLOCK_HAS_COPY_DISPOSE
    void (*copy)(void *dst, const void *src);
    void (*dispose)(const void *);
};

#define BLOCK_DESCRIPTOR_3 1
struct Block_descriptor_3 {
    // requires BLOCK_HAS_SIGNATURE
    const char *signature;
    const char *layout;     // contents depend on BLOCK_HAS_EXTENDED_LAYOUT
};

struct Block_layout {
    void *isa;
    volatile int32_t flags; // contains ref count
    int32_t reserved; 
    void (*invoke)(void *, ...);
    struct Block_descriptor_1 *descriptor;
    // imported variables
};
```

合并后，就是前面[Block详细定义](http://book.crifan.org/books/ios_re_objc_block/website/block_detail/)所整理的：

```c
// merged new layout
struct Block_descriptor {
    // Block_descriptor_1
    uintptr_t reserved;
    uintptr_t size;

    // Block_descriptor_2
    // requires BLOCK_HAS_COPY_DISPOSE
    void (*copy)(void *dst, const void *src);
    void (*dispose)(const void *);

    // Block_descriptor_3
    // requires BLOCK_HAS_SIGNATURE
    const char *signature;
    const char *layout;     // contents depend on BLOCK_HAS_EXTENDED_LAYOUT
};
```

TODO：

* Block_descriptor_1、Block_descriptor_2、Block_descriptor_3
  * 【整理】iOS逆向心得：Block中Block_descriptor_1、Block_descriptor_2、Block_descriptor_3的计算逻辑和位置
