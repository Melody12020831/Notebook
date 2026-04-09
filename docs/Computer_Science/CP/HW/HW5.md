---
statistics: True
comments: true
---

# HW5

## 5.1 (a, b)

???+ question
    Improve the hash table implementation of Program 5.2:

    a. Double the size of the array when the average bucket length grows larger than 2 (so table is now a pointer to a dynamically allocated array). To double an array, allocate a bigger one and rehash the contents of the old array; then discard the old array.

    b. Allow for more than one table to be in use by making the table a parameter to insert and lookup.

    ```c
    struct bucket {string key; void *binding; struct bucket *next;};
    #define SIZE 109
    struct bucket *table[SIZE];

    unsigned int hash(char *s0){
        unsigned int h=0; char *s;
        for(s=s0; *s; s++)
        h = h*65599 + *s;
        return h;
    }

    struct bucket *Bucket(string key, void *binding, struct bucket *next) {
        struct bucket *b = checked_malloc(sizeof(*b));
        b->key=key; b->binding=binding; b->next=next;
        return b;
    }

    void insert(string key, void *binding) {
        int index = hash(key) % SIZE;
        table[index] = Bucket(key, binding, table[index]);
    }

    void *lookup(string key) {
        int index = hash(key) % SIZE;
        struct bucket *b;
        for(b=table[index]; b; b=b->next)
        if (0==strcmp(b->key,key)) return b->binding;
        return NULL;
    }

    void pop(string key) {
        int index = hash(key) % SIZE;
        table[index] = table[index]->next;
    }
    ```

??? note "answer"
    a.

    ```c
    #include <stdlib.h>
    #include <string.h>

    typedef char* string;
    struct bucket {string key; void *binding; struct bucket *next;};

    // 初始大小和元素计数
    int current_size = 109;
    int element_count = 0;

    // 改为双重指针，用于动态分配
    struct bucket **table = NULL;

    unsigned int hash(char *s0) {
        unsigned int h = 0; char *s;
        for(s=s0; *s; s++)
            h = h*65599 + *s;
        return h;
    }

    // 安全的内存分配函数
    void *checked_malloc(size_t size) {
        void *p = malloc(size);
        if (!p) exit(1);
        return p;
    }

    struct bucket *Bucket(string key, void *binding, struct bucket *next) {
        struct bucket *b = checked_malloc(sizeof(*b));
        b->key = key; b->binding = binding; b->next = next;
        return b;
    }

    // 初始化哈希表
    void init_table() {
        table = checked_malloc(current_size * sizeof(struct bucket *));
        for(int i = 0; i < current_size; i++) {
            table[i] = NULL;
        }
    }

    // 扩容
    void rehash() {
        // 保存旧表信息
        int old_size = current_size;
        struct bucket **old_table = table;
        
        // 创建新表
        current_size = old_size * 2;
        table = checked_malloc(current_size * sizeof(struct bucket *));
        for(int i = 0; i < current_size; i++) {
            table[i] = NULL;
        }
        
        // 将旧表数据迁移至新表
        for(int i = 0; i < old_size; i++) {
            struct bucket *b = old_table[i];
            while(b != NULL) {
                // 暂存下一个节点
                struct bucket *next_b = b->next;

                // 重新计算索引
                int new_index = hash(b->key) % current_size; 
                
                // 插入新表的头部
                b->next = table[new_index];
                table[new_index] = b;
                
                b = next_b;
            }
        }

        free(old_table);
    }

    void insert(string key, void *binding) {
        if (table == NULL) init_table();
        
        int index = hash(key) % current_size;
        table[index] = Bucket(key, binding, table[index]);
        element_count++;
        
        // 如果平均桶长度大于 2 就要扩容
        if (element_count > 2 * current_size) {
            rehash();
        }
    }

    void *lookup(string key) {
        if (table == NULL) return NULL;
        int index = hash(key) % current_size;
        struct bucket *b;
        for(b = table[index]; b; b = b->next)
            if (0 == strcmp(b->key, key)) return b->binding;
        return NULL;
    }

    void pop(string key) {
        if (table == NULL) return;
        int index = hash(key) % current_size;
        
        // 维护 element_count
        struct bucket *b = table[index];
        struct bucket *prev = NULL;
        
        while(b != NULL) {
            if (0 == strcmp(b->key, key)) {
                if (prev == NULL) {
                    table[index] = b->next;
                } else {
                    prev->next = b->next;
                }
                free(b);
                element_count--;
                return;
            }
            prev = b;
            b = b->next;
        }
    }
    ```

    b.

    ```c
    #include <stdlib.h>
    #include <string.h>

    typedef char* string;
    struct bucket {string key; void *binding; struct bucket *next;};

    #define SIZE 109

    // 将哈希表抽象为结构体，允许实例化多个对象
    struct HashTable {
        struct bucket *buckets[SIZE];
    };

    unsigned int hash(char *s0) {
        unsigned int h = 0; char *s;
        for(s=s0; *s; s++)
            h = h*65599 + *s;
        return h;
    }

    void *checked_malloc(size_t size) {
        void *p = malloc(size);
        if (!p) exit(1);
        return p;
    }

    struct bucket *Bucket(string key, void *binding, struct bucket *next) {
        struct bucket *b = checked_malloc(sizeof(*b));
        b->key = key; b->binding = binding; b->next = next;
        return b;
    }

    // 哈希表构造函数
    struct HashTable* create_table() {
        struct HashTable *ht = checked_malloc(sizeof(struct HashTable));
        for(int i = 0; i < SIZE; i++) {
            ht->buckets[i] = NULL;
        }
        return ht;
    }

    // 将表作为参数传入 insert 中
    void insert(struct HashTable *ht, string key, void *binding) {
        if (ht == NULL) return;
        int index = hash(key) % SIZE;
        ht->buckets[index] = Bucket(key, binding, ht->buckets[index]);
    }

    // 将表作为参数传入 lookup 中
    void *lookup(struct HashTable *ht, string key) {
        if (ht == NULL) return NULL;
        int index = hash(key) % SIZE;
        struct bucket *b;
        for(b = ht->buckets[index]; b; b = b->next)
            if (0 == strcmp(b->key, key)) return b->binding;
        return NULL;
    }

    // 将表作为参数传入 pop 中
    void pop(struct HashTable *ht, string key) {
        if (ht == NULL) return;
        int index = hash(key) % SIZE;
        
        struct bucket *b = ht->buckets[index];
        struct bucket *prev = NULL;
        
        while(b != NULL) {
            if (0 == strcmp(b->key, key)) {
                if (prev == NULL) {
                    ht->buckets[index] = b->next;
                } else {
                    prev->next = b->next;
                }
                free(b);
                return;
            }
            prev = b;
            b = b->next;
        }
    }
    ```