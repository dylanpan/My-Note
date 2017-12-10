# My-Note

邮件信息获取

1.在function list 的lua文件中添加监听，被监听的方法从mail manager中获取unread mail num
做法：
local num = MailManager:gerUnreadNum()


2.mail manager从mail server中持续更新请求，获得unread mail num
(1)做法：
MailManager.getUnreadNum = function()
	—由MailServer:updateUnreadMailNum中获取未读邮件数量
	return unreadNum
end

(2)做法：
其他的MailManager方法中获取对应未读邮件数量，然后eventDispatch，最后由getUnreadNum方法返回

3.mail server向socket持续发送请求，获得unread mail num
(1)做法：
将updateUnreadMailNum方法添加到监听

MailServer.updateUnreadMailNum = function ()
	(1)sendPackage
	(2)getData
	(3)filterData
	(4)eventDispatch(unreadNum)
end


4.从哪里开始触发mail server持续发送请求
(1)做法：从加载主页面【home scene】中的update方法里面发起
update = function ()
	
end
