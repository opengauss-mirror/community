# openGauss Developer Day 2022 SIG组版本工作会议指南 

## <center> 介绍
openGauss开源社区按照不同的 SIG(Special Interests Group，请查看[专项兴趣小组](https://gitee.com/opengauss/tc/blob/master/sigs/README.md)) 来组织开发及版本发布工作，openGauss开源社区的主要技术产品通过 openGauss开源数据库及周边生态工具承载，它在每年的 3 月、 9 月和12月发布三个版本，分别对应正式版、创新版和Update版。当一个版本发布完成后，openGauss开源社区将召开下一个版本的开发规划会议，会议以SIG组为单位，时长为0.5~1天，用于集中讨各SIG组在下一个版本中的规划、工作事项、任务分工、优先级等相关内容。openGauss开源社区将为各SIG组的规划会议提供场地和技术支持。

SIG版本规划工作会议遵循开源、开放原则，议题收集、技术讨论、会议纪要等各讨论过程均对外开放。


## <center> 会议类型

**单SIG组工作会议**：单一SIG组内的工作会议，由该SIG组Maintainer进行组织，包括议题收集、议程安排、主持讨论、会议纪要输出等。

**跨SIG组工作会议**：跨SIG组之间的协作工作会议，需要各相关SIG组Maintainer提前通过邮件或其他方式与版本规划会议组织者联系并沟通场地安排并由各相关SIG组Maintainer负责进行组织，包括议题收集、议程安排、主持讨论、会议纪要输出等。

## <center> 需求收集

各SIG应择时启动针对后续版本的需求收集，各SIG组Maintainer在openGauss Etherpad平台(https://etherpad.opengauss.org/)创建相应的会议收集目录(建议命名方式为: sig名-版本名(例如3.1.0)-Planning)用于收集该版本规划工作会议的需求收集及计划，并将该会议目录反馈至openGauss开源社区SIG版本规划会议组织者。(参考模板：https://etherpad.opengauss.org/p/planning-template)

任何人均可以在SIG版本工作会议中提出需求，通过在各SIG版本工作会议指定的Etherpad共享文件中的Topics环节根据要求进行填写，通常需要包含以下内容：
- 需求发起人
- 需求的具体描述
- Issue 反馈的在线地址
- 已有的技术方案或PR
- 已有的讨论纪要

需求收集完成后由SIG组Maintainers按照所有收集到的需求的具体情况(类型、技术难度、工作量等)，根据会议时间安排指定会议议程，会议安排在工作会议召开前3天在Etherpad共享文件及社区邮件列表Maillist中公开发布，方便与会者了解会议议程。

## <center> 召开会议

会议由各SIG组版本规划负责人主持召开，按照预先制定的会议议程进行会议，会议过程中需要注意时间控制，确保所有已经在会议议程中的需求都能得到相应的讨论时间。各与会者需要在Etherpad的Attendees环节根据要求填写自己的名字和Gitee_ID，若未到场且未指定代参加人员则该需求视为自动放弃。

各议题讨论可以分为下面几个阶段：
1. 需求陈述：由需求发起人对需求进行陈述，包括需求目标、需求来源、提议的技术方案及既往的讨论及结果等，需求陈述阶段其余听众不允许打断。
2. 讨论：由各参会者针对该需求进行相应的讨论，所有与会者均可参与讨论，主持人负责记录各方观点及重点意见。
3. 总结：在达成共识后，由主持人根据共识输出该议题的结论。若现场没有达成共识，则应商议再次讨论的具体时间。

所有议题讨论完成后，由SIG Maintainer团队根 据各议题讨论情况及SIG组实际情况对各需求进行优先级排序及分工，“任务分工”靠贡献者“认领任务”的方式完成。

## <center> 会议纪要

各SIG组版本规划负责人在工作会议结束后一周内整理完成会议纪要，并在Etherpad及SIG组、dev, tc, release sig邮件列表Maillist上公开发布该会议纪要，以便开发者、用户了解未来版本各SIG的工作计划，会议纪要需要包含以下内容：
- 工作会议与会者
- 所有参与讨论的议题及该议题的结论
- 下一版本各工作的负责人
- 下一版本的工作优先级
会议纪要内容参考链接：https://mailweb.openeuler.org/hyperkitty/list/openstack@openeuler.org/thread/NR3O2ZUUNE46XFBTV4CND4HEYDCBPW33/
