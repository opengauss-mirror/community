## openGauss社区命令参考文档

openGauss社区的所有项目都由Bot维护。
这意味着开发人员可以在每个Pull Request或Issue下面进行回复来触发Bot命令。
这些命令包括：

<table class="command">
    <thead>
        <tr>
            <th>命令</th>
            <th width="25%">示例</th>
            <th>描述</th>
            <th>谁能使用</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                /check-cla
            </td>
            <td style="white-space:nowrap;">
                /check-cla
            </td>
            <td>
                强制重新检查一个Pull Request的CLA状态。
                如果Pull Request的作者已经签署CLA，
                这个Pull Request将会新增一个名为`opengauss-cla/yes`的标签，
                反之将会新增一个名为`opengauss-cla/no`的标签。
            </td>
            <td>
                任何人
            </td>
        </tr>
        <tr>
            <td>
                /lgtm [cancel]
            </td>
            <td style="white-space:nowrap;">
                /lgtm
                <br/>
                /lgtm cancel
            </td>
            <td>
                为一个Pull Request添加或者删除`lgtm`标签，这个标签将用于Pull Request合入判断。
            </td>
            <td>
                这个仓库的协作者。Pull Request能使用`/lgtm cancel`命令，但是不能使用`/lgtm`命令。
            </td>
        </tr>
        <tr>
            <td>
                /approve [cancel]
            </td>
            <td style="white-space:nowrap;">
                /approve
                <br/>
                /approve cancel
            </td>
            <td>
                为一个Pull Request添加或者删除`approved`标签，这个标签将用于Pull Request合入判断。
            </td>
            <td>
                这个仓库的协作者。
            </td>
        </tr>
        <tr>
            <td>
                /[remove-]kind
            </td>
            <td style="white-space:nowrap;">
                /kind bug
                <br/>
                /remove-kind bug
            </td>
            <td>
                添加或者删除这种kind类型的标签。
                例如：`kind/bug`标签。
            </td>
            <td>
                任何人都能在一个Pull Request或者Issue上触发这种命令。
            </td>
        </tr>
        <tr>
            <td>
                /[remove-]priority
            </td>
            <td style="white-space:nowrap;">
                /priority high
                <br/>
                /remove-priority high
            </td>
            <td>
                添加或者删除这种priority类型的标签。
                例如：`priority/high`标签。
            </td>
            <td>
                任何人都能在一个Pull Request或者Issue上触发这种命令。
            </td>
        </tr>
        <tr>
            <td>
                /[remove-]sig
            </td>
            <td style="white-space:nowrap;">
                /sig sqlengine
                <br/>
                /remove-sig sqlengine
            </td>
            <td>
                添加或者删除这种sig类型的标签。
                例如：`sig/sqlengine`标签。
            </td>
            <td>
                任何人都能在一个Pull Request或者Issue上触发这种命令。
            </td>
        </tr>
        <tr>
            <td>
                /close
            </td>
            <td style="white-space:nowrap;">
                /close
            </td>
            <td>
                关闭一个Pull Request或者Issue。
            </td>
            <td>
                作者和仓库的协作者能触发这种命令。
            </td>
        </tr>
        <tr>
            <td>
                /reopen
            </td>
            <td style="white-space:nowrap;">
                /reopen
            </td>
            <td>
                重新打开一个Issue。
            </td>
            <td>
                作者和仓库的协作者能触发这种命令。
            </td>
        </tr>
        <tr>
            <td>
                /retest
            </td>
            <td style="white-space:nowrap;">
                /retest
            </td>
            <td>
                重跑测试用例任务。
            </td>
            <td>
                任何人都能在一个Pull Request上触发这种命令。
            </td>
        </tr>
        <tr>
            <td>
                /assign [[@]...]
            </td>
            <td style="white-space:nowrap;">
                /assign
                <br/>
                /assign @opengauss-bot
            </td>
            <td>
                分配一个Issue给负责人。
            </td>
            <td>
                任何人都能在一个Issue上触发这种命令，
                但是目标负责人必须是这个组织的一个成员。
                如果没有指定目标负责人，这表明这个Issue会分配给自己。
            </td>
        </tr>
        <tr>
            <td>
                /unassign [[@]...]
            </td>
            <td style="white-space:nowrap;">
                /unassign
                <br/>
                /unassign @opengauss-bot
            </td>
            <td>
                取消分配一个Issue给负责人。
            </td>
            <td>
                任何人都能在一个Issue上触发这种命令，
                但是目标负责人必须是这个组织的一个成员。
                如果没有指定目标负责人，这表明这个Issue会取消分配给自己。
            </td>
        </tr>
        <tr>
            <td>
                /check-issue
            </td>
            <td style="white-space:nowrap;">
                /check-issue
            </td>
            <td>
                检查Pull Request是否关联了Issue，如果未关联Issue，添加needs-issue标签，如果已关联，则删除needs-issue标签。
            </td>
            <td>
                任何人都能在一个Pull Request上触发这种命令。
            </td>
        </tr>
        <tr>
            <td>
                /remove-needs-issue
            </td>
            <td style="white-space:nowrap;">
                /remove-needs-issue
            </td>
            <td>
                删除needs-issue标签。
            </td>
            <td>
                只有仓库成员才能在Pull Request上触发这种命令。
            </td>
        </tr>
    </tbody>
</table>

