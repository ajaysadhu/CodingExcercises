# JAVA Lambdas

### Initial Template Code is available.
- A Message is encapsulated as a class which also contains id and timestamp
- Generic MessageTransformer (Functional Interface) is written apply a function to the argument.
- A set of MessageTransformers are written that does specific work on the Message.

### Method References
- With Functional Interfaces, only 1 method - apply is available. We can use Method Reference like Message::toString to run toString function as an apply method.
```
Lambda Structure:
 (Parameter param, Parameter param2) -> { return someValue; }

  This   
  static MessageTransformer<Instant> toTimestamp = new MessageTransformer<Instant>() {
        @Override
        public Instant apply(Message message) {
            return message.getTimestamp();
        }
    };
    
    becomes
    
    static MessageTransformer<String> toString = Message::toString;
```

### Best Practices:
- Try to eliminate creating new Functional Interfaces unless required
- Try to eliminate braces, return keyword
- Don't include parameter Types unless compiler requires it.
- If logic inside the lambda body is complex, create a new method and use method reference.