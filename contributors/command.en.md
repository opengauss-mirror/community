## openGauss Community Command Help

All of the projects in openGauss Community are maintained by Bot.
That means the developpers can comment below every Pull Request or Issue to trigger Bot Commands.
The Commands incluing as follows:

<table class="command">
    <thead>
        <tr>
            <th>Command</th>
            <th width="25%">Example</th>
            <th>Description</th>
            <th>Who Can Use</th>
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
                Forces rechecking of the CLA status of a Pull Request.
                If the Pull Request author has already signed CLA,
                the label `opengauss-cla/yes` will be added in the Pull Request,
                If not, the label `opengauss-cla/no` will be added.
            </td>
            <td>
                Anyone
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
                Adds or removes the `lgtm` label which is typically used to gate merging.
            </td>
            <td>
                Collaborators on the repository. `/lgtm cancel` can be used additionally by the Pull Request author.
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
                Adds or removes the `approved` label which is typically used to gate merging.
            </td>
            <td>
                Collaborators on the repository.
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
                Applies or removes a kind label from one of the recognized types of labels.
                For example, the label is more like `kind/bug`.
            </td>
            <td>
                Anyone can trigger this command on a Pull Request or Issue.
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
                Applies or removes a priority label from one of the recognized types of labels.
                For example, the label is more like `priority/high`.
            </td>
            <td>
                Anyone can trigger this command on a Pull Request or Issue.
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
                Applies or removes a sig label from one of the recognized types of labels.
                For example, the label is more like `sig/sqlengine`.
            </td>
            <td>
                Anyone can trigger this command on a Pull Request or Issue.
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
                Closes a Pull Request or an Issue.
            </td>
            <td>
                Authors and collaborators on the repository can trigger this command.
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
                Reopens an Issue.
            </td>
            <td>
                Authors and collaborators on the repository can trigger this command.
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
                Rerun test jobs that have failed.
            </td>
            <td>
                Anyone can trigger this command on a Pull Request.
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
                Assigns an assignee to an Issue.
            </td>
            <td>
                Anyone can use this command on an Issue,
                but the target user must be a member of the org that owns the repository.
                If no target user is specified, that means this Issue will be assigned to yourself.
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
                UnAssigns an assignee from an Issue.
            </td>
            <td>
                Anyone can use this command on an Issue,
                but the target user must be a member of the org that owns the repository.
                If no target user is specified, that means this Issue will be unassigned from yourself.
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
                Check whether pull request is associated with issues,
                if pull request is not associated with issues.
                this command will add a 'needs-issue' label on pull request.
                if pull request is associated with issues, 
                this command will delete the 'needs-issue' label on pull request.
            </td>
            <td>
                Anyone can use this command on a pull request.
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
                Delete the 'needs-issue' label on a pull request.
            </td>
            <td>
                Only collaborators of repository can use this command on a pull request.
            </td>
        </tr>
        <tr>
            <td>
                /retest-static
            </td>
            <td style="white-space:nowrap;">
                /retest-static
            </td>
            <td>
                Rerun codecheck jobs that have failed.
            </td>
            <td>
                Anyone can use this command on a pull request.
            </td>
        </tr>
    </tbody>
</table>


