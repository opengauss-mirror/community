# 简介

该仓库主要用于保存贡献者公司的隶属关系。包括公司、email、gitee账号、github账号等信息，保存在配置文件data.json中（注：此data.json文件是完全公开的）。
此配置文件包括开源贡献者历史的公司信息等，主要用于展示贡献者的公司分布。


# 如何添加

参考：

```
gitee_id: gitee login id
github_id: generalfuzz
companies:
  - company_name: Huawei
    organization_name: openlookeng
    end_date: '2015-10-31'
user_name: test
emails:
  - generalftes@gmail.com
  - g.reseasdtes@gmail.com
```

- gitee_id(必选)：gitee的login账号名，比如https://gitee.com/zhongjun2  中的zhongjun2
- github_id(可选)：github的login账号名
- company_name(必选): 公司名称,如果不填将会被列入独立组织(independent)
- organization_name(可选): 公司下面的组织名称
- end_date(可选)：在这个公司的结束时间，如果不填表示当前一直在该公司，格式：YYYY-MM-DD
- user_name(可选): 显示在统计看板上面的名称，如果不填展示gitee账号的名称，github_id、gitee_id等统一对外显示成user_name
- emails(可选): 使用的email信息，比如订阅过maillist的email，注册gitee的email，注册github的email


