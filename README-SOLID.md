# SOLID

Os cinco princípios SOLID são:

S — Princípio da Responsabilidade Única (Single Responsibility Principle)

O — Princípio Aberto/Fechado (Open/Closed Principle)

L — Princípio da Substituição de Liskov (Liskov Substitution Principle)

I — Princípio da Segregação de Interfaces (Interface Segregation Principle)

D — Princípio da Inversão de Dependência (Dependency Inversion Principle)

----------------------------------------------------------------------------

**SRP** - uma classe deve ter uma única razão para, ou seja a classe deve ter apenas uma responsabilidade.


#### Exemplo incorreto

```java
class PaymentProcessor {
    public void processPayment(Payment payment) {
        // Lógica para processar o pagamento
    }
}

class PaymentLogger {
    public void logPayment(Payment payment) {
        // Lógica para registrar informações de pagamento
    }
}
```

#### Exemplo correto:

```java
class PaymentHandler {
    public void processPayment(Payment payment) {
        // Lógica para processar o pagamento
        // Lógica para registrar informações de pagamento
    }
}
```

---------------------------------------------------------------------------------

**OCP** - As classes, módulus... devem estar abertas para extensão, mas fechadas para modificação, ou seja deve ser capaz de adicionar novos recursos sem alterar o código existente.

#### Exemplo incorreto

```java
class Shape {
    // Implementação genérica para todas as formas
}

class Circle extends Shape {
    // Lógica específica para cálculo de área de círculo
}

class Rectangle extends Shape {
    // Lógica específica para cálculo de área de retângulo
}
```

#### Exemplo correto:

```java
interface Shape {
    double calculateArea();
}

class Circle implements Shape {
    private double radius;

    // Construtor, getters e setters

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

class Rectangle implements Shape {
    private double width;
    private double height;

    // Construtor, getters e setters

    @Override
    public double calculateArea() {
        return width * height;
    }
}
```

----------------------------------------------------------------------

**LSP** - objetos de uma subclasse devem poder ser substituídos por objetos da classe base sem afetar a integridade do programa, garantindo que a herança seja utilizada de forma correta e não cause comportamentos inesperados

#### Exemplo incorreto

```java
class Bird {
    void fly() {
        // Lógica para voar
    }
}

class Ostrich extends Bird {
    void fly() {
        throw new UnsupportedOperationException("As avestruzes não voam");
    }
}
```

#### Exemplo correto:

```java
class Bird {
    void fly() {
        // Lógica para voar
    }
}

class Sparrow extends Bird {
    // Implementação específica para o pardal
}

class Ostrich extends Bird {
    void run() {
        // Lógica para correr
    }
}
```

-------------------------------------------------------------------------------

**ISP** - uma classe não deve ser forçada a implementar interfaces que não utiliza. Em vez disso, devem ser criadas interfaces mais específicas para cada contexto

#### Exemplo incorreto

```java
interface WorkerAndEater {
    void work();
    void eat();
}

class Human implements WorkerAndEater {
    // Implementações para work() e eat()
}

class Robot implements WorkerAndEater {
    // Implementações fictícias para work() e eat()
}
```


#### Exemplo correto

```java
interface Worker {
    void work();
}

interface Eater {
    void eat();
}

class Human implements Worker, Eater {
    // Implementações para work() e eat()
}

class Robot implements Worker {
    // Implementação para work()
}
```

-----------------------------------------------------

**DIP** - módulos de alto nível não devem depender diretamente de módulos de baixo nível. Ambos devem depender de abstrações.

#### Exemplo incorreto
```java
class EmailSender {
    public void sendEmail(String message) {
        // Lógica para enviar email
    }
}

class NotificationService {
    private final EmailSender emailSender;
    public NotificationService(EmailSender emailSender) {
        this.emailSender = emailSender;
    }
    public void sendNotification(String message) {
        emailSender.sendEmail(message);
    }
}
```

#### Exemplo correto
```java
interface MessageSender {
    void sendMessage(String message);
}

class EmailSender implements MessageSender {
    public void sendMessage(String message) {
        // Lógica para enviar email
    }
}
class SmsSender implements MessageSender {
    public void sendMessage(String message) {
        // Lógica para enviar SMS
    }
}
class NotificationService {
    private final MessageSender messageSender;
    public NotificationService(MessageSender messageSender) {
        this.messageSender = messageSender;
    }
    public void sendNotification(String message) {
        messageSender.sendMessage(message);
    }
}
```


### Conclusão

Conclusão
Os Princípios SOLID são fundamentais na criação de software bem estruturado e facilmente mantido. Ao incorporar esses princípios em projetos Java, a modularidade, a flexibilidade e a reusabilidade do código são impulsionadas.

A prática constante é um componente vital para aprofundar o entendimento e aprimorar as habilidades de design de software. Com esse guia, o leitor está preparado para iniciar a redação de um código mais sólido e de alta qualidade em Java. A compreensão completa de cada princípio e a aplicação cuidadosa nos projetos conduzem a sistemas mais robustos e sustentáveis ao longo do tempo.
