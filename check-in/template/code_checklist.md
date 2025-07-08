## openGauss-server仓通用代码检视checklist

供开发者和committer进行代码自检、检视时，分析代码是否存在问题

# committer通用检视checklist
 - committer应确认所有的PR修改是否涉及资料修改（不管是bugfix、代码增强还是特性）。committer应该通过实际的代码修改确认是否涉及资料修改。如涉及的，应当要求PR提出者同步提交资料PR，并同步检视资料PR的正确性，如果需要修改资料而没有提交资料PR的，不应该给lgtm。
 - 新增系统表、系统表索引、系统函数、系统视图、类型、类型转换规则等涉及升级的操作。应检查升级脚本的准确性。创建系统对象时，应通过 SET LOCAL inplace_upgrade_next_system_object_oids 设置OID，创建函数的，应检查函数的各类属性和builtin_func.ini中的是否一致，避免出现升级场景和直接安装场景对象属性不一致的问题（特别容易遗漏的属性包括procost、prorows、provolatile等属性）。
 - 修改Node类型结构体时，需同步修改 _copyXXX、_equalXXX、_readXXX、_outXXX 函数（有的可能没有，或者只有一部分接口）。如涉及 _outXXX 函数修改，应通过升级版本号进行控制，对应的 _readXXX 函数通过 IF_EXIST 宏进行判断。 _copy/_equal无需通过版本号控制。
 - 确保提交的PR带有自测用例，并确认测试用例、用例结果的正确性。（如果无法进行黑盒测试，但是可以白盒测试的话，需要有白盒测试截图或证明，如果无法白盒测试，需要有原因说明，否则不予合入）
 - PG_TRY/PG_CATCH/PG_END_TRY 使用注意事项：（1） PG_TRY/PG_CATCH中不能使用return等类似语句跳出，否则会出现随机core。 （2） PG_CATCH中没有PG_RE_THROW的分支逻辑中一定要记得清理eredata （FlushErrorState();），否则会出现暴栈 （3） PG_TRY/CATCH中不要执行hash_seq_search，假设hash_seq_search未结束时longjump到catch部分。这时候hash table还没有释放。hash_seq_search返回空的时候才释放。否则会造成hash table leak。 （4） PG_TRY/CATCH中不要加锁; （5） 在PG_TRY中使用的栈对象，不可以在PG_CACHE中再次使用，若一定要用，需要把栈对象标记为volatile。对于指针类型volatile，需要理解`void * volatile`和`volatile void *` 的区别，明确volatile加的位置； （6）在PG_CATCH代码块中分配内存时，需要通过MemoryContextSwitchTo切换内存上下文再进行内存分配。
- SQL语句类的功能和简单场景的功能需要有fastcheck用例，无法添加fastcheck用例的需要有原因说明。
- MR提交模板中的每一项均属于必填项，需要填写完整。

# 内核SQL兼容性相关需求检视checklist
 - 新增的语法、函数等功能需适配逻辑导入/导出工具（gs_dump, gs_dumpall, gs_restore）、逻辑复制等场景。
 - 查找系统表时，是否正确的使用了syscache、系统表索引。

# 资源池化相关需求检视checklist
 - 涉及DDES推点的MR需要跑SS_TEST门禁，且门禁结果通过，否则不予合入。
 