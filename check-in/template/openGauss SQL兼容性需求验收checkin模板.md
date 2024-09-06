## openGauss SQL兼容性需求check-in评审报告

# 评审纪要

时间：
特性名称：
特性责任人：
评审人：

# 设计checklist

| 模块     | 类别     | 检查项                                          | 检查项详细说明                                                                                                                                                                                                                                                                   | 是否涉及 | 是否完成检查 |
| ------ | ------ | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- | ------ |
| GUC参数  | 功能     | 新增GUC参数适配项                                   | ①guc.cpp里需要新增guc参数的相应代码，包括参数的校验/赋值等功能函数；     ②如果要加入postgres.conf，需要修改postgresql_single.conf.sample     路径：src/common/backend/utils/misc/     一般以注释方式加入，如果非常确认使用某个默认值，也可以以非注释方式加入     ③如果要允许gs_guc工具设置，请修改cluster_guc.conf     路径：src/bin/gs_guc/cluster_guc.conf          |      |        |
| 升级     | 兼容性    | 版本号变更                                        | src/common/backend/utils/init/globals.cpp  ：GRAND_VERSION_NUM                                                                                                                                                                                                             |      |        |
| 升级     | 兼容性    | 前向兼容性                                        | 1）涉及系统表修改的特性，必须提供系统表升级脚本和回滚脚本，修改版本号文件     2）对于涉及修改持久化数据（如日志）的特性，必须考虑新老版本共存时的兼容性场景，必要情况下，需要增加版本号以进行识别     3）对于涉及修改执行态数据格式（如syscache结构）的特性，必须考虑新老版本共存时的兼容性场景，必要情况下，需要增加版本号以进行识别                                                                                             |      |        |
| 升级     | 兼容性    | 验证升级正常                                       | 涉及到升级时需要验证如下场景：     1. 集群环境安装：该步骤会验证集群环境安装是否正常     2. 集群环境升级：从老的版本（1.1.0版本）升级到最新版本是否正常                                                                                                                                                                                    |      |        |
| 公共数据结构 | 功能     | hashtable                                    | hashtable使用注意事项     ①在使用hash表时，entry必须封装成一个结构体，第一个成员必须是hash key     否则会造成查找失败！！     ②封装的结构体必须只有两个成员：key+value，即value需要封装起来     否则hash表在search的时候会core！！     ③hash表在创建的时候，entry 的size一定要正确     否则在enter的时候会造成写越界，不会报错但是其它变量内存会被踩，不易发现！！ ④在遍历hash表的循环过程中，使用hash_seq_init初始化游标时重点审视是否存在重复问题，是否符合预期。                                   |      |        |
| 公共数据结构 | 功能     | 禁止使用commandTag     判断Query的类型                | 需要对SELECT\INSERT\UPDATE\DELETE\MERGE  INTO等query类型进行识别判断时，应该使用CmdType进行判断或新增标识。     禁止使用commandTag作为判断标识，因为commandTag在带returning*语句执行中变化。                                                                                                                                 |      |        |
| 系统函数   | 兼容性    | 系统表升级是否正确                                    | 通过对比initdb和升级后的db中pg_proc每一列的值，避免出现升级和非升级不一致的情况                                                                                                                                                                                                                           |      |        |
| 系统函数   | 兼容性    | 新增数据类型适配FENCED函数                             | 新增数据类型如果是FENCED函数使用，需要修改UDFArgumentHandler函数，把数据类型添加到对应收发分支。                                                                                                                                                                                                              |      |        |
| 系统函数   | 功能     | NULL值处理                                      | 对于非strict函数允许接收NULL入参，在函数逻辑中应对NULL值进行细致的处理                                                                                                                                                                                                                                |      |        |
| 前向兼容性  | 兼容性    | Node相关数据结构删减                                 | 禁止对Node相关数据结构（如Query、RangeTblEntry）数据成员删减                                                                                                                                                                                                                                 |      |        |
| 兼容性    | 兼容性    | 兼容性设计原则                                      | 目前支持兼容性PG,A,B,C;对于每一个兼容点要求：     1、如果该兼容点为非冲突兼容点，应该是各个兼容模式下均支持，不需要开关控制     2、如果该兼容性点为冲突兼容点，应该由兼容开关控制。                                                                                                                                                                      |      |        |
| 查询解析   | 兼容性    | 添加关键字场景                                      | 为了尽可能的防止移进规约冲突，最大化的用关键字作为对象名，关键字分有4类：非保留关键字、列名关键字、类型函数关键字、保留关键字。他们的约束逐渐加强，比如保留关键字不可以用做表名。添加关键字需要考虑如下：     1. 添加新的关键字最好先作为非保留关键字添加     2. 如果要加其他关键字类型那么需要考虑是否有前向兼容问题。比如排查客户场景是否有用该关键字作为对象名。     3. 关键字还需要加入kwlist.h文件 4. 对于B兼容性，新增关键字时候，需要检查新增的关键字是否可以用于MySQL中不带反引号的表别名与列别名，如果可以，需要新增关键字到alias_name_XXX的对应位置。                                                    |      |        |
| 查询解析   | 兼容性    | Gram.y中处理语法冲突                                | 1、合理使用a_expr/b_expr/c_expr使用场景     为了尽可能防止冲突，划分了a_expr/b_expr/c_expr，比如BETWEEN a_expr AND b_expr中  AND属于a_expr范畴，b_expr中不含AND。否则就无法区分BETWEEN之后是Bool判断还是范围。c_expr是a_expr和b_expr的交集。所以  尽量用a_expr这样支持的范围最广。如果用b_expr/c_expr 那需要考虑潜在的用户问题场景（参考BETWEEN...AND...例子）并在手册中写清楚约束。 |      |        |
| 其他     | 功能     | 新增已有的数据结构成员适配序列化与反序列化                        | 注意适配：src/common/backend/nodes/copyfuncs.cpp     src/common/backend/nodes/equalfuncs.cpp     src/common/backend/nodes/outfuncs.cpp     src/common/backend/nodes/readfuncs.cpp                                                                                              |      |        |
| 公共子系统  | 内存定位定界 | 局部变量内存释放，非程序结尾位置，释放进行置空；全局内存变量释放，无论什么位置均需要置空 | 防止内存使用出现use-after-free模式，内存越界                                                                                                                                                                                                                                             |      |        |
| 公共子系统  | 内存定位定界 | 对于使用数组、下标访问内存操作场景，是否提前判断下标符合内存空间要求           | 防止出现heap  overflow场景                                                                                                                                                                                                                                                      |      |        |
| 公共子系统  | 内存定位定界 | 内存分配报错日志中，是否需要新增信息，便于分析报错原因                  | 内存报错场景下，快速定位内存报错原因                                                                                                                                                                                                                                                        |      |        |
| 资源负载管理 | 兼容性    | 只能新增系统表参数，不可以删除已有的参数                         | 前向兼容                                                                                                                                                                                                                                                                      |      |        |
| 资源负载管理 | 功能     | 新增系统表参数的默认初始化数值要合理，不影响已有的功能                  | 前向兼容                                                                                                                                                                                                                                                                      |      |        |
| HA用例   | 功能     | ha  check                                    | 1.HA相关设计实现需要严格系统的测试。     2.需要保证最简单的功能验证，包括搭建主备环境，确认主备可以正常同步，以及跑ha check用例，确认所有用例可以跑过。     3.需要完成各种故障场景的验证，设计详细的故障库，确保覆盖各个场景。                                                                                                                                              |      |        |
| 安全     | 未公开接口  | 是否新增或修改函数、视图、系统表                             | 新增或修改函数、视图、系统表需刷新产品文档，考虑权限控制     2.新增函数、系统表的oid避免选择[7000,8000]区间内的。                                                                                                                                                                                                                                              |      |        |
| 安全     | 未公开接口  | 是否新增SQL语法                                    | 新增SQL语法需刷新产品文档，支持记录审计日志                                                                                                                                                                                                                                                   |      |        |

# 特性LLT测试方案及验证结论

## 基本测试

基本功能测试

# 回归测试验证

| 测试集       | 结论  |
| --------- | --- |
| fastcheck |     |
| memcheck  |     |
| hacheck   |     |
| subscription/check   |     |

## Fastcheck

参考社区博客获取fastcheck/memcheck/hacheck/subcheck的执行方法：

https://opengauss.org/zh/blogs/xiteming/HowtorunFastcheck.html

## Memcheck

## hacheck

## subscription/check

# 升级验证

升级、回滚脚本编写请参考开发指导：
https://www.opengauss.org/zh/blogs/ganyang/SQL%E5%BC%95%E6%93%8E%E6%8F%92%E4%BB%B6%E5%BC%80%E5%8F%91%E6%8C%87%E5%AF%BC.html

升级、回滚操作请参考文档步骤：
https://docs.opengauss.org/zh/docs/latest/docs/DatabaseOMGuide/%E5%8D%87%E7%BA%A7%E6%93%8D%E4%BD%9C.html

升级包即 ```build.sh -pkg``` 生成的打包文件以及对应OM安装包，参考企业版安装包目录结构
验证前请先创建B兼容数据库，否则不会执行插件升级步骤

| 验证集       | 结论  |
| --------- | --- |
| openGauss LTS版本升级到最新master |    |
| 社区最新master回滚到旧版本  |     |
| openGauss LTS版本再升级到最新master   |     |
| openGauss LTS版本升级提交到最新master   |     |

## openGauss LTS版本升级到最新master
## openGauss最新master回滚到旧版本
## openGauss LTS版本再升级到最新master
## openGauss LTS版本升级提交到最新master

# 代码检视结论

## 编码规范检查

### 编程规范

请对照社区安全编码规范进行排查：

https://gitee.com/opengauss/security/blob/master/guide/SecureCoding.md

https://gitee.com/opengauss/security/blob/master/guide/SecureCompile(C&C++).md

### 内存使用排查

### 覆盖率

增量代码测试用例覆盖率80%+

参考社区博客获取增量代码覆盖率的执行方法：

https://opengauss.org/zh/blogs/totaj/%E5%A6%82%E4%BD%95%E8%B7%91%E5%A2%9E%E9%87%8F%E4%BB%A3%E7%A0%81%E8%A6%86%E7%9B%96%E7%8E%87.html

### 鲲鹏平台乱序排查

| **编号** | **排查依据**                 | **排查结果** |
| ------ | ------------------------ | -------- |
| **1**  | **是否为多线程并发场景？**          |          |
| **2**  | **是否涉及线程间共享数据？**         |          |
| **3**  | **是否未对共享数据加锁保护？**        |          |
| 4      | 线程间共享数据是否存在无锁同步模式？       |          |
| 5      | 是否 **未** 在正确的位置插入合适的内存屏障 |          |

## 代码检视意见

| 提出人 | 意见  | 答复详情 |
| --- | --- | ---- |
|     |     |      |
|     |     |      |
|     |     |      |
|     |     |      |
|     |     |      |
|     |     |      |
|     |     |      |

# 遗留问题

# 测试建议
