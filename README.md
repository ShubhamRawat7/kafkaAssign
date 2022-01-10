# kafkaAssign

## Producer.java

### To produce message as object
Add your message in ProducerRecord
```java
for (int i = 1; i <= 10; i++){
    User user=new User(i,"Girish",21,"B.Tech");
    kafkaProducer.send(new ProducerRecord("mytopic2",String.valueOf(user.getId()),user));
}
```
Here `mytopic2` is name of ***topic*** & `user` is object of **User** class

## Consumer.java
### To see consuming messages
Make sure you subscribed to the topic `mytopic2`
```java
List topics = new ArrayList();
topics.add("mytopic2");
kafkaConsumer.subscribe(topics);
```
### Writing Data into a file when consuming it
```java

while (true) {
        FileWriter fileWriter = new FileWriter("result.txt", true);
        ConsumerRecords<String, User> consumerRecords = kafkaConsumer.poll(Duration.ofSeconds(1));
        for (ConsumerRecord<String, User> consumerRecord : consumerRecords) {
            System.out.printf(
                "Topic: %s, Partition: %d, Value: %s%n",
                consumerRecord.topic(),
                consumerRecord.partition(),
                consumerRecord.value().toString());
            fileWriter.write(consumerRecord.value().toString() + "\n");
        }
        fileWriter.flush();
        fileWriter.close();
}
```
### Then
Just run the `Consumer.java` file. A terminal will open and there you can see your all messages from beginning produced by Producer.

### In result.txt
> {"id":1, "name":"Shubham Rawat", "age":21, "course":"MCA"}
>
> {"id":5, "name":"Shubham Rawat", "age":21, "course":"MCA"}
>
> {"id":7, "name":"Shubham Rawat", "age":21, "course":"MCA"}
>
> {"id":8, "name":"Shubham Rawat", "age":21, "course":"MCa"}
>
> {"id":2, "name":"Shubham Rawat", "age":21, "course":"MCA"}
>
> {"id":3, "name":"Shubham Rawat", "age":21, "course":"MCA"}
>
> {"id":9, "name":"Shubham Rawat", "age":21, "course":"MCA"}
>
> {"id":4, "name":"Shubham Rawat", "age":21, "course":"MCA"}
>
> {"id":6, "name":"Shubham Rawat", "age":21, "course":"MCA"}
>
> {"id":10, "name":"Shubham Rawat", "age":21, "course":"MCA"}
