Online Markdown Editor
Input

Android Intent

1. Overview

Android Intent��Ŀ����Ϊ�˸��������ṩһ��ͨ��js������android�ֻ�������һ��intent�ķ�����
Web Intent�� Web Intent��������android intent��һ�����ƣ���������Ŀ�Ļ�������web������web��ģ��android intent��
Android Intent�� Android Intent��һ����android�ֻ�������intent�ķ�ʽ��
�����㶹�԰ٱ������ԣ���Ҫ�ۺ����ֵ��ص㣬ʵ��һ��ͨ��js�ķ�ʽ�����ֻ�������һ��intent��
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
4. ���������ĺ�����android intent�ĺ���һ�£�

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

��ʽָ��Intent���������ͣ�MIME��
data
ִ�ж���Ҫ����������
category

��ִ�ж����ĸ�����Ϣ����ʽΪjson
Constant

CATEGORY_BROWSABLE
CATEGORY_GADGET
CATEGORY_HOME
CATEGORY_LAUNCHER
CATEGORY_PREFERENCE
component

ָ��Intent�ĵ�Ŀ�������������
extras
�������и�����Ϣ�ļ��ϣ���ʽΪjson
flags
������������
Copyright ? 2010 CtrlShift.net Powered by Markdown Engine "Showdown". Convert text  3 ms