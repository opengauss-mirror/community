
# Introduction

The data.yaml is mainly used to preserve the affiliation of contributor companies. Including company, email, gitee account, github account and other information, saved in the configuration file data.yaml (note: this data.yaml file is completely public).
This configuration file includes the company information of the open source contributor's history, etc. and is mainly used to show the company's distribution of the contributor.


# How to add

reference:

```
gitee_id: gitee login id
github_id: generalfuzz
companies:
  - company_name: Huawei
    end_date: '2015-10-31'
user_name: test
emails:
  - generalftes@gmail.com
  - g.reseasdtes@gmail.com
```


- gitee_id(Mandatory): The gitee's login account name, such as zhongjun2 in https://gitee.com/zhongjun2
- github_id(Optional): Github login account name
- company_name(Mandatory): Company name, if left blank, it will be listed as an independent organization (independent)
- end_date(Optional): The end time of this company. If left blank,it means now. Format: YYYY-MM-DD
- user_name(Optional): The name displayed on the statistical board. If left blank,it will use gitee user name. github_id, gitee_id, etc. are displayed as user_name
- emails(Optional): Email information used, such as emails that have subscribed to maillist, emails that registered gitee, emails that registered github
