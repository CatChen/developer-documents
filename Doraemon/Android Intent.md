Online Markdown Editor
Input

Android Intent

1. Overview

Android Intent的目的是为了给开发者提供一个通过js调用在android手机上启动一个intent的方法。
Web Intent： Web Intent是类似与android intent的一个机制，但是它的目的还是用于web，即在web上模拟android intent。
Android Intent： Android Intent是一个在android手机上启动intent的方式。
对于豌豆荚百宝袋而言，需要综合两种的特点，实现一种通过js的方式来在手机上启动一个intent。
2. Design

interface AndroidIntent { 
    attribute DOMString action; 
    attribute DOMString type; 
    attribute DOMString data; 
    attribute DOMString category; 
    attribute DOMString component; 
    attribute DOMString extras; 
    attribute long flags;

    void startActivity();
};
3. Implementation

var component = "com.wandoujia.phoenix2/com.wandoujia.phoenix2.ui.WelcomeActivity";
var extras = [];

var item = {};
item.key = "phoenix.intent.extra.USER_AGENT";
item.value = "wandoujia";
extras.push(item);

var i = new AndroidIntent("","","",
                         JSON.stringify(category),
                         component,
                         JSON.stringify(extras));
// i.setFlags(0);

i.startActivity();
4. 各个参数的含义与android intent的含义一致：

action

ACTION_CALL
ACTION_EDIT
ACTION_MAIN
ACTION_SYNC
ACTIONBATTERYLOW
ACTIONHEADSETPLUG
ACTIONSCREENON
ACTIONTIMEZONECHANGED
type

显式指定Intent的数据类型（MIME）
data
执行动作要操作的数据
category

被执行动作的附加信息，格式为json
Constant

CATEGORY_BROWSABLE
CATEGORY_GADGET
CATEGORY_HOME
CATEGORY_LAUNCHER
CATEGORY_PREFERENCE
component

指定Intent的的目标组件的类名称
extras
其它所有附加信息的集合，格式为json
flags
控制启动参数
Copyright ? 2010 CtrlShift.net Powered by Markdown Engine "Showdown". Convert text  3 ms