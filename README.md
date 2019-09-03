### Apache-RocketMQ
---
https://github.com/apache/rocketmq

https://github.com/alibaba/RocketMQ

```java
// openmessaging/src/test/java/io/openmessaging/rocketmq/producer/ProducerImplTest.java

@RunWith(MockitoJUintRunner.class)
public class ProducerImplTest {
  private Producer producer;
  
  @Mock
  private DefaultMQProducer rocketmqProducer;
  
  @Before
  public void init() throws NoSuchFieldException, IllegalAccessException {
    final MessagingAccessPoint messagingAccessPoint = OMS
      .getMessagingAccessPoint("oms:rocketmq://IP1:9876,IP2:9876/namespace");
    producer = messagingAccessPoint.createProducer();
    
    Field field = AbstractOMSProducer.class.getDeclaredField("rocketmqProducer");
    field.setAccessible(true);
    field.set(producer, rocketmqProducer);
    
    messagingAccessPoint.startup();
    producer.startup();
  }
  
  @Test
  public void testSend_OK() throws InterruptedException, RemotingException, MQClientException, MQBrokerException {
    SendResult sendResult = new SendResult();
    sendResult.setMsgId("TestMsgID");
    sendResult.setSendStatus(SendStatus.SEND_OK);
    when(rocketmqProducer.send(any(Message.class), anyLong())).thenReturn(sendResult);
    io.openmessaging.producer.SendREsult omsResult = 
      producer.send(producer.createBytesMessage("HELLO_TOPIC", new byte[] {'a'}));
      
    assertThat(omsResult.messageId()).isEqualTo("TestMsgID");
  }
  
  @Test
  public void testSend_Not_OK() throws InterruptedEception, RemotingException, MQClientException, MQBrokerException {}
  
  @Test
  public void testSend_WithException () throws InterruptedException, RemotingException, MQClientException, MQBrokerException {}
}

```

```
```

```
```


