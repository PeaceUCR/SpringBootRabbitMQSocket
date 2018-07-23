# SpringBoot RabbitMQ as Broker Socket

This app inherits from https://github.com/PeaceUCR/SpringBootInDepth

Run before start the localhost RabbitMQ

Difference in application.properties  
  
    spring.rabbitmq.host=localhost
    spring.rabbitmq.port = 5672
    spring.rabbitmq.password=guest
    spring.rabbitmq.username=guest

in WebSocketConfig.java  
    
    //we’re configuring a message broker that will be used to route messages from one client to another.
    //the first line defines that the messages whose destination starts with “/topic” should be routed to the message broker. Message broker broadcasts messages to all the connected clients who are subscribed to a particular topic.
    //The second line defines that the messages whose destination starts with “/app” should be routed to message-handling methods
    @Override
    public void configureMessageBroker(MessageBrokerRegistry config) {
        config.setApplicationDestinationPrefixes("/app");

        // Use this for enabling a Full featured broker like RabbitMQ
        //port 61613
        //https://www.rabbitmq.com/stomp.html
        config.enableStompBrokerRelay("/topic")
                .setRelayHost("localhost")
                .setRelayPort(61613)
                .setClientLogin("guest")
                .setClientPasscode("guest");

    }
    
Ref:  
https://www.callicoder.com/spring-boot-websocket-chat-example/
https://www.rabbitmq.com/devtools.html
https://www.rabbitmq.com/stomp.html#d    