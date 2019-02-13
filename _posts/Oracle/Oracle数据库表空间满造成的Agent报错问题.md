Title: Oracle表空间满造成的ODI Agent报错
Date:
URL: 
Tags: 

Agent运行中突然报错，没有具体错误，就显示连接到数据库出错。
任务都显示运行中，无法结束，提示连接数据库出错。如果手动关闭就提示
```
oracle.odi.runtime.agent.invocation.InvocationException: http://localhost:20910/oraclediagent:java.lang.RuntimeException: javax.xml.bind.UnmarshalException
 - with linked exception:
[Exception [EclipseLink-25004] (Eclipse Persistence Services - 2.6.5.v20170607-b3d05bd): org.eclipse.persistence.exceptions.XMLMarshalException
Exception Description: An error occurred unmarshalling the document
Internal Exception: com.ctc.wstx.exc.WstxIOException: Invalid UTF-8 middle byte 0x3f (at char #225, byte #37)] HttpPost.getResponseBodyAsString(): [
<?xml version="1.0" encoding="UTF-8"?><OdiAgentErrorResponse xmlns="xmlns.oracle.com/odi/OdiAgentMessages/V11"><MessageInvoked>OdiKillSession</MessageInvoked><Code>1269</Code><ErrorMessage>ODI-1269: 代理ODIAgentA无法停止会话Mapping_GXK_TO_XCX_XSDT_物理_SESS (23953): 会话正在由另??个同名代理运行???</ErrorMessage></OdiAgentErrorResponse>
]
	at oracle.odi.runtime.agent.invocation.RemoteRuntimeAgentInvoker.invoke(RemoteRuntimeAgentInvoker.java:498)
	at oracle.odi.runtime.agent.invocation.support.InternalRemoteRuntimeAgentInvoker.invoke(InternalRemoteRuntimeAgentInvoker.java:162)
	at oracle.odi.runtime.agent.invocation.RemoteRuntimeAgentInvoker.invokeStopSession(RemoteRuntimeAgentInvoker.java:1276)
	at oracle.odi.runtime.agent.invocation.RemoteRuntimeAgentInvoker.invokeStopSession(RemoteRuntimeAgentInvoker.java:1257)
	at oracle.odi.ui.action.SnpsPopupActionKillImmediateHandler.actionPerformed(SnpsPopupActionKillImmediateHandler.java:122)
	at com.sunopsis.graphical.frame.edit.EditFrameSnpSession$ActionForMenuToolButton.actionPerformed(EditFrameSnpSession.java:337)
	at javax.swing.AbstractButton.fireActionPerformed(AbstractButton.java:2022)
	at javax.swing.AbstractButton$Handler.actionPerformed(AbstractButton.java:2348)
	at javax.swing.DefaultButtonModel.fireActionPerformed(DefaultButtonModel.java:402)
	at javax.swing.DefaultButtonModel.setPressed(DefaultButtonModel.java:259)
	at javax.swing.AbstractButton.doClick(AbstractButton.java:376)
	at javax.swing.plaf.basic.BasicMenuItemUI.doClick(BasicMenuItemUI.java:842)
	at javax.swing.plaf.basic.BasicMenuItemUI$Handler.mouseReleased(BasicMenuItemUI.java:886)
	at java.awt.Component.processMouseEvent(Component.java:6533)
	at javax.swing.JComponent.processMouseEvent(JComponent.java:3324)
	at java.awt.Component.processEvent(Component.java:6298)
	at java.awt.Container.processEvent(Container.java:2237)
	at java.awt.Component.dispatchEventImpl(Component.java:4889)
	at java.awt.Container.dispatchEventImpl(Container.java:2295)
	at java.awt.Component.dispatchEvent(Component.java:4711)
	at java.awt.LightweightDispatcher.retargetMouseEvent(Container.java:4889)
	at java.awt.LightweightDispatcher.processMouseEvent(Container.java:4526)
	at java.awt.LightweightDispatcher.dispatchEvent(Container.java:4467)
	at java.awt.Container.dispatchEventImpl(Container.java:2281)
	at java.awt.Window.dispatchEventImpl(Window.java:2746)
	at java.awt.Component.dispatchEvent(Component.java:4711)
	at java.awt.EventQueue.dispatchEventImpl(EventQueue.java:758)
	at java.awt.EventQueue.access$500(EventQueue.java:97)
	at java.awt.EventQueue$3.run(EventQueue.java:709)
	at java.awt.EventQueue$3.run(EventQueue.java:703)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.security.ProtectionDomain$JavaSecurityAccessImpl.doIntersectionPrivilege(ProtectionDomain.java:80)
	at java.security.ProtectionDomain$JavaSecurityAccessImpl.doIntersectionPrivilege(ProtectionDomain.java:90)
	at java.awt.EventQueue$4.run(EventQueue.java:731)
	at java.awt.EventQueue$4.run(EventQueue.java:729)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.security.ProtectionDomain$JavaSecurityAccessImpl.doIntersectionPrivilege(ProtectionDomain.java:80)
	at java.awt.EventQueue.dispatchEvent(EventQueue.java:728)
	at oracle.javatools.internal.ui.EventQueueWrapper._dispatchEvent(EventQueueWrapper.java:169)
	at oracle.javatools.internal.ui.EventQueueWrapper.dispatchEvent(EventQueueWrapper.java:151)
	at java.awt.EventDispatchThread.pumpOneEventForFilters(EventDispatchThread.java:201)
	at java.awt.EventDispatchThread.pumpEventsForFilter(EventDispatchThread.java:116)
	at java.awt.EventDispatchThread.pumpEventsForHierarchy(EventDispatchThread.java:105)
	at java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:101)
	at java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:93)
	at java.awt.EventDispatchThread.run(EventDispatchThread.java:82)
Caused by: java.lang.RuntimeException: javax.xml.bind.UnmarshalException
 - with linked exception:
[Exception [EclipseLink-25004] (Eclipse Persistence Services - 2.6.5.v20170607-b3d05bd): org.eclipse.persistence.exceptions.XMLMarshalException
Exception Description: An error occurred unmarshalling the document
Internal Exception: com.ctc.wstx.exc.WstxIOException: Invalid UTF-8 middle byte 0x3f (at char #225, byte #37)] HttpPost.getResponseBodyAsString(): [
<?xml version="1.0" encoding="UTF-8"?><OdiAgentErrorResponse xmlns="xmlns.oracle.com/odi/OdiAgentMessages/V11"><MessageInvoked>OdiKillSession</MessageInvoked><Code>1269</Code><ErrorMessage>ODI-1269: 代理ODIAgentA无法停止会话Mapping_GXK_TO_XCX_XSDT_物理_SESS (23953): 会话正在由另??个同名代理运行???</ErrorMessage></OdiAgentErrorResponse>
]
	at oracle.odi.runtime.agent.invocation.RemoteRuntimeAgentInvoker.invoke(RemoteRuntimeAgentInvoker.java:464)
	... 45 more
Caused by: javax.xml.bind.UnmarshalException
 - with linked exception:
[Exception [EclipseLink-25004] (Eclipse Persistence Services - 2.6.5.v20170607-b3d05bd): org.eclipse.persistence.exceptions.XMLMarshalException
Exception Description: An error occurred unmarshalling the document
Internal Exception: com.ctc.wstx.exc.WstxIOException: Invalid UTF-8 middle byte 0x3f (at char #225, byte #37)]
	at org.eclipse.persistence.jaxb.JAXBUnmarshaller.handleXMLMarshalException(JAXBUnmarshaller.java:1110)
	at org.eclipse.persistence.jaxb.JAXBUnmarshaller.unmarshal(JAXBUnmarshaller.java:638)
	at org.eclipse.persistence.jaxb.JAXBUnmarshaller.unmarshal(JAXBUnmarshaller.java:163)
	at oracle.odi.runtime.agent.invocation.util.XmlBindHelper.unmarshal(XmlBindHelper.java:105)
	at oracle.odi.runtime.agent.invocation.RemoteRuntimeAgentInvoker.invoke(RemoteRuntimeAgentInvoker.java:441)
	... 45 more
Caused by: Exception [EclipseLink-25004] (Eclipse Persistence Services - 2.6.5.v20170607-b3d05bd): org.eclipse.persistence.exceptions.XMLMarshalException
Exception Description: An error occurred unmarshalling the document
Internal Exception: com.ctc.wstx.exc.WstxIOException: Invalid UTF-8 middle byte 0x3f (at char #225, byte #37)
	at org.eclipse.persistence.exceptions.XMLMarshalException.unmarshalException(XMLMarshalException.java:120)
	at org.eclipse.persistence.internal.oxm.record.SAXUnmarshaller.convertSAXException(SAXUnmarshaller.java:1040)
	at org.eclipse.persistence.internal.oxm.record.SAXUnmarshaller.unmarshal(SAXUnmarshaller.java:946)
	at org.eclipse.persistence.internal.oxm.XMLUnmarshaller.unmarshal(XMLUnmarshaller.java:653)
	at org.eclipse.persistence.jaxb.JAXBUnmarshaller.unmarshal(JAXBUnmarshaller.java:635)
	... 48 more
Caused by: com.ctc.wstx.exc.WstxIOException: Invalid UTF-8 middle byte 0x3f (at char #225, byte #37)
	at com.ctc.wstx.sr.StreamScanner.constructFromIOE(StreamScanner.java:625)
	at com.ctc.wstx.sr.StreamScanner.loadMore(StreamScanner.java:997)
	at com.ctc.wstx.sr.StreamScanner.getNext(StreamScanner.java:754)
	at com.ctc.wstx.sr.BasicStreamReader.nextFromProlog(BasicStreamReader.java:2000)
	at com.ctc.wstx.sr.BasicStreamReader.next(BasicStreamReader.java:1134)
	at org.eclipse.persistence.internal.oxm.record.XMLStreamReaderReader.parse(XMLStreamReaderReader.java:98)
	at org.eclipse.persistence.internal.oxm.record.XMLStreamReaderReader.parse(XMLStreamReaderReader.java:86)
	at org.eclipse.persistence.internal.oxm.record.SAXUnmarshaller.unmarshal(SAXUnmarshaller.java:938)
	... 50 more
Caused by: java.io.CharConversionException: Invalid UTF-8 middle byte 0x3f (at char #225, byte #37)
	at com.ctc.wstx.io.UTF8Reader.reportInvalidOther(UTF8Reader.java:314)
	at com.ctc.wstx.io.UTF8Reader.read(UTF8Reader.java:212)
	at com.ctc.wstx.io.ReaderSource.readInto(ReaderSource.java:87)
	at com.ctc.wstx.io.BranchingReaderSource.readInto(BranchingReaderSource.java:57)
	at com.ctc.wstx.sr.StreamScanner.loadMore(StreamScanner.java:991)
	... 56 more

```

但是数据库通过ODI连接是没有问题的，SQL Developer连接也没问题。

突然想起来看了一下表空间，发现空间确实满了。扩容即可。


另外发现，Oracle 12c PDB数据库，表空间扩容，用这个
```alter database  datafile 'C:\APP\ADMINISTRATOR\VIRTUAL\ORADATA\ORCL\ORCLPDB\DEV_ODI_USER.DBF'  resize  10240M; 
```
发现无效，仍然是1024M
但是用这个就可以了，变成11g了。不知道具体原因~
```
ALTER TABLESPACE DEV_ODI_USER ADD DATAFILE'C:\APP\ADMINISTRATOR\VIRTUAL\ORADATA\ORCL\ORCLPDB\DEV_ODI_USER2.DBF' SIZE 10240M;
```