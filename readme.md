### Usage
1. create a table: `Table *display_table;`
- give it a release function pointer if needed:
    ```c
    void release_display(void *display) {
        Display *dis = (Display *)display;
        CFRelease(dis->uuid);
    }

    display_table->release = &release_display;
    ```

2. insert the table to a bucket, passing the table, the struct value to be used as table key, and the struct to store
    ```c
    table_insert(display_table, display->did, (void *)display);
    ```

3. `table_free(display_table);` to clear it

4. To get items, create a get function for whatever struct you add, taking the field you set to be the table key
    ```c
    Display *get_display(int did) {
        Display *display;
        display = (Display *)table_search(display_table, did);
        return display;
    }```

5. to delete items, create a delete function for your struct that calls `table_delete_item(Table *table, int key)` with the table and key
    ```c
    void remove_process(ProcessSerialNumber psn) {
        table_delete_item(proc_table, psn.lowLongOfPSN);
    }
    ```

See [source/display.c](https://github.com/a-soll/mac_window/blob/master/source/display.c) from [mac-window](https://github.com/a-soll/mac_window) for more indepth usage examples
