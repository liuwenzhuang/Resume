# 求职-前端开发工程师-刘文壮

# 联系方式
- 手机：17611267056
- Email：liu1114589929@gmail.com
- 微信号：liu1114589929

# 工作经历

|**时间**|**公司**|**职责**|
| ------- | ------ | ----- |
|2015年7月 ~ 2016年5月|北京迈特克科技有限公司|负责crm应用开发，旨在解决客户管理、代理管理、机构内部管理；负责维护公司主页，添加最新功能。|
|2016年5月 ~ 至今|用友网络科技股份有限公司|负责友报账APP端，Web端开发；负责集团审批系统的开发与维护工作|

# 项目经历

## 碧桂园财务共享项目现场支持
碧桂园财务共享项目为集团级支持项目，16年6月份-16年12月份受公司指派前往碧桂园总部进行现场支持，主要负责审批子系统和人力子系统的上线与维护工作。

项目框架：
React + Redux + redux-saga

主要功能：
1. 审批子系统
审批子系统主要的功能是为了简化工作流程，提高工作效率，面对的对象均是各级具有审批权限的领导，提供手机端审批功能和PC端审批功能。项目支持期间共解决项目问题600余个，其中涉及到多部门协作的问题约300余个。并且期间在碧桂园东莞分公司成功部署使用，至年底报销周期通过线上审批单据约达2万张。

2. 人力子系统
人力子系统主要的功能是为了简化人力部门的包括入职、培训、离职等工作。项目支持期间共解决问题200余个，并且在16年10月份按期上线。

由于两个子系统均涉及到移动端web开发，故性能优化极为重要，大致优化过程如下：
1. 解决大量重复渲染的问题，主要利用`shouldComponentUpdate`和`PureComponent`避免重复渲染，对未按照immutable规范的数据的使用进行了彻底的重构。

2. 解决deepCompare带来的性能问题，抛弃较深的数据层级结构，首先与后端约定浅层次数据结构，其次在前端保证状态树的纵深不会过大。

3. 解决数据重复请求的问题，由于列表数据量较大，多次重复请求会造成性能损失，并且会造成无意义请求。主要对列表数据接口约定时效性，在时效性内使用状态树中数据，并配合本地存储，不造成重复请求。

## 移动审批轻应用
公司移动审批本为原生应用，由于维护、升级成本高，且不符合“去App化”的趋势，故进行移动审批转轻应用的开发工作，需要在完全保留原生应用的功能下增加查看影像、附件等功能。

项目框架：
Angular + Webpack

主要功能：
1. 异步审批
审批操作，特别是涉及到交叉校验规则的单据，审批时间会比较长，堵塞用户操作，造成用户体验问题，故将审批动作设计成异步操作，与后台开发配合，当用户进行审批动作后可马上返回列表，在列表中显示单据的审批状态。

2. 批量审批
集团级单据具有单据集中提交的特点，故单独为“批准”操作开发出批量审批的功能。

性能优化：
1. 对大部分输出组件的设置检测策略`changeDetection`为`ChangeDetectionStrategy.OnPush`从而避免无意义刷新。

2. 列表循环设置`trackBy`，减少DOM更新操作。

3. 对大量单据的批量审批操作采用`循环展开`的方式，分部分独立处理以避免大量循环产生的开销。

项目最终在为期30人天的开发周期内完成开发，并在集团内部和多家客户应用内上线。

## 友报账APP
公司在PC端报销方面发展多年，为适应移动APP时代需要将报销相关业务转移到移动APP中，故而公司组建财务云事业部，主要进行友报账APP的开发，与PC端报销相辅相成。我主要负责**记事模块**和**单据模块**的开发。

项目框架：
Ionic + Angular + Cordova

负责模块：
1. 记事模块
记事模块的难点在于抽象多种类型记事的共同点以及动态表单的开发，抽象多种记事共同点后通过继承关系可以避免大量重复逻辑（如保存、提交、加载附件等操作）。而动态表单则涉及到读取配置、渲染配置、针对不同类型表单元素的处理和校验等过程，主要涉及到与后台约定表单元素的类型和数据结构，而且要对用户输入进行统一的前端校验及状态提示。

2. 单据模块
单据模块的处理包含查看单据的审批流、对单据进行删、改操作以及催审的功能。查看审批流支持查看单据在手时间、完整审批流程等功能；催审操作目前支持传统的电话、邮件、短信方式，而且还能够使用即时通信与审批人进行会话。

经过与同事的协同开发，友报账APP第一版本经过45人天双端顺利发版，至今已迭代近30个版本（包括原生应用的发布以及应用内更新发布）。

在开发迭代过程中经历多次框架版本升级，首先需要确定框架升级的版本号，其次评估对工程中各依赖模块的影响，团队内一般采用[框架最新版本-2]的原则进行升级，升级后对各功能模块进行单元测试。

## 友报账工作台及嵌入功能
友报账工作台为PC端Web应用，主要是用来对友报账APP进行权限、功能的配置。考虑到开发的速度和功能的重用性，使用React全家桶开发工作台应用及嵌入应用。开发过程中主要关注点在于各功能模块相互独立，仅是共用登录信息，故将工作台设计为**应用容器**，并通过iframe嵌入主体功能页面的方式简化实际功能的开发过程，如能够屏蔽繁琐的登录操作、避免路由的混乱等。但使用iframe需要解决前端缓存问题，除了各嵌入功能使用webpack的**hash**功能解决前端js缓存，各嵌入应用发布时，工作台应用也需要为应用链接增加版本号。目前公司内部和用户已经能够使用友报账工作台对友报账进行配置，财务人员也可使用友报账工作台进行支付，配合友报账APP实现了从**提单-审批-支付**的全部流程。

项目框架：
dva + antd + redux-saga

主要功能：
1. 工作台动态菜单、应用
工作台使用动态获取菜单、应用的方式，根据用户权限开放不同功能，使用React高阶组件控制菜单项的加载以及应用的展示。

2. 结算中心
结算中心为面向财务的嵌入应用，接入畅捷支付，用户需要使用畅捷支付提供的u盾保证支付的安全性。用户支付时首先需要校验用户是否安装证书、证书是否和u盾相匹配。

3. 自动报账
自动报账为管理员提供了批量为员工生成报销单的方式，仅需按照提供的excel模板填写相关人员信息和报销信息，系统即可为这些人员自动生成报销单，免去了员工自己手工提单的操作。管理员能够进行查看单据信息、为报销单相关用户发送通知(APP、邮件、短信)、删除单剧等操作。

* * *
# 开发中遇到的问题及解决方案

- 单页面应用首页加载慢的问题：按需加载页面、最小化引入。
- 叶子节点预加载：按需加载页面大部分情况下作用良好，但对于叶子节点页面可以预加载，提升页面加载速度。
- 应用效率问题：对静态资源启用压缩、对ajax请求数据使用Redis缓存、前端数据按时效性进行缓存。
- 提高调试效率：启用“模块热替换”、SourceMap。

* * *
# 专业技能

 - 4年前端开发经验，2年H5移动端开发经验，1年团队管理经验
 - 熟悉Redux内部原理
 - 有性能优化的经验
 - 熟练掌握git

* * *
# 教育经历
2011-2015：计算机科学与技术、辽宁石油化工大学、本科

* * *
# 技术文章

## 翻译文章

- [Angular2 Form之模板驱动](http://liuwenzhuang.github.io/2016/05/24/angular2-template-form.html)
- [自此使用Object字面量取代switch](http://liuwenzhuang.github.io/2016/03/25/replace-switch-with-object-literals.html)

## 自我笔记

- [Ionic 2之页面堆栈](http://liuwenzhuang.github.io/2016/04/15/ionic2-navigation-stack.html)
- [Angular 2 父子组件数据通信](http://liuwenzhuang.github.io/2016/03/11/angular2-component-data-binding-and-event.html)
