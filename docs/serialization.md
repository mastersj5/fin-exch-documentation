# Serialization

## Table of Contents
1. [What is Serialization](#what-is-serialization)
    - [Kafka](#kafka)
    - [JSON Implementation](#json-implementation)
    - [Byte Implementation](#byte-implementation)
2. [Serializing](#serializing)
3. [Deserializing](#deserializing)


## What is Serialization

Serialization refers to the encoding of an object into a form of transportable data. This can take may forms but the most common are JSON and byte array serialization. In the project JSON is used but in the final product the serialization would have been switched to a byte array implementation.

### Kafka

- [Kafka](./glossary.md#kafka) is used for communication between the microservices, it sends data in a key value pair (topic, message). Each of these values can be serialized differently. 
  - The key/topic is serialized as a string. Strings although less efficient are by far the most easily readable implementation. These values are checked in the beginning of the listen function and using a byte array would be needlessly cumbersome on readability.
  - The value/message is serialized as a byte array. Byte arrays are more efficient especially when large objects are communicated. The project uses byte arrays as the make the larger messages more efficient and make deserialization easier and less error prone.
- The steps to configure Kafka for different serialization and deserialization formats are shown in [Serializing](#serializing) and [Deserializing](#deserializing) respectively.

### JSON Implementation
- The JSON implementation is the version of serialization present in the project but in the future we would like to move to byte array serialization. JSON is a standardized form of communicating objects. It is represented as a pair of curly brackets "{}" and inside are a list of variable name and value pairs separated by commas. An example can be seen below. JSONs can be transmitted as strings which makes them relatively quick and painless to implement.

```json
 {
    Source='SOD',
    CSN='0',
    ESN='0',
    time='2024/12/04',
    type='PendingCreateUser'
 }
```
- In order to convert the objects into JSON the project includes **Jackson** Object Mapper. Jackson is a library that provides the OMapper class giving various functionalities for converting objects into JSON.

### Byte Implementation
- The byte array implementation is how we would have implemented serialization in the final build of the project. As the name implies, a byte array is an array where each value in the array is a byte of data. It is one of the most basic forms of data. 

- In order to convert the objects into byte arrays the project utilizes **java.io.Serializable** and **ByteArrayStream**. These libraries need precise stipulations in order to be cross platform communicative. Firstly the original class of the object must have a unique id for deserialization. Additionally this class must also be in the exact same file location within the project. An example of both of these requirements are shown below.

```
<microservice>/src/main/java/CPS491FinancialExchange/models/User
```
```java
private static final long serialVersionUID = XXXXXXXXXXXXXXXXXXl;
```

## Serializing
1. In the `application.yml` file. Change the kaka *value-serializer* to the desired format.
```java
  producer:
    key-serializer: org.apache.kafka.common.serialization.StringSerializer
    value-serializer: org.apache.kafka.common.serialization.ByteArraySerializer
```
2. Alter the desired object class to implement *java.io.Serializable*. See the code block below.
 a. Change file location to a universal directory among all the projects.
 b. Add `import java.io.Serializable`
 c. Make sure the class `implements Serializable`
 d. Add a unique `serialVersionUID`
```java

import java.io.Serializable;

public class XXX implements Serializable {

    private static final long serialVersionUID = XXXXXXXXXXXXXXXXXXl;
```

3. If a Kafka producer and kafka template are present alter their arguments and the config's value serializer to be ByteArray
```java
@Configuration
public class KafkaProducerConfig {
    @Bean
    public ProducerFactory<String, byte[]> producerFactory() {
        Map<String, Object> configProps = new HashMap<>();
        configProps.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
        configProps.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
        configProps.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, ByteArraySerializer.class);
        return new DefaultKafkaProducerFactory<>(configProps);
    }

    @Bean
    public KafkaTemplate<String, byte[]> kafkaTemplate() {
        return new KafkaTemplate<>(producerFactory());
    }
```
 
4. Change the Message Producer to utilize byte arrays as well

```java
@Component
public class MessageProducer {
    @AutoWired
    private KafkaTemplate<String, byte[]> kafkaTemplate;

    public void sendMessage(String topic, byte[] message) {
        kafkaTemplate.send(topic, message);
    }

}
```

5. Serialize an object using the `java.io.ByteArrayOutputStream` class. Then send the message using the updated messageProducer.

```java
  try {
    ByteArrayOutputStream bos = new ByteArrayOutputStream(); 
    ObjectOutputStream oos = new ObjectOutputStream(bos); 
    oos.writeObject(object);
    messageProducer.sendMessage("Command", bos.toByteArray());
    bos.close();
    oos.close();
  } catch (Exception e) {
    System.err.println(e);
  }
```


## Deserializing
1. In the `application.yml` file. Change the kaka *value-serializer* to the desired format.
```java
  consumer:
    group-id: CAP3
    auto-offset-reset: earliest
    key-deserializer: org.apache.kafka.common.serialization.StringDeserializer
    value-deserializer: org.apache.kafka.common.serialization.ByteArrayDeserializer
```

2. Alter the desired object class to implement *java.io.Serializable* in the ***EXACT same way*** as in the equivalent serializer. See the code block below.
 a. Change file location to a universal directory among all the projects.
 b. Add `import java.io.Serializable`
 c. Make sure the class `implements Serializable`
 d. Add the same `serialVersionUID`
```java

import java.io.Serializable;

public class XXX implements Serializable {
  private static final long serialVersionUID = XXXXXXXXXXXXXXXXXXl;
```

3. Alter the Kafka message consumer to listen for byte arrays

```java
  @KafkaListener(topics = "Event", groupId = "CAP3")
  public void listen(byte[] message) {
```

4. Deserialize the byte array using `ByteArrayInputStream`

```java
ObjectInputStream ois = new ObjectInputStream(new ByteArrayInputStream(s));
Object o =  ois.readObject();
ois.close();
return (XXX) o;
```

**Additional Notes:**
- Kafka can send byte arrays natively but also has functionality for serializing classes. To do this a custom serializer needs to be made. This involves taking a class and breaking down each of its variables into a byte array. For additional instructions on serialization with Kafka and their custom serializers, the [Kafka Guide](https://assets.confluent.io/m/1b509accf21490f0/original/20170707-EB-Confluent_Kafka_Definitive-Guide_Complete.pdf?utm_medium=sem&utm_source=google&utm_campaign=ch.sem_br.nonbrand_tp.prs_tgt.dsa_mt.dsa_rgn.namer_lng.eng_dv.all_con.resources&utm_term=&placement=&device=c&creative=&session_ref=https://www.google.com/&_ga=2.184418662.1944723477.1710451033-617771951.1706545305&_gac=1.54811353.1710538902.CjwKCAjw48-vBhBbEiwAzqrZVCIsQwlz8YAm89yDBWUPNwq5MXOJxu_Y_YeTeuPnXDAu0ynByia5OBoCTgkQAvD_BwE) has all the information needed.
